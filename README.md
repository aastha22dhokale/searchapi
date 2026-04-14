package com.ing.datadist.batch.schedular;

import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.enums.ErrorType;
import com.ing.datadist.enums.RecordType;
import com.ing.datadist.service.FileIngestionService;
import com.ing.datadist.util.CsvTotalRecordsParser;
import com.ing.datadist.util.FileUtility;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.Job;
import org.springframework.batch.core.JobExecution;
import org.springframework.batch.core.JobParameters;
import org.springframework.batch.core.JobParametersBuilder;
import org.springframework.batch.core.explore.JobExplorer;
import org.springframework.batch.core.launch.JobLauncher;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Component;

import java.io.PrintWriter;
import java.io.StringWriter;
import java.time.LocalDateTime;
import java.util.concurrent.atomic.AtomicBoolean;

@Slf4j
@Component
public class BatchSchedular {

    private final JobLauncher jobLauncher;
    private final Job cofaceOUjob;
    private final Job cofaceLEJob;
    private final Job incapablesJob;
    private final Job leDeletionJob;
    private final JobExplorer jobExplorer;
    private final ErrorLogDAO errorLogDAO;
    private final FileIngestionService fileIngestionService;
    private final AtomicBoolean organisationUnitBatchRunning = new AtomicBoolean(false);
    private final AtomicBoolean legalEntityBatchRunning = new AtomicBoolean(false);
    private final AtomicBoolean incapablesBatchRunning = new AtomicBoolean(false);
    private final AtomicBoolean leDeletionBatchRunning = new AtomicBoolean(false);
    Boolean runFlagOU = true;
    Boolean runFlagLE = true;
    Boolean runFlagIncapables = true;
    Boolean runFlagLEDeletion = true;


    @Value("${spring.batch.schedular.organisationUnitCron}")
    private String organisationUnitCron;

    @Value("${spring.batch.schedular.legalEntityCron}")
    private String legalEntityCron;

    @Value("${spring.batch.schedular.incapablesCron}")
    private String incapablesCron;

    @Value("${spring.batch.schedular.leDeletionCron}")
    private String leDeletionCron;

    @Value("${ecs.cofaceIncapablesFileName}")
    private String cofaceIncapablesFileName;

    @Value("${ecs.cofaceOUFileName}")
    private String cofaceOUFileName;

    @Value("${ecs.cofaceLEParentFileName}")
    private String cofaceLEParentFileName;

    @Value("${ecs.cofaceLEChildFileName}")
    private String cofaceLEChildFileName;

    @Value("${ecs.cofaceLEDeleteFileName:COFACE_LE_DEL.csv}")
    private String cofaceLEDeleteFileName;

    @Value("${ecs.readFileFrom}")
    private String readFileFrom;


    public BatchSchedular(JobLauncher jobLauncher,
                          @Qualifier("organisationUnitEnrichmentJob") Job job,
                          @Qualifier("LegalEntityEnrichmentJob") Job cofaceLEJob,
                          @Qualifier("IncapablesEnrichmentJob") Job incapablesJob,
                          @Qualifier("LegalEntityDeletionJob") Job leDeletionJob,
                          JobExplorer jobExplorer, ErrorLogDAO errorLogDAO, FileIngestionService fileIngestionService) {    this.jobLauncher = jobLauncher;
        this.cofaceOUjob = job;
        this.cofaceLEJob = cofaceLEJob;
        this.incapablesJob = incapablesJob;
        this.leDeletionJob = leDeletionJob;
        this.jobExplorer = jobExplorer;
        this.errorLogDAO = errorLogDAO;
        this.fileIngestionService = fileIngestionService;
    }

    @Scheduled(cron = "${spring.batch.schedular.organisationUnitCron}")
    public void run() {
        log.info("OrganisationUnit Batch Schedular started:{}", LocalDateTime.now());
        JobExecution execution = null;
        String fileId = null;
        String fileName = null;

        if (!organisationUnitBatchRunning.compareAndSet(false, true)) {
            log.info("OrganisationUnit Batch still running, skipping this run :{}", LocalDateTime.now());
            return;
        }
        if (runFlagOU) {
            try {
                log.info("OrganisationUnit Batch Schedular cron:{} started:{}", organisationUnitCron, LocalDateTime.now());

                // Fetch file name from configuration
                fileName = cofaceOUFileName;
                String filePath = buildFilePath(fileName);

                // Calculate total records from CSV file BEFORE registration
                Long ouTotalRecords = 0L;
                Long ouFileSize = 0L;

                log.info("OrganisationUnit File: {} - Total records from file: {}, File size: {}",
                        fileName, ouTotalRecords, ouFileSize);

                fileId = fileIngestionService.registerFileIngestion(
                        fileName,
                        "COFACE_OPS",
                        "OPS",
                        "COFACE_SYSTEM",
                        "DAILY",
                        ouTotalRecords
                );

                JobParameters jobParameters = new JobParametersBuilder(jobExplorer)
                        .addLong("run.id", System.currentTimeMillis())
                        .addString("opsFileId", fileId)
                        .addString("fileName", fileName)
                        .toJobParameters();

                // Mark file processing start
                fileIngestionService.markFileProcessingStart(fileId, String.valueOf(System.currentTimeMillis()));

                execution = jobLauncher.run(cofaceOUjob, jobParameters);

                // Update file processing completion based on execution status
                String formattedSize = FileUtility.formatFileSize(ouFileSize);

                if (execution.getStatus().toString().equals("COMPLETED")) {
                    // Get record counts from job execution context
                    Long totalRecords = getTotalRecordsFromExecution(execution,"totalRecordsOps");
                    Long processedRecords = getProcessedRecordsFromExecution(execution,"processedRecordsOps");
                    Long failedRecords = getFailedRecordsFromExecution(execution,"failedRecordsOps");

                    // If execution context doesn't have counts, use parsed value for total
                    if (totalRecords == 0L && ouTotalRecords > 0L) {
                        totalRecords = ouTotalRecords;
                    }

                    // For successful completion, if processedRecords is 0, assume all records were processed
                    if (processedRecords == 0L && totalRecords > 0L) {
                        processedRecords = totalRecords;
                    }

                    // If no failures logged, set to 0
                    if (failedRecords == null) {
                        failedRecords = 0L;
                    }

                    log.info("OrganisationUnit Batch completed - fileSize: {}, totalRecords: {}, processedRecords: {}, failedRecords: {}",
                            formattedSize, totalRecords, processedRecords, failedRecords);

                    fileIngestionService.updateFileProcessingEnd(fileId, ouFileSize, null,
                            totalRecords, processedRecords, failedRecords);
                } else {
                    String errorMsg = "Batch execution failed with status: " + execution.getStatus();
                    log.error("OrganisationUnit Batch failed: {}", errorMsg);
                    fileIngestionService.markFileProcessingFailed(fileId, errorMsg);
                }
            } catch (Exception e) {
                log.error("Exception in OrganisationUnit Batch Schedular", e);

                // Log to DD_ERROR_LOG table
                try {
                    StringWriter sw = new StringWriter();
                    e.printStackTrace(new PrintWriter(sw));
                    errorLogDAO.logError(
                            RecordType.ORGANISATION_UNIT,
                            "BATCH_JOB",
                            null,
                            ErrorType.PARSING_ERROR,
                            "Batch Scheduler Exception: " + e.getMessage(),
                            null,
                            fileName,
                            sw.toString(),
                            fileId  // File ID
                    );
                } catch (Exception logEx) {
                    log.error("Failed to log batch scheduler error", logEx);
                }

                // Mark file as failed
                if (fileId != null) {
                    try {
                        fileIngestionService.markFileProcessingFailed(fileId, "Exception in batch scheduler: " + e.getMessage());
                    } catch (Exception fileEx) {
                        log.error("Failed to mark file as failed", fileEx);
                    }
                }
            } finally {
                if (execution != null) {
                    log.info("OrganisationUnit Batch Schedular finished name:{} status:{}", cofaceOUjob.getName(), execution.getStatus());
                } else {
                    log.info("OrganisationUnit Batch Schedular failed name:{}", cofaceOUjob.getName());
                }
                organisationUnitBatchRunning.set(false);
            }
        }else{
            log.info("OrganisationUnit Batch Schedular flag stopped");
        }
        runFlagOU =  false;
    }

