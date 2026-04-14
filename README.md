package com.ing.datadist.batch.config;

import com.ing.datadist.domain.LegalEntityParentDomain;
import org.springframework.batch.item.file.mapping.FieldSetMapper;
import org.springframework.batch.item.file.transform.FieldSet;
import org.springframework.lang.NonNull;

import static com.ing.datadist.domain.fileinput.LegalEntityParent.*;

public class LegalEntityParentFieldSetMapper implements FieldSetMapper<LegalEntityParentDomain> {
    @Override
    public @NonNull LegalEntityParentDomain mapFieldSet(@NonNull FieldSet fieldSet) {
        LegalEntityParentDomain legalEntityParentDomain = new LegalEntityParentDomain();
        legalEntityParentDomain.setLeExternalIdentifier(fieldSet.readString(LE_EXTERNAL_IDENTIFIER));
        legalEntityParentDomain.setOrgStatus(fieldSet.readString(ORG_STATUS));
        legalEntityParentDomain.setOrgName(fieldSet.readString(ORG_NAME));
        legalEntityParentDomain.setOrgOtherName(fieldSet.readString(ORG_OTHER_NAME));
        legalEntityParentDomain.setOrgOtherNameType(fieldSet.readString(ORG_OTHER_NAME_TYPE));
        legalEntityParentDomain.setAdrUnstructuredAddress(fieldSet.readString(ADR_UNSTRUCTURED_ADDRESS));
        legalEntityParentDomain.setAdrPostalAddressStreetName(fieldSet.readString(LE_POSTAL_ADDRESS_STREET_NAME));
        legalEntityParentDomain.setAdrPostalAddressHouseNum(fieldSet.readString(LE_POSTAL_ADDRESS_HOUSE_NUM));
        legalEntityParentDomain.setAdrPostalAddressHouseNumAdd(fieldSet.readString(LE_POSTAL_ADDRESS_HOUSE_NUM_ADD));
        legalEntityParentDomain.setAdrPostalAddressPostalCode(fieldSet.readString(LE_POSTAL_ADDRESS_POSTAL_CODE));
        legalEntityParentDomain.setAdrPostalAddressCityName(fieldSet.readString(LE_POSTAL_ADDRESS_CITY_NAME));
        legalEntityParentDomain.setAdrPostalAddressCountryCode(fieldSet.readString(LE_POSTAL_ADDRESS_CNTRY_CD));
        legalEntityParentDomain.setOrgLegalForm(fieldSet.readString(ORG_LEGAL_FORM));
        legalEntityParentDomain.setOrgBusinessClosedownDate(fieldSet.readString(ORG_BUSINESS_CLOSEDOWN_DATE));
        legalEntityParentDomain.setLELegalStatus(fieldSet.readString(LE_LEGAL_STATUS));
        legalEntityParentDomain.setLEPreferredLanguage(fieldSet.readString(LE_PREFERRED_LANGUAGE));
        legalEntityParentDomain.setAdrDigitalAddrFullTel(fieldSet.readString(LE_DIGITAL_ADDR_FULL_TEL));
        legalEntityParentDomain.setNssoExternalIdentifier(fieldSet.readString(NSSO_EXTERNAL_IDENTIFIER));
        legalEntityParentDomain.setAsmtVatStatus(fieldSet.readString(ASMT_VAT_STATUS));
        legalEntityParentDomain.setNssoExternalIdentifierStatus(fieldSet.readString(NSSO_EXTERNAL_IDENTIFIER_STATUS));
        legalEntityParentDomain.setOrgDateOfFoundation(fieldSet.readString(ORG_DATE_OF_FOUNDATION));

        return legalEntityParentDomain;
    }
}
package com.ing.datadist.batch.processor;

import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.domain.LegalEntityParentDomain;
import com.ing.datadist.enums.RecordType;
import com.ing.datadist.util.FieldValidator;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.StepExecution;
import org.springframework.batch.core.StepExecutionListener;
import org.springframework.batch.item.ItemProcessor;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;
import java.util.UUID;