    @Scheduled(cron = "${spring.batch.schedular.legalEntityCron}")
    public void runLE() {
        log.info("LegalEntity Batch Schedular started:{}", LocalDateTime.now());
        JobExecution execution = null;
        String parentFileId = null;
        String childFileId = null;
        String parentFileName = null;
        String childFileName = null;

        if (!legalEntityBatchRunning.compareAndSet(false, true)) {
            log.info("LegalEntity Batch still running, skipping this run :{}", LocalDateTime.now());
            return;
        }
        if(runFlagLE) {
            try {
                log.info("LegalEntity Batch Schedular cron:{} started:{}", legalEntityCron, LocalDateTime.now());

                // Fetch PARENT file name from configuration
                parentFileName = cofaceLEParentFileName;
                String parentFilePath = buildFilePath(parentFileName);
                Long parentTotalRecords = 0L;
                Long parentFileSize = 0L;

                parentFileId = fileIngestionService.registerFileIngestion(
                        parentFileName,
                        "COFACE_LE_PARENT",
                        "LE",
                        "COFACE_SYSTEM",
                        "DAILY",
                        parentTotalRecords
                );

                // Fetch CHILD file name from configuration
                childFileName = cofaceLEChildFileName;
                String childFilePath = buildFilePath(childFileName);
                Long childTotalRecords = 0L;
                Long childFileSize = 0L;

                childFileId = fileIngestionService.registerFileIngestion(
                        childFileName,
                        "COFACE_LE_CHILD",
                        "LE",
                        "COFACE_SYSTEM",
                        "DAILY",
                        childTotalRecords
                );

                JobParameters jobParameters = new JobParametersBuilder(jobExplorer)
                        .addLong("run.id", System.currentTimeMillis())
                        .addString("leParentFileId", parentFileId)
                        .addString("leChildFileId",  childFileId)
                        .addString("leParentFileName", parentFileName)
                        .addString("leChildFileName", childFileName)
                        .toJobParameters();

                // Mark file processing start
                fileIngestionService.markFileProcessingStart(parentFileId, String.valueOf(System.currentTimeMillis()));
                fileIngestionService.markFileProcessingStart(childFileId, String.valueOf(System.currentTimeMillis()));

                execution = jobLauncher.run(cofaceLEJob, jobParameters);

                // Update file processing completion based on execution status
                String parentFormattedSize = FileUtility.formatFileSize(parentFileSize);
                String childFormattedSize = FileUtility.formatFileSize(childFileSize);

                if (execution.getStatus().toString().equals("COMPLETED")) {
                    // Get record counts from job execution context
                    Long totalRecords = getTotalRecordsFromExecution(execution,"totalRecordsLEP");
                    Long processedRecords = getProcessedRecordsFromExecution(execution,"processedRecordsLEP");
                    Long failedRecords = getFailedRecordsFromExecution(execution,"failedRecordsLEP");

                    // If execution context doesn't have counts, use parsed values
                    if (totalRecords == 0L && parentTotalRecords > 0L) {
                        totalRecords = parentTotalRecords;
                    }

                    // For successful completion, if processedRecords is 0, assume all records were processed
                    if (processedRecords == 0L && totalRecords > 0L) {
                        processedRecords = totalRecords;
                    }

                    // If no failures logged, set to 0
                    if (failedRecords == null) {
                        failedRecords = 0L;
                    }

                    log.info("LegalEntity Batch completed - PARENT fileSize: {}, CHILD fileSize: {}, totalRecords: {}, processedRecords: {}, failedRecords: {}",
                            parentFormattedSize, childFormattedSize, totalRecords, processedRecords, failedRecords);

                    fileIngestionService.updateFileProcessingEnd(parentFileId, parentFileSize, null,
                            totalRecords, processedRecords, failedRecords);

                    Long totalRecordsChild = getTotalRecordsFromExecution(execution,"totalRecordsLEC");
                    Long processedRecordsChild = getProcessedRecordsFromExecution(execution,"processedRecordsLEC");
                    Long failedRecordsChild = getFailedRecordsFromExecution(execution,"failedRecordsLEC");

                    log.info("LegalEntity Batch completed - Child fileSize: {}, CHILD fileSize: {}, totalRecords: {}, processedRecords: {}, failedRecords: {}",
                            parentFormattedSize, childFormattedSize, totalRecordsChild, processedRecordsChild, failedRecordsChild);

                    fileIngestionService.updateFileProcessingEnd(childFileId, childFileSize, null,
                            totalRecordsChild, processedRecordsChild, failedRecordsChild);
                } else {
                    String errorMsg = "Batch execution failed with status: " + execution.getStatus();
                    log.error("LegalEntity Batch failed: {}", errorMsg);
                    fileIngestionService.markFileProcessingFailed(parentFileId, errorMsg);
                    fileIngestionService.markFileProcessingFailed(childFileId, errorMsg);
                }
            } catch (Exception e) {
                log.error("Exception in LegalEntity Batch Schedular", e);

                // Log to DD_ERROR_LOG table
                try {
                    StringWriter sw = new StringWriter();
                    e.printStackTrace(new PrintWriter(sw));

                    errorLogDAO.logError(
                            RecordType.ORGANISATION_PARENT,
                            "BATCH_JOB",
                            null,
                            ErrorType.DATABASE_ERROR,
                            "Batch Scheduler Exception: " + e.getMessage(),
                            null,
                            parentFileName,
                            sw.toString(),
                            parentFileId
                    );
                } catch (Exception logEx) {
                    log.error("Failed to log batch scheduler error", logEx);
                }

                // Mark files as failed
                if (parentFileId != null) {
                    try {
                        fileIngestionService.markFileProcessingFailed(parentFileId, "Exception in batch scheduler: " + e.getMessage());
                    } catch (Exception fileEx) {
                        log.error("Failed to mark parent file as failed", fileEx);
                    }
                }
                if (childFileId != null) {
                    try {
                        fileIngestionService.markFileProcessingFailed(childFileId, "Exception in batch scheduler: " + e.getMessage());
                    } catch (Exception fileEx) {
                        log.error("Failed to mark child file as failed", fileEx);
                    }
                }
            } finally {
                if (execution != null) {
                    log.info("LegalEntity Batch Schedular finished name:{} status:{}", cofaceLEJob.getName(), execution.getStatus());
                } else {
                    log.info("LegalEntity Batch Schedular failed name:{}", cofaceLEJob.getName());
                }
                legalEntityBatchRunning.set(false);
            }
        }else{
            log.info("LegalEntity Batch Schedular flag stopped");
        }
        runFlagLE =  false;
    }

    /**
     * Extract total records processed from job execution context
     */
    private Long getTotalRecordsFromExecution(JobExecution execution, String val) {
        try {
            Object totalRecords = execution.getExecutionContext().get(val);
            return totalRecords != null ? Long.valueOf(totalRecords.toString()) : 0L;
        } catch (Exception e) {
            log.warn("Unable to retrieve totalRecords from job execution context", e);
            return 0L;
        }
    }

    /**
     * Extract processed records from job execution context
     */
    private Long getProcessedRecordsFromExecution(JobExecution execution,String val) {
        try {
            Object processedRecords = execution.getExecutionContext().get(val);
            return processedRecords != null ? Long.valueOf(processedRecords.toString()) : 0L;
        } catch (Exception e) {
            log.warn("Unable to retrieve processedRecords from job execution context", e);
            return 0L;
        }
    }

    /**
     * Extract failed records from job execution context
     */
    private Long getFailedRecordsFromExecution(JobExecution execution,String val) {
        try {
            Object failedRecords = execution.getExecutionContext().get(val);
            return failedRecords != null ? Long.valueOf(failedRecords.toString()) : 0L;
        } catch (Exception e) {
            log.warn("Unable to retrieve failedRecords from job execution context", e);
            return 0L;
        }
    }

    /**
     * Build file path based on readFileFrom configuration
     */
    private String buildFilePath(String fileName) {
        if ("RESOURCES".equals(readFileFrom)) {
            return "src/main/resources/" + fileName;
        } else if ("ECS".equals(readFileFrom)) {
            // For ECS, return just the file name - it will be fetched from S3
            return fileName;
        } else {
            // Default to resources
            return "src/main/resources/" + fileName;
        }
    }

    @Scheduled(cron = "${spring.batch.schedular.incapablesCron}")
    public void runIncapables() {
        log.info("Incapables Batch Schedular started:{}", LocalDateTime.now());
        JobExecution execution = null;
        String fileId = null;
        String fileName = null;

        if (!incapablesBatchRunning.compareAndSet(false, true)) {
            log.info("Incapables Batch still running, skipping this run :{}", LocalDateTime.now());
            return;
        }
        if (runFlagIncapables) {
            try {
                log.info("Incapables Batch Schedular cron:{} started:{}", incapablesCron, LocalDateTime.now());

                fileName = cofaceIncapablesFileName;
                String filePath = buildFilePath(fileName);

                // Parse total records from last line of CSV file
                Long incapablesTotalRecords = CsvTotalRecordsParser.getTotalRecordsFromCsv(filePath);
                Long incapablesFileSize = CsvTotalRecordsParser.getFileSizeInBytes(filePath);

                log.info("Incapables File: {} - Total records from file: {}, File size: {}",
                        fileName, incapablesTotalRecords, incapablesFileSize);

                fileId = fileIngestionService.registerFileIngestion(
                        fileName,
                        "COFACE_INCAPABLES",
                        "INCAPABLES",
                        "COFACE_SYSTEM",
                        "DAILY",
                        incapablesTotalRecords
                );

                JobParameters jobParameters = new JobParametersBuilder(jobExplorer)
                        .addLong("run.id", System.currentTimeMillis())
                        .addString("fileId", fileId)
                        .addString("fileName", fileName)
                        .toJobParameters();
                fileIngestionService.markFileProcessingStart(fileId, String.valueOf(System.currentTimeMillis()));
                execution = jobLauncher.run(incapablesJob, jobParameters);

                // Update file processing completion based on execution status
                String formattedSize = FileUtility.formatFileSize(incapablesFileSize);

                if (execution.getStatus().toString().equals("COMPLETED")) {
                    // Get record counts from job execution context
                    Long totalRecords = getTotalRecordsFromExecution(execution,"totalRecordsICP");
                    Long processedRecords = getProcessedRecordsFromExecution(execution,"processedRecordsICP");
                    Long failedRecords = getFailedRecordsFromExecution(execution,"failedRecordsICP");

                    // If execution context doesn't have counts, use parsed value for total
                    if (totalRecords == 0L && incapablesTotalRecords > 0L) {
                        totalRecords = incapablesTotalRecords;
                    }

                    // For successful completion, if processedRecords is 0, assume all records were processed
                    if (processedRecords == 0L && totalRecords > 0L) {
                        processedRecords = totalRecords;
                    }

                    // If no failures logged, set to 0
                    if (failedRecords == null) {
                        failedRecords = 0L;
                    }

                    log.info("Incapables Batch completed - fileSize: {}, totalRecords: {}, processedRecords: {}, failedRecords: {}",
                            formattedSize, totalRecords, processedRecords, failedRecords);

                    fileIngestionService.updateFileProcessingEnd(fileId, incapablesFileSize, null,
                            totalRecords, processedRecords, failedRecords);
                } else {
                    String errorMsg = "Batch execution failed with status: " + execution.getStatus();
                    log.error("Incapables Batch failed: {}", errorMsg);
                    fileIngestionService.markFileProcessingFailed(fileId, errorMsg);
                }
            } catch (Exception e) {
                log.error("Exception in Incapables Batch Schedular", e);

                // Log to DD_ERROR_LOG table
                try {
                    StringWriter sw = new StringWriter();
                    e.printStackTrace(new PrintWriter(sw));
                    errorLogDAO.logError(
                            RecordType.INCAPABLE,
                            null,  // externalIdentifier
                            null,  // ddUuid
                            ErrorType.PROCESSING_ERROR,
                            e.getMessage(),
                            null,  // apiEndpoint
                            null,  // requestPayload
                            null,  // responsePayload
                            sw.toString()  // stackTrace
                    );
                } catch (Exception logEx) {
                    log.error("Failed to log error to DD_ERROR_LOG", logEx);
                }

                if (fileId != null) {
                    fileIngestionService.markFileProcessingFailed(fileId, e.getMessage());
                }
            } finally {
                if (execution != null) {
                    log.info("Incapables Batch Schedular finished name:{} status:{}", incapablesJob.getName(), execution.getStatus());
                } else {
                    log.info("Incapables Batch Schedular failed name:{}", incapablesJob.getName());
                }
                incapablesBatchRunning.set(false);
            }
        } else {
            log.info("Incapables Batch Schedular flag stopped");
        }
        runFlagIncapables = false;
    }