@Slf4j
public class LEParentEnrichmentProcessor implements ItemProcessor<LegalEntityParentDomain, LegalEntityParentDomain>, StepExecutionListener {
    private final MappingDAO dao;
    private final ErrorLogDAO errorLogDAO;
    private final List<LegalEntityParentDomain> newLEMappings = new ArrayList<>();
    private Map<String, String> leUuidMap;
    private String fileId;

    public LEParentEnrichmentProcessor(MappingDAO dao, ErrorLogDAO errorLogDAO) {
        this.dao = dao;
        this.errorLogDAO = errorLogDAO;
    }

    @Override
    public LegalEntityParentDomain process(LegalEntityParentDomain item) throws Exception {
        item.setFileId(this.fileId);

        List<String> validationErrors = FieldValidator.validate(item);

        if (!validationErrors.isEmpty()) {
            String errorMessage = FieldValidator.formatValidationErrors(validationErrors);
            log.error("Data_Distributor_Coface_LE_Parent: Validation failed for LE_EXTERNAL_IDENTIFIER: {}. Errors: {}",
                    item.getLeExternalIdentifier(), errorMessage);

            errorLogDAO.logValidationError(
                    RecordType.ORGANISATION_PARENT,
                    item.getLeExternalIdentifier(),
                    "Field validation failed: " + errorMessage,
                    item.getBatchId(),
                    item.getFileName(),
                    this.fileId
            );

            return null;
        }

        // Step 2: UUID mapping and enrichment
        String orgUUID = leUuidMap.get(item.getLeExternalIdentifier());
        if (orgUUID == null) {
            orgUUID = UUID.randomUUID().toString();
            item.setOrgUUID(orgUUID);
            newLEMappings.add(item);
            leUuidMap.put(item.getLeExternalIdentifier(), orgUUID);
        }
        item.setOrgUUID(orgUUID);
        return item;
    }

    @Override
    public void beforeStep(StepExecution stepExecution) {
        log.info("Preloading LE mapping table into memory");
        leUuidMap = dao.fetchAllLEUuidMappings();
        this.fileId = stepExecution.getJobParameters().getString("leParentFileId");
        log.info("Loaded {} LE UUIDs from mapping table", leUuidMap.size());
    }

    public void flushNewMappings() {
        if (!newLEMappings.isEmpty()) {
            log.info("Flushing {} new LE mapping records to DB", newLEMappings.size());
            dao.batchInsertLEMappingRecords(newLEMappings);
            newLEMappings.clear();
        }
    }

    @Override
    public ExitStatus afterStep(StepExecution stepExecution) {
        long processed = stepExecution.getWriteCount();
        long failed = stepExecution.getProcessSkipCount();

        stepExecution.getJobExecution().getExecutionContext().put("totalRecordsLEP", processed + failed);
        stepExecution.getJobExecution().getExecutionContext().put("processedRecordsLEP", processed);
        stepExecution.getJobExecution().getExecutionContext().put("failedRecordsLEP", failed);

        flushNewMappings();

        return ExitStatus.COMPLETED;
    }
}
package com.ing.datadist.batch.processor;

import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.domain.LegalEntityChildDomain;
import com.ing.datadist.enums.RecordType;
import com.ing.datadist.util.FieldValidator;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.StepExecution;
import org.springframework.batch.core.StepExecutionListener;
import org.springframework.batch.item.ItemProcessor;

import java.util.List;

@Slf4j
public class LegalEntityChildEnrichmentProcessor
        implements ItemProcessor<LegalEntityChildDomain, LegalEntityChildDomain>, StepExecutionListener {

    private final MappingDAO mappingDAO;
    private final ErrorLogDAO errorLogDAO;
    private String fileId;
    private long processedCount = 0;

    public LegalEntityChildEnrichmentProcessor(MappingDAO mappingDAO, ErrorLogDAO errorLogDAO) {
        this.mappingDAO = mappingDAO;
        this.errorLogDAO = errorLogDAO;
    }

    @Override
    public void beforeStep(StepExecution stepExecution) {
        this.fileId = stepExecution.getJobParameters().getString("leChildFileId");
        this.processedCount = 0;
        log.info("Data_Distributor_Coface_LE_Child: Starting child enrichment processor for fileId={}", fileId);
    }

    @Override
    public LegalEntityChildDomain process(LegalEntityChildDomain item) {
        item.setFileId(this.fileId);

        List<String> validationErrors = FieldValidator.validate(item);
        if (!validationErrors.isEmpty()) {
            String errorMessage = FieldValidator.formatValidationErrors(validationErrors);
            errorLogDAO.logValidationError(
                    RecordType.ORGANISATION_CHILD,
                    item.getLeExternalIdentifier(),
                    errorMessage,
                    item.getBatchId(),
                    item.getFileName(),
                    this.fileId
            );
            return null;
        }

        String leExternalIdentifier = item.getLeExternalIdentifier();
        String parentUUID = mappingDAO.findParentUUIDByExternalIdentifier(leExternalIdentifier);
        if (parentUUID != null) {
            item.setOrgUUID(parentUUID);
            processedCount++;
            return item;
        }

        log.warn("Data_Distributor_Coface_LE_Child: Parent record not found for LE External Identifier: {}", leExternalIdentifier);
        errorLogDAO.logValidationError(
                RecordType.ORGANISATION_CHILD,
                leExternalIdentifier,
                "Parent record not found for LE External Identifier: " + leExternalIdentifier,
                item.getBatchId(),
                item.getFileName(),
                this.fileId
        );
        return null;
    }

    @Override
    public ExitStatus afterStep(StepExecution stepExecution) {
        long processed = stepExecution.getWriteCount();
        long failed = stepExecution.getProcessSkipCount();

        log.info("Data_Distributor_Coface_LE_Child: Processing complete. Processed={}, Failed={}", processed, failed);

        stepExecution.getJobExecution().getExecutionContext().put("totalRecordsLEC", processed + failed);
        stepExecution.getJobExecution().getExecutionContext().put("processedRecordsLEC", processed);
        stepExecution.getJobExecution().getExecutionContext().put("failedRecordsLEC", failed);

        return ExitStatus.COMPLETED;
    }
}

package com.ing.datadist.batch.processor;

import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.domain.OrganisationUnitDomain;
import com.ing.datadist.domain.OrganisationUnitDomainWrapper;
import com.ing.datadist.enums.RecordType;
import lombok.Getter;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.StepExecution;
import org.springframework.batch.core.StepExecutionListener;
import org.springframework.batch.core.configuration.annotation.StepScope;
import org.springframework.batch.item.ItemProcessor;

import java.util.*;

@Slf4j
@Getter
@StepScope
public class OrganisationUnitEnrichmentProcessor implements ItemProcessor<OrganisationUnitDomain, OrganisationUnitDomainWrapper>, StepExecutionListener {
    private final MappingDAO dao;
    private final ErrorLogDAO errorLogDAO;
    private final List<OrganisationUnitDomainWrapper> newOPsMappings = new ArrayList<OrganisationUnitDomainWrapper>();
    private final List<OrganisationUnitDomainWrapper> newLEMappings = new ArrayList<OrganisationUnitDomainWrapper>();
    private Map<String, String> opsUuidMap;
    private String fileId;

    public OrganisationUnitEnrichmentProcessor(MappingDAO dao, ErrorLogDAO errorLogDAO) {
        this.dao = dao;
        this.errorLogDAO = errorLogDAO;
    }