    @Scheduled(cron = "${spring.batch.schedular.leDeletionCron:0 */5 * * * *}")
    public void runLEDeletion() {
        log.info("LegalEntity Deletion Batch Schedular started:{}", LocalDateTime.now());
        JobExecution execution = null;
        String fileId = null;
        String fileName = null;

        if (!leDeletionBatchRunning.compareAndSet(false, true)) {
            log.info("LegalEntity Deletion Batch still running, skipping this run :{}", LocalDateTime.now());
            return;
        }
        if (runFlagLEDeletion) {
            try {
                log.info("LegalEntity Deletion Batch Schedular cron:{} started:{}", leDeletionCron, LocalDateTime.now());

                // Fetch file name from configuration
                fileName = cofaceLEDeleteFileName;
                String filePath = buildFilePath(fileName);

                Long totalRecords = 0L;
                Long fileSize = 0L;

                fileId = fileIngestionService.registerFileIngestion(
                        fileName,
                        "COFACE_LE_DELETION",
                        "LE",
                        "COFACE_SYSTEM",
                        "DAILY",
                        totalRecords
                );

                JobParameters jobParameters = new JobParametersBuilder(jobExplorer)
                        .addLong("run.id", System.currentTimeMillis())
                        .addString("leDeletionFileId", fileId)
                        .addString("fileName", fileName)
                        .toJobParameters();

                // Mark file processing start
                fileIngestionService.markFileProcessingStart(fileId, String.valueOf(System.currentTimeMillis()));

                execution = jobLauncher.run(leDeletionJob, jobParameters);

                // Update file processing completion based on execution status
                if (execution.getStatus().toString().equals("COMPLETED")) {
                    log.info("LegalEntity Deletion Batch completed - fileId: {}", fileId);
                } else {
                    String errorMsg = "Batch execution failed with status: " + execution.getStatus();
                    log.error("LegalEntity Deletion Batch failed: {}", errorMsg);
                    fileIngestionService.markFileProcessingFailed(fileId, errorMsg);
                }
            } catch (Exception e) {
                log.error("Exception in LegalEntity Deletion Batch Schedular", e);

                // Log to DD_ERROR_LOG table
                try {
                    StringWriter sw = new StringWriter();
                    e.printStackTrace(new PrintWriter(sw));

                    errorLogDAO.logError(
                        RecordType.LEGAL_ENTITY_DELETION,
                        "BATCH_JOB",
                        null,
                        ErrorType.DATABASE_ERROR,
                        "Batch Scheduler Exception: " + e.getMessage(),
                        null,
                        fileName,
                        sw.toString(),
                        fileId
                    );
                } catch (Exception logEx) {
                    log.error("Failed to log batch scheduler error", logEx);
                }

                // Mark file as failed
                if (fileId != null) {
                    try {
                        fileIngestionService.markFileProcessingFailed(fileId, "Exception in batch scheduler: " + e.getMessage());
                    } catch (Exception fileEx) {
                        log.error("Failed to mark file as failed", fileEx);
                    }
                }
            } finally {
                if (execution != null) {
                    log.info("LegalEntity Deletion Batch Schedular finished name:{} status:{}", leDeletionJob.getName(), execution.getStatus());
                } else {
                    log.info("LegalEntity Deletion Batch Schedular failed name:{}", leDeletionJob.getName());
                }
                leDeletionBatchRunning.set(false);
            }
        } else {
            log.info("LegalEntity Deletion Batch Schedular flag stopped");
        }
        runFlagLEDeletion = false;
    }
}
package com.ing.datadist.batch.config;

import com.ing.datadist.batch.listener.CsvParsingSkipListener;
import com.ing.datadist.batch.processor.*;
import com.ing.datadist.batch.processor.OrganisationUnitEnrichmentProcessor;
import com.ing.datadist.batch.tasklet.LEDeletionApiTasklet;
import com.ing.datadist.batch.tasklet.IncapablesApiTasklet;
import com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet;
import com.ing.datadist.batch.tasklet.OrganisationUnitSearchApiTasklet;
import com.ing.datadist.dao.LegalEntityDeletionDAO;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.dao.IncapablesDAO;
import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.dao.queries.OrganisationUnitQueries;
import com.ing.datadist.domain.*;
import com.ing.datadist.enums.RecordType;
import com.ing.datadist.domain.fileinput.LegalEntityParent;
import com.ing.datadist.domain.fileinput.OrganisationUnit;
import com.ing.datadist.domain.incapables.IncapableRelationship;
import com.ing.datadist.ecs.services.FileProviderService;
import com.ing.datadist.retention.config.DataRetentionConfig;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.*;
import org.springframework.batch.core.configuration.annotation.StepScope;
import org.springframework.batch.core.job.builder.JobBuilder;
import org.springframework.batch.core.launch.support.RunIdIncrementer;
import org.springframework.batch.core.repository.JobRepository;
import org.springframework.batch.core.scope.context.ChunkContext;
import org.springframework.batch.core.scope.context.StepSynchronizationManager;
import org.springframework.batch.core.step.builder.StepBuilder;
import org.springframework.batch.item.database.JdbcBatchItemWriter;
import org.springframework.batch.item.database.builder.JdbcBatchItemWriterBuilder;
import org.springframework.batch.item.file.FlatFileItemReader;
import org.springframework.batch.item.file.FlatFileParseException;
import org.springframework.batch.item.file.builder.FlatFileItemReaderBuilder;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.core.io.Resource;
import org.springframework.dao.DataIntegrityViolationException;
import org.springframework.jdbc.UncategorizedSQLException;
import org.springframework.transaction.PlatformTransactionManager;
import com.ing.datadist.service.FileIngestionService;

import javax.sql.DataSource;

import java.sql.BatchUpdateException;

import static com.ing.datadist.batch.config.BatchConstants.*;
import static com.ing.datadist.domain.fileinput.Incapables.*;
import static com.ing.datadist.domain.fileinput.LegalEntityChild.*;
import static com.ing.datadist.domain.fileinput.LegalEntityParent.*;
import static com.ing.datadist.domain.fileinput.OrganisationUnit.*;

@Slf4j
@Configuration
public class BatchJobConfig {