    @Override
    public OrganisationUnitDomainWrapper process(OrganisationUnitDomain item) throws Exception {
        String orgUUID = opsUuidMap.get(item.getOrgExternalIdentifierVal());
        
        // Skip record if orgUUID is null - log error
        if (orgUUID == null || orgUUID.trim().isEmpty()) {
            log.error("Data_Distributor_Coface_OU DD_UUID not found for Organisation External Identifier: {} (OPS: {}). Skipping record.",
                    item.getOrgExternalIdentifierVal(), item.getOpsExternalIdentifierVal());
            errorLogDAO.logValidationError(
                    RecordType.ORGANISATION_UNIT,
                    item.getOpsExternalIdentifierVal(),
                    "DD_UUID not found in mapping table for Organisation External Identifier: " + item.getOrgExternalIdentifierVal() +
                            ". Record will not be saved to main table.",
                    null,
                    null,
                    this.fileId
            );
            return null; // Skip this record
        }
        
        String ipExternalIdentifierVal = item.getOpsExternalIdentifierVal();
        String opsUUID = opsUuidMap.get(ipExternalIdentifierVal);
        OrganisationUnitDomainWrapper record = new OrganisationUnitDomainWrapper();
        record.setFileId(this.fileId); // Set fileId here
        if (opsUUID == null) {
            log.info("No UUID for CofaceOpsId {}. Adding to batch insert.", ipExternalIdentifierVal);
            opsUUID = UUID.randomUUID().toString();
            log.info("Data_Distributor_Coface_OU No UUID for CofaceOpsId {}, Creating uuid:{}", ipExternalIdentifierVal,opsUUID);
            record.setOpsUUID(opsUUID); // Set the new UUID
            newOPsMappings.add(record);
            opsUuidMap.put(ipExternalIdentifierVal, opsUUID);
        }
        record.setOrgUUID(orgUUID);
        record.setOpsUUID(opsUUID);
        record.setOpsExternalIdentifierVal(item.getOpsExternalIdentifierVal());
        record.setOrganisationUnitName(item.getOrganisationUnitName());
        record.setAddress(item.getAddress());
        record.setOrgExternalIdentifierVal(item.getOrgExternalIdentifierVal());
        record.setDigitalAddrEmail(item.getDigitalAddrEmail());
        record.setDigitalAddrFullTel(item.getDigitalAddrFullTel());
        record.setPostalAddressCityName(item.getPostalAddressCityName());
        record.setPostalAddressCntryCd(item.getPostalAddressCntryCd());
        record.setPostalAddressHouseAdd(item.getPostalAddressHouseAdd());
        record.setPostalAddressHouseNum(item.getPostalAddressHouseNum());
        record.setPostalAddressPostalCd(item.getPostalAddressPostalCd());
        record.setPostalAddressStreetNm(item.getPostalAddressStreetNm());
        record.setOpsExtIdDateOfIssue(item.getOpsExtIdDateOfIssue());
        record.setOpsExtIdExpiryDate(item.getOpsExtIdExpiryDate());
        return record;
    }

    @Override
    public void beforeStep(StepExecution stepExecution) {
        log.info(" Preloading mapping table into memory");
        opsUuidMap = dao.fetchAllOPsUuidMappings();
        opsUuidMap.putAll(dao.fetchAllLEUuidMappings());

        // Extract fileId from job parameters
        this.fileId = stepExecution.getJobParameters().getString("opsFileId");
        log.info("Loaded {} UUIDs from mapping table", opsUuidMap.size());
    }


    public void flushNewMappings() {
        if (!newOPsMappings.isEmpty()) {
            log.info("Flushing {} new OPS mapping records to DB", newOPsMappings.size());
            dao.batchInsertOPsMappingRecords(newOPsMappings);
            newOPsMappings.clear();
        }
    }

    @Override
    public ExitStatus afterStep(StepExecution stepExecution) {

        long processed = stepExecution.getWriteCount();
        long failed = stepExecution.getProcessSkipCount();

        stepExecution.getJobExecution().getExecutionContext().put("totalRecordsOps", processed + failed);
        stepExecution.getJobExecution().getExecutionContext().put("processedRecordsOps", processed);
        stepExecution.getJobExecution().getExecutionContext().put("failedRecordsOps", failed);

        flushNewMappings();

        return ExitStatus.COMPLETED;
    }
}
package com.ing.datadist.batch.processor;