    private final static String COFACE_OPS_BATCH_FILE_READER_NAME = "organisationUnitReader";
    private final static String COFACE_OPS_BATCH_STEP_NAME = "organisationUnitEnrichmentStep";
    private final static String COFACE_OPS_BATCH_JOB_NAME = "organisationUnitEnrichmentJob";
    private final static String COFACE_LE_BATCH_JOB_NAME = "LegalEntityEnrichmentJob";
    private final static String COFACE_LE_BATCH_PARENT_FILE_READER_NAME = "legalEntityParentReader";
    private final static String COFACE_LE_BATCH_CHILD_FILE_READER_NAME = "legalEntityChildReader";
    String LEGAL_ENTITY_PARENT_TABLE_INSERT_SQL =
            "INSERT INTO DD_LEGAL_ENTITY_PARENT_TBL (" +
                    "DD_UUID, ORG_STATUS, ORG_NAME, ORG_OTHER_NAME, ORG_OTHER_NAME_TYPE, " +
                    "ADR_UNSTRUCTURED_ADDRESS, ADR_POSTALADDRESS_STREETNM, ADR_POSTALADDRESS_HOUSENUM, " +
                    "ADR_POSTALADDRESS_HOUSEADD, ADR_POSTALADDRESS_POSTALCD, ADR_POSTALADDRESS_CITYNAME, " +
                    "ADR_POSTALADDRESS_CNTRYCD, ORG_LEGAL_FORM, ORG_BUSINESS_CLOSE_DOWN_DATE, " +
                    "LE_LEGAL_STATUS, ORG_DATE_OF_FOUNDATION, LE_PREFERRED_LANGUAGE, " +
                    "ADR_DIGITALADDR_FULLTEL, NSSO_EXTL_IDENTIFIER, " +
                    "ASMT_VAT_STATUS, NSSO_EXTL_IDENTIFIER_STATUS, EXTERNALIDENTIFIER_VAL, " +
                    "FILE_ID) " +
                    "VALUES (" +
                    ":orgUUID, :orgStatus, :orgName, :orgOtherName, :orgOtherNameType, " +
                    ":adrUnstructuredAddress, :adrPostalAddressStreetName, :adrPostalAddressHouseNum, " +
                    ":adrPostalAddressHouseNumAdd, :adrPostalAddressPostalCode, :adrPostalAddressCityName, " +
                    ":adrPostalAddressCountryCode, :orgLegalForm, :orgBusinessClosedownDate, " +
                    ":lELegalStatus, :orgDateOfFoundation, :lEPreferredLanguage, " +
                    ":adrDigitalAddrFullTel, :nssoExternalIdentifier, " +
                    ":asmtVatStatus, :nssoExternalIdentifierStatus, :leExternalIdentifier, " +
                    ":fileId)";
    String LEGAL_ENTITY_CHILD_TABLE_INSERT_SQL =
            "INSERT INTO DD_LEGAL_ENTITY_CHILD_TBL (" +
                    "DD_UUID, INDUSTRY_CLASS_CODE, INDUSTRY_CLASS_CODE_RANK, INDUSTRY_CLASS_EFF_DATE, INDUSTRY_CLASS_END_DATE, " +
                    "FILE_ID) " +
                    "VALUES (" +
                    ":orgUUID, :industryClassCode, :industryClassRank, :industryClassEffDate, :industryClassEndDate, :fileId)";

    @Autowired
    FileProviderService fileProviderService;
    @Autowired
    private MappingDAO mappingDAO;
    @Autowired
    private ErrorLogDAO errorLogDAO;
    @Autowired
    private TaskletLeDeletionDomainWrapper taskletLeDeletionDomainWrapper;
    @Autowired
    private LegalEntityDeletionDAO legalEntityDeletionDAO;
    @Autowired
    private FileIngestionService fileIngestionService;
    @Value("${ecs.bucketName}")
    private String bucketName;
    @Value("${ecs.cofaceOUFileName}")
    private String cofaceOUFileName;
    @Value("${ecs.cofaceLEParentFileName}")
    private String cofaceLEParentFileName;
    @Value("${ecs.cofaceLEChildFileName}")
    private String cofaceLEChildFileName;
    @Value("${ecs.cofaceIncapablesFileName:CofaceIncapables.csv}")
    private String cofaceIncapablesFileName;
    @Value("${ecs.cofaceLEDeleteFileName:COFACE_LE_DEL.csv}")
    private String cofaceLEDeleteFileName;
    @Value("${ecs.readFileFrom}")
    private String readFileFrom;
    @Value("${app.input-file}")
    private Resource resourceOUFile;
    @Value("${app.le-parent-file}")
    private Resource resourceLEParentFile;
    @Value("${app.le-child-file}")
    private Resource resourceLEChildFile;
    @Value("${app.incapables-file}")
    private Resource resourceIncapablesFile;
    @Value("${app.le-delete-file:classpath:COFACE_LE_DEL.csv}")
    private Resource resourceLEDeleteFile;

    @Bean
    @StepScope
    public FlatFileItemReader<OrganisationUnitDomain> organisationUnitReader() {
        String fileId = StepSynchronizationManager.getContext().getStepExecution()
                .getJobParameters().getString("opsFileId");
        return new FlatFileItemReaderBuilder<OrganisationUnitDomain>()
                .name(COFACE_OPS_BATCH_FILE_READER_NAME)
                .resource(getFileForLocalRun(readFileFrom, cofaceOUFileName,fileId))
                .delimited()
                .names(OrganisationUnit.LE_EXTERNAL_IDENTIFIER, OPS_EXTERNAL_IDENTIFIER_VAL, ORGANISATION_UNIT_NAME,
                        ADDRESS, UNIT_POSTAL_ADDRESS_STREET_NM, UNIT_POSTAL_ADDRESS_HOUSE_NUM,
                        UNIT_POSTAL_ADDRESS_HOUSE_ADD, UNIT_POSTAL_ADDRESS_POSTAL_CD,
                        UNIT_POSTAL_ADDRESS_CITY_NAME, UNIT_POSTAL_ADDRESS_CNTRY_CD,
                        OPS_EXT_ID_DATE_OF_ISSUE, OPS_EXT_ID_EXPIRY_DATE,
                        UNIT_DIGITAL_ADDR_EMAIL,UNIT_DIGITAL_ADDR_FULL_TEL)
                .fieldSetMapper(new OrganisationUnitFieldSetMapper())
                .linesToSkip(1)
                .build();
    }

    @Bean
    public OrganisationUnitEnrichmentProcessor organisationUnitProcessor() {
        return new OrganisationUnitEnrichmentProcessor(mappingDAO, errorLogDAO);
    }


    @Bean
    public JdbcBatchItemWriter<OrganisationUnitDomainWrapper> organisationUnitWriter(DataSource dataSource) {
        return new JdbcBatchItemWriterBuilder<OrganisationUnitDomainWrapper>()
                .sql(OrganisationUnitQueries.INSERT_ORGANISATION_UNIT)
                .beanMapped()
                .dataSource(dataSource)
                .build();
    }


    @Bean
    public Step organisationUnitEnrichmentStep(JobRepository jobRepository,
                                               PlatformTransactionManager transactionManager,
                                               FlatFileItemReader<OrganisationUnitDomain> organisationUnitReader,
                                               OrganisationUnitEnrichmentProcessor organisationUnitProcessor,
                                               JdbcBatchItemWriter<OrganisationUnitDomainWrapper> organisationUnitWriter) {
        // Get file context for error logging
        String fileId = null;
        String batchId = null;
        try {
            fileId = StepSynchronizationManager.getContext().getStepExecution()
                    .getJobParameters().getString("opsFileId");
            batchId = String.valueOf(StepSynchronizationManager.getContext().getStepExecution()
                    .getJobExecution().getId());
        } catch (Exception e) {
            log.warn("Could not get file context for skip listener: {}", e.getMessage());
        }

        CsvParsingSkipListener<OrganisationUnitDomain, OrganisationUnitDomainWrapper> skipListener =
                new CsvParsingSkipListener<>(errorLogDAO, RecordType.ORGANISATION_UNIT,
                        cofaceOUFileName, batchId, fileId);

        return new StepBuilder(COFACE_OPS_BATCH_STEP_NAME, jobRepository)
                .<OrganisationUnitDomain, OrganisationUnitDomainWrapper>chunk(100, transactionManager)
                .reader(organisationUnitReader)
                .processor(organisationUnitProcessor)
                .writer(organisationUnitWriter)
                .listener((StepExecutionListener) organisationUnitProcessor)
                .listener(new ChunkListener() {
                    @Override
                    public void afterChunk(ChunkContext context) {
                        organisationUnitProcessor.flushNewMappings();
                    }
                })
                .faultTolerant()
                .skip(FlatFileParseException.class)
                .skipLimit(100)
                .listener(skipListener)
                .build();
    }