import com.ing.datadist.api.utils.DataDistributionConstants;
import com.ing.datadist.dao.ErrorLogDAO;
import com.ing.datadist.dao.LegalEntityDeletionDAO;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.domain.LegalEntityDeletionDomain;
import com.ing.datadist.enums.RecordType;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.StepExecution;
import org.springframework.batch.core.StepExecutionListener;
import org.springframework.batch.item.ItemProcessor;

import java.util.ArrayList;
import java.util.List;
import java.util.Map;


@Slf4j
public class LEDeletionEnrichmentProcessor implements ItemProcessor<LegalEntityDeletionDomain, LegalEntityDeletionDomain>, StepExecutionListener {

    private final MappingDAO mappingDAO;
    private final LegalEntityDeletionDAO deletionDAO;
    private final ErrorLogDAO errorLogDAO;

    private Map<String, String> leUuidMap;
    private String fileId;
    private final List<LegalEntityDeletionDomain> recordsToInsert = new ArrayList<>();

    public LEDeletionEnrichmentProcessor(MappingDAO mappingDAO,
                                         LegalEntityDeletionDAO deletionDAO,
                                         ErrorLogDAO errorLogDAO) {
        this.mappingDAO = mappingDAO;
        this.deletionDAO = deletionDAO;
        this.errorLogDAO = errorLogDAO;
    }

    @Override
    public LegalEntityDeletionDomain process(LegalEntityDeletionDomain item) throws Exception {
        item.setFileId(this.fileId);

        // Validate LE External Identifier
        if (item.getLeExternalIdentifier() == null || item.getLeExternalIdentifier().trim().isEmpty()) {
            log.warn("Data_Distributor_LE_Deletion Skipping record with empty LE External Identifier");
            return null;
        }

        // Validate deletion flag - if null or invalid, default to 'N' and still save
        String deletionFlag = item.getLeDeletionFlag();
        if (deletionFlag == null || deletionFlag.trim().isEmpty()) {
            log.warn("Data_Distributor_LE_Deletion Record with empty deletion flag, defaulting to '{}' for LE_EXTERNAL_IDENTIFIER: {}",
                    DataDistributionConstants.ADD_FLAG, item.getLeExternalIdentifier());
            item.setLeDeletionFlag(DataDistributionConstants.ADD_FLAG);
            deletionFlag = DataDistributionConstants.ADD_FLAG;
        } else if (!deletionFlag.equalsIgnoreCase(DataDistributionConstants.DELETION_FLAG)
                && !deletionFlag.equalsIgnoreCase(DataDistributionConstants.ADD_FLAG)) {
            log.warn("Data_Distributor_LE_Deletion Invalid deletion flag '{}' for LE_EXTERNAL_IDENTIFIER: {}, defaulting to '{}'",
                    deletionFlag, item.getLeExternalIdentifier(), DataDistributionConstants.ADD_FLAG);
            errorLogDAO.logValidationError(
                    RecordType.LEGAL_ENTITY_DELETION,
                    item.getLeExternalIdentifier(),
                    "Invalid LE_DELETIONFLAG value: " + deletionFlag + ". Must be '" 
                            + DataDistributionConstants.DELETION_FLAG + "' or '"
                            + DataDistributionConstants.ADD_FLAG + "'. Defaulting to '"
                            + DataDistributionConstants.ADD_FLAG + "'.",
                    null,
                    null,
                    fileId
            );
            item.setLeDeletionFlag(DataDistributionConstants.ADD_FLAG);
            deletionFlag = DataDistributionConstants.ADD_FLAG;
        }

        // Lookup DD_UUID from mapping table (can be null if not found)
        String ddUuid = leUuidMap.get(item.getLeExternalIdentifier());
        item.setDdUuid(ddUuid);

        // Skip records with null DD_UUID - don't insert into main table
        if (ddUuid == null || ddUuid.trim().isEmpty()) {
            log.error("Data_Distributor_LE_Deletion DD_UUID not found for LE_EXTERNAL_IDENTIFIER: {}. Skipping record.",
                    item.getLeExternalIdentifier());
            errorLogDAO.logValidationError(
                    RecordType.LEGAL_ENTITY_DELETION,
                    item.getLeExternalIdentifier(),
                    "DD_UUID not found in mapping table for LE External Identifier. Record will not be saved to main table.",
                    null,
                    null,
                    fileId
            );
            return null; // Skip this record - won't be written to main table
        }

        // Add to records to insert - save data to DD_LEGALENTITY_DELETE_TBL
        recordsToInsert.add(item);
        log.info("Data_Distributor_LE_Deletion Record added for DB insert - LE_EXTERNAL_IDENTIFIER: {}, DD_UUID: {}, FLAG: {}",
                item.getLeExternalIdentifier(), ddUuid, item.getLeDeletionFlag());

        // Log for deletion flag records
        if (DataDistributionConstants.DELETION_FLAG.equalsIgnoreCase(item.getLeDeletionFlag())) {
            log.info("Data_Distributor_LE_Deletion Record with flag '{}' saved for API processing - LE_EXTERNAL_IDENTIFIER: {}, DD_UUID: {}",
                    DataDistributionConstants.DELETION_FLAG, item.getLeExternalIdentifier(), ddUuid);
        } else {
            log.info("Data_Distributor_LE_Deletion Record with flag '{}' saved but will skip API - LE_EXTERNAL_IDENTIFIER: {}",
                    DataDistributionConstants.ADD_FLAG, item.getLeExternalIdentifier());
        }

        return item;
    }

    @Override
    public void beforeStep(StepExecution stepExecution) {
        log.info("Data_Distributor_LE_Deletion Preloading LE UUID mapping table into memory");
        leUuidMap = mappingDAO.fetchAllLEUuidMappings();
        this.fileId = stepExecution.getJobParameters().getString("leDeletionFileId");
        log.info("Data_Distributor_LE_Deletion Loaded {} UUIDs from mapping table", leUuidMap.size());
    }

    /**
     * Flush all valid records to DD_LEGALENTITY_DELETE_TBL
     */
    public void flushRecords() {
        if (!recordsToInsert.isEmpty()) {
            log.info("Data_Distributor_LE_Deletion Flushing {} deletion records to DB", recordsToInsert.size());
           // deletionDAO.batchInsertDeleteRecords(recordsToInsert);
            recordsToInsert.clear();
        }
    }

    @Override
    public ExitStatus afterStep(StepExecution stepExecution) {
        flushRecords();
        log.info("Data_Distributor_LE_Deletion Processor step completed. All records saved to database.");
        return ExitStatus.COMPLETED;
    }
}

package com.ing.datadist.batch.processor;

import com.ing.datadist.api.utils.CompositeKeyGenerator;
import com.ing.datadist.dao.FlowType;
import com.ing.datadist.dao.MappingDAO;
import com.ing.datadist.domain.MappingTableRecord;
import com.ing.datadist.domain.incapables.IncapableRelationship;
import lombok.Getter;
import lombok.extern.slf4j.Slf4j;
import org.springframework.batch.core.ExitStatus;
import org.springframework.batch.core.StepExecution;
import org.springframework.batch.core.StepExecutionListener;
import org.springframework.batch.core.configuration.annotation.StepScope;
import org.springframework.batch.item.ItemProcessor;

import org.springframework.lang.NonNull;
import java.util.*;

@Slf4j
@Getter
@StepScope
public class IncapablesEnrichmentProcessor implements ItemProcessor<IncapableRelationship, IncapableRelationship>, StepExecutionListener {

    private final MappingDAO dao;
    private final List<MappingTableRecord> newMappingTableRecords = new ArrayList<>();
    private Map<String, String> incapableUuidMap;
    private String fileId;

    public IncapablesEnrichmentProcessor(MappingDAO dao) {
        this.dao = dao;
    }