    @Bean
    public Step organisationUnitSearchApiTaskletStep(JobRepository jobRepository,
                                                     PlatformTransactionManager transactionManager,
                                                     OrganisationUnitSearchApiTasklet organisationUnitSearchApiTasklet) {
        return new StepBuilder("organisationUnitSearchApiTaskletStep", jobRepository)
                .tasklet(organisationUnitSearchApiTasklet, transactionManager)
                .build();
    }

    @Bean(name = "organisationUnitEnrichmentJob")

    public Job enrichmentJob(JobRepository jobRepository, Step organisationUnitEnrichmentStep, Step organisationUnitSearchApiTaskletStep) {
        return new JobBuilder(COFACE_OPS_BATCH_JOB_NAME, jobRepository)
                .incrementer(new RunIdIncrementer())


                .start(organisationUnitEnrichmentStep)
                .next(organisationUnitSearchApiTaskletStep)
                .build();
    }

    // Legal Entity batch config start ----------------------------------------------------------------------------------------
    @Bean
    public Step organisationSearchApiTaskletStep(JobRepository jobRepository,
                                                 PlatformTransactionManager transactionManager,
                                                 OrganisationSearchApiTasklet organisationSearchApiTasklet) {
        return new StepBuilder("organisationSearchApiTaskletStep", jobRepository)
                .tasklet(organisationSearchApiTasklet, transactionManager)
                .build();
    }

    @Bean
    public Step legalEntityParentEnrichStep(JobRepository jobRepository,
                                            PlatformTransactionManager transactionManager,
                                            FlatFileItemReader<LegalEntityParentDomain> legalEntityParentReader,
                                            LEParentEnrichmentProcessor leParentEnrichmentProcessor,
                                            JdbcBatchItemWriter<LegalEntityParentDomain> legalEntityParentWriter) {
        // Get file context for error logging
        String fileId = null;
        String batchId = null;
        try {
            fileId = StepSynchronizationManager.getContext().getStepExecution()
                    .getJobParameters().getString("leParentFileId");
            batchId = String.valueOf(StepSynchronizationManager.getContext().getStepExecution()
                    .getJobExecution().getId());
        } catch (Exception e) {
            log.warn("Could not get file context for skip listener: {}", e.getMessage());
        }

        CsvParsingSkipListener<LegalEntityParentDomain, LegalEntityParentDomain> skipListener =
                new CsvParsingSkipListener<>(errorLogDAO, RecordType.ORGANISATION_PARENT,
                        cofaceLEParentFileName, batchId, fileId);

        return new StepBuilder(COFACE_LE_BATCH_PARENT_STEP_NAME, jobRepository)
                .<LegalEntityParentDomain, LegalEntityParentDomain>chunk(100, transactionManager)
                .reader(legalEntityParentReader)
                .processor(leParentEnrichmentProcessor)
                .writer(legalEntityParentWriter)
                .listener(leParentEnrichmentProcessor)
                .listener(leParentWriterSkipListener())
                .listener(new ChunkListener() {
                    @Override
                    public void afterChunk(ChunkContext context) {
                        leParentEnrichmentProcessor.flushNewMappings();
                    }
                })
                .faultTolerant()
                .skip(FlatFileParseException.class)
                .skip(DataIntegrityViolationException.class)
                .skip(BatchUpdateException.class)
                .skip(UncategorizedSQLException.class)
                .skipLimit(1000)
                .listener(skipListener)
                .build();
    }

    @Bean
    public LegalEntityChildEnrichmentProcessor legalEntityChildEnrichmentProcessor(MappingDAO mappingDAO) {
        return new LegalEntityChildEnrichmentProcessor(mappingDAO, errorLogDAO);
    }

    @Bean
    public Step legalEntityChildEnrichStep(JobRepository jobRepository,
                                           PlatformTransactionManager transactionManager,
                                           FlatFileItemReader<LegalEntityChildDomain> legalEntityChildReader,
                                           LegalEntityChildEnrichmentProcessor legalEntityChildEnrichmentProcessor,
                                           JdbcBatchItemWriter<LegalEntityChildDomain> legalEntityChildWriter) {
        // Get file context for error logging
        String fileId = null;
        String batchId = null;
        try {
            fileId = StepSynchronizationManager.getContext().getStepExecution()
                    .getJobParameters().getString("leChildFileId");
            batchId = String.valueOf(StepSynchronizationManager.getContext().getStepExecution()
                    .getJobExecution().getId());
        } catch (Exception e) {
            log.warn("Could not get file context for skip listener: {}", e.getMessage());
        }

        CsvParsingSkipListener<LegalEntityChildDomain, LegalEntityChildDomain> skipListener =
                new CsvParsingSkipListener<>(errorLogDAO, RecordType.ORGANISATION_CHILD,
                        cofaceLEChildFileName, batchId, fileId);

        return new StepBuilder("legalEntityChildEnrichStep", jobRepository)
                .<LegalEntityChildDomain, LegalEntityChildDomain>chunk(100, transactionManager)
                .reader(legalEntityChildReader)
                .processor(legalEntityChildEnrichmentProcessor)
                .writer(legalEntityChildWriter)
                .listener(legalEntityChildEnrichmentProcessor)
                .faultTolerant()
                .skip(FlatFileParseException.class)
                .skipLimit(100)
                .listener(skipListener)
                .build();
    }


    @Bean
    public LEParentEnrichmentProcessor leParentEnrichmentProcessor() {
        return new LEParentEnrichmentProcessor(mappingDAO, errorLogDAO);
    }

    @StepScope
    @Bean
    public FlatFileItemReader<LegalEntityParentDomain> legalEntityParentReader() {
        String fileId = StepSynchronizationManager.getContext().getStepExecution()
                .getJobParameters().getString("leParentFileId");
        return new FlatFileItemReaderBuilder<LegalEntityParentDomain>()
                .name(COFACE_LE_BATCH_PARENT_FILE_READER_NAME)
                .resource(getFileForLocalRun(readFileFrom, cofaceLEParentFileName,fileId))
                .delimited()
                .names(LegalEntityParent.LE_EXTERNAL_IDENTIFIER, ORG_STATUS, ORG_NAME, ORG_OTHER_NAME,
                        ORG_OTHER_NAME_TYPE, ADR_UNSTRUCTURED_ADDRESS, LE_POSTAL_ADDRESS_STREET_NAME,
                        LE_POSTAL_ADDRESS_HOUSE_NUM, LE_POSTAL_ADDRESS_HOUSE_NUM_ADD,
                        LE_POSTAL_ADDRESS_POSTAL_CODE, LE_POSTAL_ADDRESS_CITY_NAME,
                        LE_POSTAL_ADDRESS_CNTRY_CD, ORG_LEGAL_FORM, ORG_BUSINESS_CLOSEDOWN_DATE,
                        LE_LEGAL_STATUS, ORG_DATE_OF_FOUNDATION, LE_PREFERRED_LANGUAGE,
                        LE_DIGITAL_ADDR_FULL_TEL, NSSO_EXTERNAL_IDENTIFIER, ASMT_VAT_STATUS,
                        NSSO_EXTERNAL_IDENTIFIER_STATUS)
                .fieldSetMapper(new LegalEntityParentFieldSetMapper())
                .linesToSkip(1)
                .build();
    }

    @Bean
    public JdbcBatchItemWriter<LegalEntityParentDomain> legalEntityParentWriter(DataSource dataSource) {

        return new JdbcBatchItemWriterBuilder<LegalEntityParentDomain>()
                .sql(LEGAL_ENTITY_PARENT_TABLE_INSERT_SQL)
                .beanMapped()
                .dataSource(dataSource)
                .build();
    }

    @StepScope
    @Bean
    public FlatFileItemReader<LegalEntityChildDomain> legalEntityChildReader() {
        String fileId = StepSynchronizationManager.getContext().getStepExecution()
                .getJobParameters().getString("leChildFileId");
        return new FlatFileItemReaderBuilder<LegalEntityChildDomain>()
                .name(COFACE_LE_BATCH_CHILD_FILE_READER_NAME)
                .resource(getFileForLocalRun(readFileFrom, cofaceLEChildFileName,fileId))
                .delimited()
                .names(LegalEntityParent.LE_EXTERNAL_IDENTIFIER, INDUSTRY_CLASS_CODE, INDUSTRY_CLASS_RANK,
                        INDUSTRY_CLASS_EFF_DATE, INDUSTRY_CLASS_END_DATE)
                .fieldSetMapper(new LegalEntityChildFieldSetMapper())
                .linesToSkip(1)
                .build();
    }

    @Bean
    public JdbcBatchItemWriter<LegalEntityChildDomain> legalEntityChildWriter(DataSource dataSource) {
        return new JdbcBatchItemWriterBuilder<LegalEntityChildDomain>()
                .sql(LEGAL_ENTITY_CHILD_TABLE_INSERT_SQL)
                .beanMapped()
                .dataSource(dataSource)
                .build();
    }

    @Bean(name = "LegalEntityEnrichmentJob")
    public Job lEEnrichmentJob(JobRepository jobRepository, Step legalEntityParentEnrichStep, Step legalEntityChildEnrichStep, Step organisationSearchApiTaskletStep) {

        return new JobBuilder(COFACE_LE_BATCH_JOB_NAME, jobRepository)
                .incrementer(new RunIdIncrementer())
                .start(legalEntityParentEnrichStep)
                .next(legalEntityChildEnrichStep)
                .next(organisationSearchApiTaskletStep)
                .build();
    }
    // Legal Entity batch config End ----------------------------------------------------------------------------------------


    @Bean
    @StepScope
    public FlatFileItemReader<IncapableRelationship> incapablesReader() {

        String fileId = StepSynchronizationManager.getContext()
                .getStepExecution()
                .getJobParameters()
                .getString("incapablesFileId");

        return new FlatFileItemReaderBuilder<IncapableRelationship>()
                .name(INCAPABLES_BATCH_FILE_READER_NAME)
                .resource(getFileForLocalRun(readFileFrom, cofaceIncapablesFileName, fileId))
                .delimited()
                .names(INCP_GENDER, INCP_LASTNAME, INCP_FIRSTNAME, INCP_STREETNAME,
                        INCP_HOUSENUMBER, INCP_HOUSENUMBERADDITION, INCP_POSTALCODE,
                        INCP_CITYNAME, INCP_COUNTRYOFRESIDENCE, INCP_DATEOFBIRTH,
                        INCP_DATEOFDEATH, INCP_CITYOFBIRTH, INCP_COUNTRYOFBIRTH,
                        OBJECT_CODE, INAB_ENDDATE, INAB_EFFECTIVEDATE,
                        ADM_OCCUPATIONCODE, ADM_LASTNAME, ADM_FIRSTNAME,
                        ADM_STREETNAME, ADM_HOUSENUMBER, ADM_HOUSENUMBERADDITION,
                        ADM_POSTALCODE, ADM_CITYNAME, ADM_COUNTRYOFRESIDENCE,
                        ADM_RESPONSIBILITY_ENDDATE)
                .fieldSetMapper(new IncapablesFieldSetMapper())
                .linesToSkip(1)
                .build();
    }

    @Bean
    public IncapablesEnrichmentProcessor incapablesEnrichmentProcessor() {
        return new IncapablesEnrichmentProcessor(mappingDAO);
    }

    @Bean
    public JdbcBatchItemWriter<IncapableRelationship> incapablesWriter(DataSource dataSource) {
        return new JdbcBatchItemWriterBuilder<IncapableRelationship>()
                .sql(IncapablesDAO.INCAPABLES_TABLE_INSERT_SQL)
                .beanMapped()
                .dataSource(dataSource)
                .build();
    }

    @Bean
    public Step incapablesEnrichmentStep(JobRepository jobRepository,
                                         PlatformTransactionManager transactionManager,
                                         FlatFileItemReader<IncapableRelationship> incapablesReader,
                                         IncapablesEnrichmentProcessor incapablesProcessor,
                                         JdbcBatchItemWriter<IncapableRelationship> incapablesWriter) {
        // Get file context for error logging
        String fileId = null;
        String batchId = null;
        try {
            fileId = StepSynchronizationManager.getContext().getStepExecution()
                    .getJobParameters().getString("incapablesFileId");
            batchId = String.valueOf(StepSynchronizationManager.getContext().getStepExecution()
                    .getJobExecution().getId());
        } catch (Exception e) {
            log.warn("Could not get file context for skip listener: {}", e.getMessage());
        }

        CsvParsingSkipListener<IncapableRelationship, IncapableRelationship> skipListener =
                new CsvParsingSkipListener<>(errorLogDAO, RecordType.INCAPABLE,
                        cofaceIncapablesFileName, batchId, fileId);

        return new StepBuilder(INCAPABLES_BATCH_STEP_NAME, jobRepository)
                .<IncapableRelationship, IncapableRelationship>chunk(100, transactionManager)
                .reader(incapablesReader)
                .processor(incapablesProcessor)
                .writer(incapablesWriter)
                .listener(incapablesProcessor)
                .listener(new ChunkListener() {
                    @Override
                    public void afterChunk(ChunkContext context) {
                        incapablesProcessor.flushNewMappings();
                    }
                })
                .faultTolerant()
                .skip(FlatFileParseException.class)
                .skipLimit(100)
                .listener(skipListener)
                .build();
    }

    @Bean
    public Step incapablesApiTaskletStep(JobRepository jobRepository,
                                         PlatformTransactionManager transactionManager,
                                         IncapablesApiTasklet incapablesApiTasklet) {
        return new StepBuilder("incapablesApiTaskletStep", jobRepository)
                .tasklet(incapablesApiTasklet, transactionManager)
                .build();
    }

    @Bean(name = "IncapablesEnrichmentJob")
    public Job incapablesEnrichmentJob(JobRepository jobRepository,
                                       Step incapablesEnrichmentStep,
                                       Step incapablesApiTaskletStep) {
        log.info("IncapablesEnrichmentJob job started");
        return new JobBuilder(INCAPABLES_BATCH_JOB_NAME, jobRepository)
                .incrementer(new RunIdIncrementer())
                .start(incapablesEnrichmentStep)
                .next(incapablesApiTaskletStep)
                .build();
    }