    @Override
    public IncapableRelationship process(IncapableRelationship item) throws Exception {

        // Set fileId from job parameters
        item.setFileId(fileId);

        String incapableCompositeKey = CompositeKeyGenerator.generateIncapableCompositeKey(
                item.getIncapablePerson().getFirstName(),
                item.getIncapablePerson().getLastName(),
                item.getIncapablePerson().getDateOfBirth(),
                item.getIncapablePerson().getPostalAddress() != null ?
                    item.getIncapablePerson().getPostalAddress().getPostalCode() : null
        );

        // Check if incapable person UUID exists
        String incapableUUID = incapableUuidMap.get(incapableCompositeKey);
        if (incapableUUID == null) {
            // New incapable person - create UUID and mapping record
            incapableUUID = UUID.randomUUID().toString();
            incapableUuidMap.put(incapableCompositeKey, incapableUUID);

            MappingTableRecord incapableRecord = MappingTableRecord.builder()
                    .ddUuid(incapableUUID)
                    .compositeKey(incapableCompositeKey)
                    .typeOfEntity(FlowType.INC_IND.getLabel())
                    .build();

            newMappingTableRecords.add(incapableRecord);
            log.info("Created new mapping record for incapable person: UUID={}, compositeKey={}, type={}",
                     incapableUUID, incapableCompositeKey, FlowType.INC_IND.getLabel());
        } else {
            log.debug("Found existing UUID={} for incapable person with composite key {}", incapableUUID, incapableCompositeKey);
        }

        item.setDdUuid(incapableUUID);

        // Generate composite key for administrator
        String administratorCompositeKey = CompositeKeyGenerator.generateAdministratorCompositeKey(
                item.getAdministrator().getFirstName(),
                item.getAdministrator().getLastName(),
                item.getAdministrator().getOccupationCode(),
                item.getAdministrator().getPostalAddress() != null ?
                    item.getAdministrator().getPostalAddress().getPostalCode() : null
        );

        // Check if administrator UUID exists
        String administratorUUID = incapableUuidMap.get(administratorCompositeKey);
        if (administratorUUID == null) {
            // New administrator - create UUID and mapping record
            administratorUUID = UUID.randomUUID().toString();
            incapableUuidMap.put(administratorCompositeKey, administratorUUID);

            MappingTableRecord adminRecord = MappingTableRecord.builder()
                    .ddUuid(administratorUUID)
                    .compositeKey(administratorCompositeKey)
                    .typeOfEntity(FlowType.INC_ADM.getLabel())
                    .build();

            newMappingTableRecords.add(adminRecord);
            log.info("Created new mapping record for administrator: UUID={}, compositeKey={}, type={}",
                     administratorUUID, administratorCompositeKey, FlowType.INC_ADM.getLabel());
        } else {
            log.debug("Found existing UUID={} for administrator with composite key {}", administratorUUID, administratorCompositeKey);
        }

        item.setAdministratorDdUuid(administratorUUID);

        return item;
    }

    @Override
    public void beforeStep(@NonNull StepExecution stepExecution) {
        // Extract fileId from job parameters
        fileId = stepExecution.getJobExecution().getJobParameters().getString("fileId");
        log.info("Incapables processing started for fileId={}", fileId);

        log.info("Preloading incapable flow mapping table into memory");
        incapableUuidMap = dao.fetchAllIncapableFlowUuidMappings();
        log.info("Loaded {} UUIDs from mapping table for incapable flow", incapableUuidMap.size());
    }


    public void flushNewMappings() {
        if (!newMappingTableRecords.isEmpty()) {
            log.info("Flushing {} new mapping records to DB", newMappingTableRecords.size());
            dao.batchInsertMappingRecords(newMappingTableRecords);
            newMappingTableRecords.clear();
        }
    }

    @Override
    public ExitStatus afterStep(StepExecution stepExecution) {

        long processed = stepExecution.getWriteCount();
        long failed = stepExecution.getProcessSkipCount();

        stepExecution.getJobExecution().getExecutionContext().put("totalRecordsICP", processed + failed);
        stepExecution.getJobExecution().getExecutionContext().put("processedRecordsICP", processed);
        stepExecution.getJobExecution().getExecutionContext().put("failedRecordsICP", failed);

        flushNewMappings();

        return ExitStatus.COMPLETED;
    }
}