    // Legal Entity Deletion batch config start ----------------------------------------------------------------------------------------

    @Bean
    @StepScope
    public FlatFileItemReader<LegalEntityDeletionDomain> legalEntityDeletionReader() {
        String fileId = StepSynchronizationManager.getContext().getStepExecution()
                .getJobParameters().getString("leDeletionFileId");
        return new FlatFileItemReaderBuilder<LegalEntityDeletionDomain>()
                .name(COFACE_LE_DELETION_BATCH_FILE_READER_NAME)
                .resource(getFileForLocalRun(readFileFrom, cofaceLEDeleteFileName, fileId))
                .delimited()
                .names(LegalEntityDeletionFieldSetMapper.LE_EXTERNAL_IDENTIFIER,
                        LegalEntityDeletionFieldSetMapper.LE_DELETION_FLAG)
                .fieldSetMapper(new LegalEntityDeletionFieldSetMapper())
                .linesToSkip(1)
                .build();
    }

    @Bean
    public LEDeletionEnrichmentProcessor leDeletionEnrichmentProcessor() {
        return new LEDeletionEnrichmentProcessor(mappingDAO, legalEntityDeletionDAO, errorLogDAO);
    }

    @Bean
    public JdbcBatchItemWriter<LegalEntityDeletionDomain> legalEntityDeletionWriter(DataSource dataSource) {
        String sql = "INSERT INTO DD_LEGALENTITY_DELETE_TBL (LE_EXTERNAL_IDENTIFIER, LE_DELETION_FLAG, DD_UUID, FILE_ID, CREATED_BY, CREATED_TS) " +
                "VALUES (:leExternalIdentifier, :leDeletionFlag, :ddUuid, :fileId, 'DD_USER', SYSTIMESTAMP)";
        return new JdbcBatchItemWriterBuilder<LegalEntityDeletionDomain>()
                .sql(sql)
                .beanMapped()
                .dataSource(dataSource)
                .build();
    }

    @Bean
    public Step legalEntityDeletionEnrichStep(JobRepository jobRepository,
                                              PlatformTransactionManager transactionManager,
                                              FlatFileItemReader<LegalEntityDeletionDomain> legalEntityDeletionReader,
                                              LEDeletionEnrichmentProcessor leDeletionEnrichmentProcessor,
                                              JdbcBatchItemWriter<LegalEntityDeletionDomain> legalEntityDeletionWriter) {
        // Get file context for error logging
        String fileId = null;
        String batchId = null;
        try {
            fileId = StepSynchronizationManager.getContext().getStepExecution()
                    .getJobParameters().getString("leDeletionFileId");
            batchId = String.valueOf(StepSynchronizationManager.getContext().getStepExecution()
                    .getJobExecution().getId());
        } catch (Exception e) {
            log.warn("Could not get file context for skip listener: {}", e.getMessage());
        }

        CsvParsingSkipListener<LegalEntityDeletionDomain, LegalEntityDeletionDomain> skipListener =
                new CsvParsingSkipListener<>(errorLogDAO, RecordType.LEGAL_ENTITY_DELETION,
                        cofaceLEDeleteFileName, batchId, fileId);

        return new StepBuilder(COFACE_LE_DELETION_BATCH_STEP_NAME, jobRepository)
                .<LegalEntityDeletionDomain, LegalEntityDeletionDomain>chunk(100, transactionManager)
                .reader(legalEntityDeletionReader)
                .processor(leDeletionEnrichmentProcessor)
                .writer(legalEntityDeletionWriter)
                .listener((StepExecutionListener) leDeletionEnrichmentProcessor)
                .listener(new ChunkListener() {
                    @Override
                    public void afterChunk(ChunkContext context) {
                        leDeletionEnrichmentProcessor.flushRecords();
                    }
                })
                .faultTolerant()
                .skip(FlatFileParseException.class)
                .skipLimit(100)
                .listener(skipListener)
                .build();
    }

    @Bean
    public Step leDeletionApiTaskletStep(JobRepository jobRepository,
                                         PlatformTransactionManager transactionManager,
                                         LEDeletionApiTasklet leDeletionApiTasklet) {
        return new StepBuilder(LE_DELETION_API_TASKLET_STEP, jobRepository)
                .tasklet(leDeletionApiTasklet, transactionManager)
                .build();
    }

    @Bean(name = "LegalEntityDeletionJob")
    public Job legalEntityDeletionJob(JobRepository jobRepository,
                                      Step legalEntityDeletionEnrichStep,
                                      Step leDeletionApiTaskletStep) {
        log.info("LegalEntityDeletionJob job started");
        return new JobBuilder(COFACE_LE_DELETION_BATCH_JOB_NAME, jobRepository)
                .incrementer(new RunIdIncrementer())
                .start(legalEntityDeletionEnrichStep)
                .next(leDeletionApiTaskletStep)
                .build();
    }
    // Legal Entity Deletion batch config End ----------------------------------------------------------------------------------------


    // Read File from ECS/Local-folder --------------------------------------------------------------------------------------
    private Resource getFileForLocalRun(String fileFrom, String fileName, String fileId) {
        Resource resource = null;
        log.info("DD_Data_Distributor Read File from {}, filename:{}", fileFrom, fileName);
        if (fileFrom.equalsIgnoreCase("ECS")) {
            resource = fileProviderService.getFile(bucketName, fileName);
        } else if (fileName.equalsIgnoreCase(cofaceLEChildFileName)) {
            resource = resourceLEChildFile;
        } else if (fileName.equalsIgnoreCase(cofaceLEParentFileName)) {
            resource = resourceLEParentFile;
        } else if (fileName.equalsIgnoreCase(cofaceOUFileName)) {
            resource = resourceOUFile;
        } else if (fileName.equalsIgnoreCase(cofaceIncapablesFileName)) {
            resource = resourceIncapablesFile;
        } else if (fileName.equalsIgnoreCase(cofaceLEDeleteFileName)) {
            resource = resourceLEDeleteFile;
        } else {
            log.error("DD_Data_Distributor Unknown File Name {}", fileName);
            return null;
        }
        log.info("DD_Data_Distributor File Downloaded Successfully...!");
        fileIngestionService.updateTotalNumberOfRecords(fileId, resource);
        return resource;
    }

    public void logDataRetentionSchedulerStatus(DataRetentionConfig dataRetentionConfig) {
        boolean isRetentionJobEnabled = dataRetentionConfig.isEnabled();
        dataRetentionConfig.logRetentionJobStatus(isRetentionJobEnabled);
    }

    @Bean
    public SkipListener<LegalEntityParentDomain, LegalEntityParentDomain> leParentWriterSkipListener() {
        return new SkipListener<>() {

            @Override
            public void onSkipInWrite(LegalEntityParentDomain item, Throwable t) {
                errorLogDAO.logValidationError(
                        RecordType.ORGANISATION_PARENT,
                        item.getLeExternalIdentifier(),
                        "DB write failed: " + t.getMessage(),
                        null,
                        null,
                        item.getFileId()
                );
            }
        };
    }
}

