logs analyse then tell files tht u want to analyse this error and fix it plz plz pl 
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@633548414 wrapping oracle.jdbc.driver.T4CConnection@74742899] after transaction
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || cleanupAfterCompletion || Resuming suspended transaction after completion of inner transaction
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.retry.support.RetryTemplate || doExecute || Retry: count=0
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Suspending current transaction, creating new transaction with name [com.ing.datadist.dao.ErrorLogDAO.logValidationError]
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1225001200 wrapping oracle.jdbc.driver.T4CConnection@74742899] for JDBC transaction
14/04/2026 09:12:01,586 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1225001200 wrapping oracle.jdbc.driver.T4CConnection@74742899] to manual commit
14/04/2026 09:12:01,587 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logValidationError || Data_Distributor_Error_Log: Logging validation error - RecordType:ORGANISATION_CHILD, ExternalIdentifier:0723880222, ErrorMsg:IndustryClass_Rank must be between 1 and 9. Current value: 0, FileId:FILE_1776150720966_04b50af6
14/04/2026 09:12:01,587 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,587 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_ERROR_LOG (RECORD_TYPE, External_IDENTIFIER, ERROR_TYPE, ERROR_MESSAGE, BATCH_ID, FILE_NAME, FILE_ID) VALUES (?, ?, ?, ?, ?, ?, ?)]
14/04/2026 09:12:01,592 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logValidationError || Data_Distributor_Error_Log: Validation error logged successfully for ExternalIdentifier:0723880222, FileId:FILE_1776150720966_04b50af6
14/04/2026 09:12:01,593 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,593 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1225001200 wrapping oracle.jdbc.driver.T4CConnection@74742899]
14/04/2026 09:12:01,594 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1225001200 wrapping oracle.jdbc.driver.T4CConnection@74742899] after transaction
14/04/2026 09:12:01,594 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || cleanupAfterCompletion || Resuming suspended transaction after completion of inner transaction
14/04/2026 09:12:01,594 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.retry.support.RetryTemplate || doExecute || Retry: count=0
14/04/2026 09:12:01,595 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,595 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT DD_UUID FROM DD_MAP_TBL WHERE ORG_NUMBER = ?]
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || WARN  || c.i.d.b.p.LegalEntityChildEnrichmentProcessor || process || Parent record not found for LE External Identifier: 0724737082
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Suspending current transaction, creating new transaction with name [com.ing.datadist.dao.ErrorLogDAO.logValidationError]
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1537903016 wrapping oracle.jdbc.driver.T4CConnection@74742899] for JDBC transaction
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1537903016 wrapping oracle.jdbc.driver.T4CConnection@74742899] to manual commit
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logValidationError || Data_Distributor_Error_Log: Logging validation error - RecordType:ORGANISATION_CHILD, ExternalIdentifier:0724737082, ErrorMsg:Parent record not found for LE External Identifier: 0724737082, FileId:FILE_1776150720966_04b50af6
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,597 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_ERROR_LOG (RECORD_TYPE, External_IDENTIFIER, ERROR_TYPE, ERROR_MESSAGE, BATCH_ID, FILE_NAME, FILE_ID) VALUES (?, ?, ?, ?, ?, ?, ?)]
14/04/2026 09:12:01,603 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logValidationError || Data_Distributor_Error_Log: Validation error logged successfully for ExternalIdentifier:0724737082, FileId:FILE_1776150720966_04b50af6
14/04/2026 09:12:01,603 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,603 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1537903016 wrapping oracle.jdbc.driver.T4CConnection@74742899]
14/04/2026 09:12:01,604 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1537903016 wrapping oracle.jdbc.driver.T4CConnection@74742899] after transaction
14/04/2026 09:12:01,604 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || cleanupAfterCompletion || Resuming suspended transaction after completion of inner transaction
14/04/2026 09:12:01,605 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.retry.support.RetryTemplate || doExecute || Retry: count=0
14/04/2026 09:12:01,605 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,605 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT DD_UUID FROM DD_MAP_TBL WHERE ORG_NUMBER = ?]
14/04/2026 09:12:01,607 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.retry.support.RetryTemplate || doExecute || Retry: count=0
14/04/2026 09:12:01,607 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || batchUpdate || Executing SQL batch update [INSERT INTO DD_LEGAL_ENTITY_CHILD_TBL (DD_UUID, INDUSTRY_CLASS_CODE, INDUSTRY_CLASS_CODE_RANK, INDUSTRY_CLASS_EFF_DATE, INDUSTRY_CLASS_END_DATE, FILE_ID) VALUES (?, ?, ?, ?, ?, ?)]
14/04/2026 09:12:01,607 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_LEGAL_ENTITY_CHILD_TBL (DD_UUID, INDUSTRY_CLASS_CODE, INDUSTRY_CLASS_CODE_RANK, INDUSTRY_CLASS_EFF_DATE, INDUSTRY_CLASS_END_DATE, FILE_ID) VALUES (?, ?, ?, ?, ?, ?)]
14/04/2026 09:12:01,608 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.support.JdbcUtils || supportsBatchUpdates || JDBC driver supports batch updates
14/04/2026 09:12:01,609 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Participating in existing transaction
14/04/2026 09:12:01,610 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,610 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE STEP_EXECUTION_ID = ?
]
14/04/2026 09:12:01,612 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Participating in existing transaction
14/04/2026 09:12:01,613 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,613 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION
SET START_TIME = ?, END_TIME = ?, STATUS = ?, COMMIT_COUNT = ?, READ_COUNT = ?, FILTER_COUNT = ?, WRITE_COUNT = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, READ_SKIP_COUNT = ?, PROCESS_SKIP_COUNT = ?, WRITE_SKIP_COUNT = ?, ROLLBACK_COUNT = ?, LAST_UPDATED = ?
WHERE STEP_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:01,614 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,615 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:01,616 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,616 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1642252176 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,618 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1642252176 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,618 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || o.s.batch.core.step.AbstractStep || execute || Step: [legalEntityChildEnrichStep] executed in 68ms
14/04/2026 09:12:01,618 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.updateExecutionContext]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,618 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@590163158 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,618 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@590163158 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,619 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,619 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE STEP_EXECUTION_ID = ?
]
14/04/2026 09:12:01,621 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,621 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@590163158 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,622 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@590163158 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,622 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.update]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,622 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@356690404 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,623 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@356690404 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,623 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,623 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION
SET START_TIME = ?, END_TIME = ?, STATUS = ?, COMMIT_COUNT = ?, READ_COUNT = ?, FILTER_COUNT = ?, WRITE_COUNT = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, READ_SKIP_COUNT = ?, PROCESS_SKIP_COUNT = ?, WRITE_SKIP_COUNT = ?, ROLLBACK_COUNT = ?, LAST_UPDATED = ?
WHERE STEP_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:01,624 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,625 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:01,626 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,626 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@356690404 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,627 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@356690404 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,627 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.updateExecutionContext]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,628 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1317792645 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,628 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1317792645 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,628 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,628 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_JOB_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE JOB_EXECUTION_ID = ?
]
14/04/2026 09:12:01,630 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,630 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1317792645 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,631 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1317792645 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,631 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.getLastStepExecution]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,632 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@498667947 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,632 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@498667947 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,632 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,632 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT SE.STEP_EXECUTION_ID, SE.STEP_NAME, SE.START_TIME, SE.END_TIME, SE.STATUS, SE.COMMIT_COUNT, SE.READ_COUNT, SE.FILTER_COUNT, SE.WRITE_COUNT, SE.EXIT_CODE, SE.EXIT_MESSAGE, SE.READ_SKIP_COUNT, SE.WRITE_SKIP_COUNT, SE.PROCESS_SKIP_COUNT, SE.ROLLBACK_COUNT, SE.LAST_UPDATED, SE.VERSION, SE.CREATE_TIME, JE.JOB_EXECUTION_ID, JE.START_TIME, JE.END_TIME, JE.STATUS, JE.EXIT_CODE, JE.EXIT_MESSAGE, JE.CREATE_TIME, JE.LAST_UPDATED, JE.VERSION
FROM BATCH_JOB_EXECUTION JE
	JOIN BATCH_STEP_EXECUTION SE ON SE.JOB_EXECUTION_ID = JE.JOB_EXECUTION_ID
WHERE JE.JOB_INSTANCE_ID = ? AND SE.STEP_NAME = ?
]
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@498667947 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@498667947 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.getStepExecutionCount]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@193052711 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@193052711 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,648 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT COUNT(*)
FROM BATCH_JOB_EXECUTION JE
	JOIN BATCH_STEP_EXECUTION SE ON SE.JOB_EXECUTION_ID = JE.JOB_EXECUTION_ID
WHERE JE.JOB_INSTANCE_ID = ? AND SE.STEP_NAME = ?
]
14/04/2026 09:12:01,665 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,665 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@193052711 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,665 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@193052711 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,665 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.add]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,666 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@921204681 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,666 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@921204681 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,667 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,667 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO BATCH_STEP_EXECUTION(STEP_EXECUTION_ID, VERSION, STEP_NAME, JOB_EXECUTION_ID, START_TIME, END_TIME, STATUS, COMMIT_COUNT, READ_COUNT, FILTER_COUNT, WRITE_COUNT, EXIT_CODE, EXIT_MESSAGE, READ_SKIP_COUNT, WRITE_SKIP_COUNT, PROCESS_SKIP_COUNT, ROLLBACK_COUNT, LAST_UPDATED, CREATE_TIME)
	VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)
]
14/04/2026 09:12:01,669 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,669 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO BATCH_STEP_EXECUTION_CONTEXT (SHORT_CONTEXT, SERIALIZED_CONTEXT, STEP_EXECUTION_ID)
	VALUES(?, ?, ?)
]
14/04/2026 09:12:01,670 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,671 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@921204681 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,671 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@921204681 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || o.s.batch.core.job.SimpleStepHandler || handleStep || Executing step: [organisationSearchApiTaskletStep]
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.update]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1138693258 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1138693258 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,672 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION
SET START_TIME = ?, END_TIME = ?, STATUS = ?, COMMIT_COUNT = ?, READ_COUNT = ?, FILTER_COUNT = ?, WRITE_COUNT = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, READ_SKIP_COUNT = ?, PROCESS_SKIP_COUNT = ?, WRITE_SKIP_COUNT = ?, ROLLBACK_COUNT = ?, LAST_UPDATED = ?
WHERE STEP_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:01,674 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,674 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:01,675 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,675 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1138693258 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,683 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1138693258 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,685 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.c.e.PropertySourcesPropertyResolver || logKeyFound || Found key 'app.apiFlow' in PropertySource 'environmentProperties' with value of type String
14/04/2026 09:12:01,686 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.c.e.PropertySourcesPropertyResolver || logKeyFound || Found key 'app.initialLoad' in PropertySource 'environmentProperties' with value of type String
14/04/2026 09:12:01,687 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.updateExecutionContext]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,687 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1496718397 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,687 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1496718397 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,687 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,688 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE STEP_EXECUTION_ID = ?
]
14/04/2026 09:12:01,689 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,689 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1496718397 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:01,690 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1496718397 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:01,690 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [null]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:01,691 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1493036889 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:01,691 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1493036889 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:01,691 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || execute || Data_Distributor_Coface_ORG: Starting API processing tasklet, apiFlow=true, fileId=FILE_1776150720006_a48fcce7
14/04/2026 09:12:01,692 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.dao.LegalEntityParentDAO || fetchRecordsByFileId || Data_Distributor_Coface_LE: Fetching parent records for fileId=FILE_1776150720006_a48fcce7, limit=10000
14/04/2026 09:12:01,692 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,692 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT DD_UUID, ORG_STATUS, ORG_NAME, ORG_OTHER_NAME, ORG_OTHER_NAME_TYPE, ADR_UNSTRUCTURED_ADDRESS, ADR_POSTALADDRESS_STREETNM, ADR_POSTALADDRESS_HOUSENUM, ADR_POSTALADDRESS_HOUSEADD, ADR_POSTALADDRESS_POSTALCD, ADR_POSTALADDRESS_CITYNAME, ADR_POSTALADDRESS_CNTRYCD, ORG_LEGAL_FORM, ORG_BUSINESS_CLOSE_DOWN_DATE, LE_LEGAL_STATUS, ORG_DATE_OF_FOUNDATION, LE_PREFERRED_LANGUAGE, ADR_DIGITALADDR_FULLTEL, NSSO_EXTL_IDENTIFIER, ASMT_VAT_STATUS, NSSO_EXTL_IDENTIFIER_STATUS, EXTERNALIDENTIFIER_VAL, FILE_ID FROM DD_LEGAL_ENTITY_PARENT_TBL WHERE FILE_ID = ? AND ROWNUM <= ?]
14/04/2026 09:12:01,694 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.dao.LegalEntityParentDAO || fetchRecordsByFileId || Data_Distributor_Coface_LE: Fetched 1 parent records for fileId=FILE_1776150720006_a48fcce7
14/04/2026 09:12:01,694 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.datadist.dao.LegalEntityChildDAO || fetchRecordsByFileId || Data_Distributor_Coface_LE: Fetching child records for fileId=FILE_1776150720966_04b50af6, limit=10000
14/04/2026 09:12:01,694 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:01,695 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT DD_UUID, INDUSTRY_CLASS_CODE, INDUSTRY_CLASS_CODE_RANK, INDUSTRY_CLASS_EFF_DATE, INDUSTRY_CLASS_END_DATE, FILE_ID FROM DD_LEGAL_ENTITY_CHILD_TBL WHERE FILE_ID = ? AND ROWNUM <= ?]
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.datadist.dao.LegalEntityChildDAO || fetchRecordsByFileId || Data_Distributor_Coface_LE: Fetched 1 child records for fileId=FILE_1776150720966_04b50af6
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || execute || Data_Distributor_Coface_ORG file records parent file size:1, child file size:1
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || execute || Data_Distributor_Coface_ORG Processing Organisation file, API FLOW:true
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || processOrganisation || Data_Distributor_Coface_LE Processing Organisation for uuid:814753a1-ed9c-48a1-97eb-71bdc716eda0
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || processOrganisation || Data_Distributor_Coface_LE Searching for Organisation for uuid:814753a1-ed9c-48a1-97eb-71bdc716eda0
14/04/2026 09:12:01,696 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartySearchService || searchInvolvedPartyByInternalIdentifier || searchInvolvedPartyByInternalIdentifier request payload: 814753a1-ed9c-48a1-97eb-71bdc716eda0 type:CSI_BE
14/04/2026 09:12:01,698 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || searchInvolvedPartyByInternalIdentifier || searchInvolvedPartyByInternalIdentifier request payload: SearchInvolvedPartiesRequestV1(entityMap={organisation=SearchInvolvedPartyByInternalIdentifierRequestV1(involvedPartyInternalIdentifier=CreateInternalIdentifierRequest(involvedPartyInternalIdentifierType=CSI_BE, involvedPartyInternalIdentifierValue=814753a1-ed9c-48a1-97eb-71bdc716eda0))})
14/04/2026 09:12:01,705 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Data_Distributor_Coface_OU API Request for /peer/v1/partyandagreementsearch/involved-parties/search -------------------------------
14/04/2026 09:12:01,706 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Method: POST
14/04/2026 09:12:01,706 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || URI: /peer/v1/partyandagreementsearch/involved-parties/search
14/04/2026 09:12:01,706 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Version: HTTP/1.1
14/04/2026 09:12:01,706 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Host: api.ing.com
14/04/2026 09:12:01,707 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Content-Type: application/json
14/04/2026 09:12:01,707 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Content-Length: 179
14/04/2026 09:12:01,707 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Body: {"organisation":{"involvedPartyInternalIdentifier":{"involvedPartyInternalIdentifierType":"CSI_BE","involvedPartyInternalIdentifierValue":"814753a1-ed9c-48a1-97eb-71bdc716eda0"}}}
14/04/2026 09:12:01,707 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Data_Distributor_Coface_OU API Request -------------------------------------------------
14/04/2026 09:12:01,707 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.h.r.HostAwareRoutingService || callHostSpecificService || Routing request 508898216 for host header: api.ing.com
14/04/2026 09:12:01,776 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.a.t.c.t.c.f.f.DebugLoggingFilter$ || make || DebugLogging is enabled for /endpoint/api.ing.com/POST/peer/v1/partyandagreementsearch/involved-parties/search, this might cause logging of sensitive information, not recommended for production!
14/04/2026 09:12:01,842 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.c.f.f.DebugLoggingFilter || apply || Sending request [508898216:cf4fd70327c3b821:23c99dd33e0faed26aae635e9fc799a8] to instance [Inet(172-21-16-230.tp-sea-tst.pod.cluster.local/172.21.16.230:8443,Map(instanceMetadata -> InstanceMetadata(172-21-16-230.tp-sea-tst.pod.cluster0047.non-prod.ichp.ing.net,8443,WPR,ModeLive,PartyandAgreementSearchAPI)))] with contents
POST /peer/v1/partyandagreementsearch/involved-parties/search HTTP/1.1
Host: api.ing.com
traceparent: 00-23c99dd33e0faed26aae635e9fc799a8-cf4fd70327c3b821-01
X-B3-SpanId: c2b536bf32a639d6
Content-Type: application/json
X-B3-TraceId: c2b536bf32a639d6
uber-trace-id: 23c99dd33e0faed26aae635e9fc799a8:cf4fd70327c3b821:0:1
Content-Length: 179

{"organisation":{"involvedPartyInternalIdentifier":{"involvedPartyInternalIdentifierType":"CSI_BE","involvedPartyInternalIdentifierValue":"814753a1-ed9c-48a1-97eb-71bdc716eda0"}}}
14/04/2026 09:12:01,857 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.c.f.f.DebugLoggingFilter || $anonfun$apply$3 || Received response [2080200748] to request [508898216:Some(cf4fd70327c3b821:23c99dd33e0faed26aae635e9fc799a8)] from instance [Inet(172-21-16-230.tp-sea-tst.pod.cluster.local/172.21.16.230:8443,Map(instanceMetadata -> InstanceMetadata(172-21-16-230.tp-sea-tst.pod.cluster0047.non-prod.ichp.ing.net,8443,WPR,ModeLive,PartyandAgreementSearchAPI)))] with contents
HTTP/1.1 200 OK
Date: Tue, 14 Apr 2026 07:12:01 GMT
traceparent: 00-23c99dd33e0faed26aae635e9fc799a8-820d6b1d0142a0b5-01
Content-Type: application/json
Content-Length: 56

{"organisations":[],"offset":0,"totalNumberOfResults":0}
14/04/2026 09:12:01,859 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || lambda$searchInvolvedPartyByInternalIdentifier$2 || searchInvolvedPartyByInternalIdentifier response: Response("HTTP/1.1 Status(200)")
14/04/2026 09:12:01,890 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || processOrganisation || Data_Distributor_Coface_LE Organisation not found, Creating organisation for uuid:814753a1-ed9c-48a1-97eb-71bdc716eda0
14/04/2026 09:12:01,891 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Suspending current transaction, creating new transaction with name [com.ing.datadist.dao.ErrorLogDAO.logOnePamValidationError]
14/04/2026 09:12:01,891 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@963910896 wrapping oracle.jdbc.driver.T4CConnection@74742899] for JDBC transaction
14/04/2026 09:12:01,891 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@963910896 wrapping oracle.jdbc.driver.T4CConnection@74742899] to manual commit
14/04/2026 09:12:01,893 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logOnePamValidationError || Data_Distributor_Error_Log: Logging OnePAM validation error - RecordType:ORGANISATION, ExternalIdentifier:null, DDUuid:814753a1-ed9c-48a1-97eb-71bdc716eda0, ErrorMsg:Organisation not found in OnePAM for OrgUUID: 814753a1-ed9c-48a1-97eb-71bdc716eda0 ,going to create flow., FileId:FILE_1776150720006_a48fcce7
14/04/2026 09:12:01,893 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:01,893 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_ERROR_LOG (RECORD_TYPE, External_IDENTIFIER, DD_UUID, ERROR_TYPE, ERROR_MESSAGE, BATCH_ID, FILE_NAME, FILE_ID, CREATED_BY, CREATED_TS) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, SYSTIMESTAMP)]
14/04/2026 09:12:01,900 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logOnePamValidationError || Data_Distributor_Error_Log: OnePAM validation error logged successfully for ExternalIdentifier:null, FileId:FILE_1776150720006_a48fcce7
14/04/2026 09:12:01,900 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:01,900 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@963910896 wrapping oracle.jdbc.driver.T4CConnection@74742899]
14/04/2026 09:12:01,905 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@963910896 wrapping oracle.jdbc.driver.T4CConnection@74742899] after transaction
14/04/2026 09:12:01,905 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || cleanupAfterCompletion || Resuming suspended transaction after completion of inner transaction
14/04/2026 09:12:01,905 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || processOrganisation || Data_Distributor_Coface_LE TEST-LE API FLOW
14/04/2026 09:12:01,905 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.service.OrganisationService || createOrganisation || Data_Distributor_Coface_ORG Creating organisation with Primary Name: Stines pvt lmt, Other Name: STON
14/04/2026 09:12:01,905 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.service.OrganisationService || createOrganisation || Data_Distributor_Coface_ORG Name Types - Primary: LGL_NM, Other: LGL_NM_SHRT
14/04/2026 09:12:01,906 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.service.OrganisationService || createOrganisation || Data_Distributor_Coface_ORG Total organisation names to create: 2
14/04/2026 09:12:01,908 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || createInvolvedParty || CreateInvolvedParty request payload: CreateInvolvedPartyRequestV5(individual=null, organisation=CreateOrganisationRequest(dataSource=DIDD_CD_BE, logicalDataDomain=ING_BE_EXT_DATA, countryOfResidence=BE, preferredLanguage=nl, financialLegalStatusType=IN_LQD, channelOfEntry=MOB_CHAN, effectiveDate=2026-04-14T00:00:00.000Z, endDate=null, countryOfIncorporation=null, dateOfFoundation=1996-12-10, legalForm=BE_129, organisationLifeCycleStatusType=ACTV_ORG, businessClosedDownDate=2026-12-16, organisationNames=[CreateOrganisationNameRequest(organisationNameType=LGL_NM, organisationName=Stines pvt lmt, effectiveDate=null, endDate=null, dataSource=DIDD_CD_BE), CreateOrganisationNameRequest(organisationNameType=LGL_NM_SHRT, organisationName=STON, effectiveDate=null, endDate=null, dataSource=DIDD_CD_BE)], involvedPartyInternalIdentifiers=[CreateInternalIdentifierRequest(involvedPartyInternalIdentifierType=CSI_BE, involvedPartyInternalIdentifierValue=814753a1-ed9c-48a1-97eb-71bdc716eda0)]), organisationUnit=null)
14/04/2026 09:12:01,920 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Data_Distributor_Coface_OU API Request for /v5/involved-parties -------------------------------
14/04/2026 09:12:01,920 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Method: POST
14/04/2026 09:12:01,920 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || URI: /v5/involved-parties
14/04/2026 09:12:01,920 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Version: HTTP/1.1
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Host: apis.ing.com
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Content-Type: application/json;charset=UTF-8
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: Content-Length: 749
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Header: X-ING-LastUpdateUser: DD_USER
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Body: {"organisation":{"dataSource":"DIDD_CD_BE","logicalDataDomain":"ING_BE_EXT_DATA","countryOfResidence":"BE","preferredLanguage":"nl","financialLegalStatusType":"IN_LQD","channelOfEntry":"MOB_CHAN","effectiveDate":"2026-04-14T00:00:00.000Z","dateOfFoundation":"1996-12-10","legalForm":"BE_129","organisationLifeCycleStatusType":"ACTV_ORG","businessClosedDownDate":"2026-12-16","organisationNames":[{"organisationNameType":"LGL_NM","organisationName":"Stines pvt lmt","dataSource":"DIDD_CD_BE"},{"organisationNameType":"LGL_NM_SHRT","organisationName":"STON","dataSource":"DIDD_CD_BE"}],"involvedPartyInternalIdentifiers":[{"involvedPartyInternalIdentifierType":"CSI_BE","involvedPartyInternalIdentifierValue":"814753a1-ed9c-48a1-97eb-71bdc716eda0"}]}}
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.s.InvolvedPartyOnePamRepository || printRequest || Data_Distributor_Coface_OU API Request -------------------------------------------------
14/04/2026 09:12:01,921 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.h.r.HostAwareRoutingService || callHostSpecificService || Routing request 2096070475 for host header: apis.ing.com
14/04/2026 09:12:01,986 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.a.t.c.t.c.f.f.DebugLoggingFilter$ || make || DebugLogging is enabled for /endpoint/apis.ing.com/POST/v5/involved-parties, this might cause logging of sensitive information, not recommended for production!
14/04/2026 09:12:02,043 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.c.f.f.DebugLoggingFilter || apply || Sending request [2096070475:20dd7293b54d6afd:00398db9cd7c180511ab6134fdff5096] to instance [Inet(172-20-17-77.tp-ivp-tst.pod.cluster0046.non-prod.ichp.ing.net/10.219.120.7:8443,Map(instanceMetadata -> InstanceMetadata(172-20-17-77.tp-ivp-tst.pod.cluster0046.non-prod.ichp.ing.net,8443,DCR,ModeLive,InvolvedPartyAPI)))] with contents
POST /v5/involved-parties HTTP/1.1
Host: apis.ing.com
traceparent: 00-00398db9cd7c180511ab6134fdff5096-20dd7293b54d6afd-01
X-B3-SpanId: d3b3deaf7d3e79df
Content-Type: application/json;charset=UTF-8
X-B3-TraceId: d3b3deaf7d3e79df
uber-trace-id: 00398db9cd7c180511ab6134fdff5096:20dd7293b54d6afd:0:1
Content-Length: 749
X-ING-LastUpdateUser: DD_USER

{"organisation":{"dataSource":"DIDD_CD_BE","logicalDataDomain":"ING_BE_EXT_DATA","countryOfResidence":"BE","preferredLanguage":"nl","financialLegalStatusType":"IN_LQD","channelOfEntry":"MOB_CHAN","effectiveDate":"2026-04-14T00:00:00.000Z","dateOfFoundation":"1996-12-10","legalForm":"BE_129","organisationLifeCycleStatusType":"ACTV_ORG","businessClosedDownDate":"2026-12-16","organisationNames":[{"organisationNameType":"LGL_NM","organisationName":"Stines pvt lmt","dataSource":"DIDD_CD_BE"},{"organisationNameType":"LGL_NM_SHRT","organisationName":"STON","dataSource":"DIDD_CD_BE"}],"involvedPartyInternalIdentifiers":[{"involvedPartyInternalIdentifierType":"CSI_BE","involvedPartyInternalIdentifierValue":"814753a1-ed9c-48a1-97eb-71bdc716eda0"}]}}
14/04/2026 09:12:02,175 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.t.c.t.c.f.f.DebugLoggingFilter || $anonfun$apply$3 || Received response [504497595] to request [2096070475:Some(20dd7293b54d6afd:00398db9cd7c180511ab6134fdff5096)] from instance [Inet(172-20-17-77.tp-ivp-tst.pod.cluster0046.non-prod.ichp.ing.net/10.219.120.7:8443,Map(instanceMetadata -> InstanceMetadata(172-20-17-77.tp-ivp-tst.pod.cluster0046.non-prod.ichp.ing.net,8443,DCR,ModeLive,InvolvedPartyAPI)))] with contents
HTTP/1.1 400 Bad Request
Date: Tue, 14 Apr 2026 07:12:02 GMT
Pragma: no-cache
Connection: close
traceparent: 00-00398db9cd7c180511ab6134fdff5096-69394861c1834807-01
Content-Type: application/json
Cache-Control: no-store
Content-Length: 203

{
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}
14/04/2026 09:12:02,176 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.d.a.s.InvolvedPartyOnePamRepository || checkHttpStatusOrThrow || API CREATE_INVOLVED_PARTY failed: status=400, body={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}
14/04/2026 09:12:02,177 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.d.a.e.DataDistributionApiException || <init> || ReqKey CREATE_INVOLVED_PARTY - DataDistributionApiException message HTTP call failed for CREATE_INVOLVED_PARTY - innerMessage {
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}
14/04/2026 09:12:02,179 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,180 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_API_STATUS_TBL (DD_UUID, FILE_ID, FLOW_NAME, API_ENDPOINT, API_METHOD, STATUS, REQUEST_PAYLOAD, RESPONSE_STATUS_CODE, RESPONSE_PAYLOAD, ERROR_CODE, ERROR_MESSAGE, RETRY_COUNT, CREATED_BY, CREATED_TS) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, 0, 'DD_USER', SYSTIMESTAMP)]
14/04/2026 09:12:02,181 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.dao.ApiTransactionLogDAO || logApiTransaction || DD_API_STATUS Logged Flow=COFACE_LE_PARENT, Endpoint=https://apis.ing.com/v5/involved-parties, Status=FAILED, Code=null, DD_UUID=814753a1-ed9c-48a1-97eb-71bdc716eda0, FileId=FILE_1776150720006_a48fcce7
14/04/2026 09:12:02,181 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.d.a.service.OrganisationService || createOrganisation || Create failed for ddUuid 814753a1-ed9c-48a1-97eb-71bdc716eda0: DataDistributionApiException(code=400, innerMessage={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}, timeStamp=1776150722177)
java.util.concurrent.ExecutionException: DataDistributionApiException(code=400, innerMessage={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}, timeStamp=1776150722177)
	at java.base/java.util.concurrent.CompletableFuture.reportGet(CompletableFuture.java:396)
	at java.base/java.util.concurrent.CompletableFuture.get(CompletableFuture.java:2073)
	at com.ing.datadist.api.service.OrganisationService.createOrganisation(OrganisationService.java:453)
	at com.ing.datadist.api.service.OrganisationService.processOrganisation(OrganisationService.java:75)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet.processOrganisation(OrganisationSearchApiTasklet.java:226)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet.execute(OrganisationSearchApiTasklet.java:138)
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
	at java.base/java.lang.reflect.Method.invoke(Method.java:580)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:360)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:196)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
	at org.springframework.aop.support.DelegatingIntroductionInterceptor.doProceed(DelegatingIntroductionInterceptor.java:137)
	at org.springframework.aop.support.DelegatingIntroductionInterceptor.invoke(DelegatingIntroductionInterceptor.java:124)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:184)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:728)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet$$SpringCGLIB$$0.execute(<generated>)
	at org.springframework.batch.core.step.tasklet.TaskletStep$ChunkTransactionCallback.doInTransaction(TaskletStep.java:383)
	at org.springframework.batch.core.step.tasklet.TaskletStep$ChunkTransactionCallback.doInTransaction(TaskletStep.java:307)
	at org.springframework.transaction.support.TransactionTemplate.execute(TransactionTemplate.java:140)
	at org.springframework.batch.core.step.tasklet.TaskletStep$2.doInChunkContext(TaskletStep.java:250)
	at org.springframework.batch.core.scope.context.StepContextRepeatCallback.doInIteration(StepContextRepeatCallback.java:82)
	at org.springframework.batch.repeat.support.RepeatTemplate.getNextResult(RepeatTemplate.java:369)
	at org.springframework.batch.repeat.support.RepeatTemplate.executeInternal(RepeatTemplate.java:206)
	at org.springframework.batch.repeat.support.RepeatTemplate.iterate(RepeatTemplate.java:140)
	at org.springframework.batch.core.step.tasklet.TaskletStep.doExecute(TaskletStep.java:235)
	at org.springframework.batch.core.step.AbstractStep.execute(AbstractStep.java:230)
	at org.springframework.batch.core.job.SimpleStepHandler.handleStep(SimpleStepHandler.java:153)
	at org.springframework.batch.core.job.AbstractJob.handleStep(AbstractJob.java:403)
	at org.springframework.batch.core.job.SimpleJob.doExecute(SimpleJob.java:127)
	at org.springframework.batch.core.job.AbstractJob.execute(AbstractJob.java:305)
	at org.springframework.batch.core.launch.support.TaskExecutorJobLauncher$1.run(TaskExecutorJobLauncher.java:155)
	at org.springframework.core.task.SyncTaskExecutor.execute(SyncTaskExecutor.java:48)
	at org.springframework.batch.core.launch.support.TaskExecutorJobLauncher.run(TaskExecutorJobLauncher.java:146)
	at com.ing.datadist.batch.schedular.BatchSchedular.runLE(BatchSchedular.java:294)
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
	at java.base/java.lang.reflect.Method.invoke(Method.java:580)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.runInternal(ScheduledMethodRunnable.java:130)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.lambda$run$2(ScheduledMethodRunnable.java:124)
	at io.micrometer.observation.Observation.observe(Observation.java:498)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.run(ScheduledMethodRunnable.java:124)
	at org.springframework.scheduling.config.Task$OutcomeTrackingRunnable.run(Task.java:87)
	at org.springframework.scheduling.support.DelegatingErrorHandlingRunnable.run(DelegatingErrorHandlingRunnable.java:54)
	at org.springframework.scheduling.concurrent.ReschedulingRunnable.run(ReschedulingRunnable.java:96)
	at java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:572)
	at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:317)
	at java.base/java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:304)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at java.base/java.lang.Thread.run(Thread.java:1583)
Caused by: DataDistributionApiException(code=400, innerMessage={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}, timeStamp=1776150722177)
	at com.ing.datadist.api.service.InvolvedPartyOnePamRepository.checkHttpStatusOrThrow(InvolvedPartyOnePamRepository.java:432)
	at com.ing.datadist.api.service.InvolvedPartyOnePamRepository.lambda$createInvolvedParty$0(InvolvedPartyOnePamRepository.java:67)
	at java.base/java.util.concurrent.CompletableFuture$UniApply.tryFire(CompletableFuture.java:646)
	at java.base/java.util.concurrent.CompletableFuture.postComplete(CompletableFuture.java:510)
	at java.base/java.util.concurrent.CompletableFuture.complete(CompletableFuture.java:2179)
	at com.ing.apisdk.toolkit.connectivity.api.Implicits$FinagleServiceBasicOps$$anon$1.$anonfun$apply$2(Implicits.scala:40)
	at com.ing.apisdk.toolkit.connectivity.api.Implicits$FinagleServiceBasicOps$$anon$1.$anonfun$apply$2$adapted(Implicits.scala:40)
	at com.twitter.util.Future.$anonfun$onSuccess$1(Future.scala:1965)
	at com.twitter.util.Future.$anonfun$onSuccess$1$adapted(Future.scala:1964)
	at com.twitter.util.Promise$Monitored.$anonfun$apply$1(Promise.scala:218)
	at scala.runtime.java8.JFunction0$mcV$sp.apply(JFunction0$mcV$sp.scala:18)
	at com.twitter.util.Local$.let(Local.scala:7030)
	at com.twitter.util.Promise$Monitored.apply(Promise.scala:218)
	at com.twitter.util.Promise$WaitQueue.com$twitter$util$Promise$WaitQueue$$$anonfun$runInScheduler$1(Promise.scala:97)
	at com.twitter.util.Promise$WaitQueue$$anonfun$runInScheduler$2.doRun(Promise.scala:97)
	at com.twitter.util.FiberTask.run(FiberTask.scala:14)
	at com.twitter.concurrent.LocalScheduler$Activation.run(Scheduler.scala:167)
	at com.twitter.concurrent.LocalScheduler$Activation.submit(Scheduler.scala:126)
	at com.twitter.concurrent.LocalScheduler.submit(Scheduler.scala:243)
	at com.twitter.concurrent.Scheduler$.submit(Scheduler.scala:78)
	at com.twitter.util.Fiber$$anon$1.submitTask(Fiber.scala:22)
	at com.twitter.util.Promise$WaitQueue.runInScheduler(Promise.scala:97)
	at com.twitter.util.Promise.updateIfEmpty(Promise.scala:825)
	at com.twitter.util.Promise.update(Promise.scala:788)
	at com.twitter.util.Promise.setValue(Promise.scala:764)
	at com.twitter.concurrent.AsyncQueue.offer(AsyncQueue.scala:121)
	at com.twitter.finagle.netty4.transport.ChannelTransport$$anon$2.channelRead(ChannelTransport.scala:169)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.UnpoolHttpHandler$.channelRead(UnpoolHttpHandler.scala:32)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.ClientExceptionMapper$.channelRead(ClientExceptionMapper.scala:35)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.UriValidatorHandler$.channelRead(UriValidatorHandler.scala:30)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.HeaderValidatorHandler$.channelRead(HeaderValidatorHandler.scala:51)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.codec.MessageToMessageDecoder.channelRead(MessageToMessageDecoder.java:107)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.codec.http.HttpContentDecoder.decode(HttpContentDecoder.java:166)
	at io.netty.handler.codec.http.HttpContentDecoder.decode(HttpContentDecoder.java:48)
	at io.netty.handler.codec.MessageToMessageDecoder.channelRead(MessageToMessageDecoder.java:91)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.CombinedChannelDuplexHandler$DelegatingChannelHandlerContext.fireChannelRead(CombinedChannelDuplexHandler.java:436)
	at io.netty.handler.codec.ByteToMessageDecoder.fireChannelRead(ByteToMessageDecoder.java:361)
	at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:325)
	at io.netty.channel.CombinedChannelDuplexHandler.channelRead(CombinedChannelDuplexHandler.java:251)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:93)
	at com.twitter.finagle.netty4.channel.ChannelRequestStatsHandler.channelRead(ChannelRequestStatsHandler.scala:48)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:93)
	at com.twitter.finagle.netty4.channel.ChannelStatsHandler.channelRead(ChannelStatsHandler.scala:151)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.ssl.SslHandler.unwrap(SslHandler.java:1519)
	at io.netty.handler.ssl.SslHandler.decodeJdkCompatible(SslHandler.java:1377)
	at io.netty.handler.ssl.SslHandler.decode(SslHandler.java:1428)
	at io.netty.handler.codec.ByteToMessageDecoder.decodeRemovalReentryProtection(ByteToMessageDecoder.java:545)
	at io.netty.handler.codec.ByteToMessageDecoder.callDecode(ByteToMessageDecoder.java:484)
	at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:296)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.DefaultChannelPipeline$HeadContext.channelRead(DefaultChannelPipeline.java:1357)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:440)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.DefaultChannelPipeline.fireChannelRead(DefaultChannelPipeline.java:868)
	at io.netty.channel.epoll.AbstractEpollStreamChannel$EpollStreamUnsafe.epollInReady(AbstractEpollStreamChannel.java:805)
	at io.netty.channel.epoll.EpollEventLoop.processReady(EpollEventLoop.java:501)
	at io.netty.channel.epoll.EpollEventLoop.run(EpollEventLoop.java:399)
	at io.netty.util.concurrent.SingleThreadEventExecutor$4.run(SingleThreadEventExecutor.java:998)
	at io.netty.util.internal.ThreadExecutorMap$2.run(ThreadExecutorMap.java:74)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at com.twitter.finagle.util.BlockingTimeTrackingThreadFactory$$anon$1.run(BlockingTimeTrackingThreadFactory.scala:23)
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30)
	... 1 common frames omitted
14/04/2026 09:12:02,185 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,185 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_API_STATUS_TBL (DD_UUID, FILE_ID, FLOW_NAME, API_ENDPOINT, API_METHOD, STATUS, REQUEST_PAYLOAD, RESPONSE_STATUS_CODE, RESPONSE_PAYLOAD, ERROR_CODE, ERROR_MESSAGE, RETRY_COUNT, CREATED_BY, CREATED_TS) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, 0, 'DD_USER', SYSTIMESTAMP)]
14/04/2026 09:12:02,187 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.dao.ApiTransactionLogDAO || logApiTransaction || DD_API_STATUS Logged Flow=COFACE_LE_PARENT, Endpoint=https://apis.ing.com/v5/involved-parties, Status=FAILED, Code=null, DD_UUID=814753a1-ed9c-48a1-97eb-71bdc716eda0, FileId=FILE_1776150720006_a48fcce7
14/04/2026 09:12:02,187 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Suspending current transaction, creating new transaction with name [com.ing.datadist.dao.ErrorLogDAO.logApiError]
14/04/2026 09:12:02,187 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@685681096 wrapping oracle.jdbc.driver.T4CConnection@74742899] for JDBC transaction
14/04/2026 09:12:02,187 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@685681096 wrapping oracle.jdbc.driver.T4CConnection@74742899] to manual commit
14/04/2026 09:12:02,189 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logApiError || Data_Distributor_Error_Log: Logging error - RecordType:ORGANISATION, ExternalIdentifier:0500000170, ErrorType:API_ERROR, ErrorCode:null, FileId:FILE_1776150720006_a48fcce7
14/04/2026 09:12:02,189 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,189 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [INSERT INTO DD_ERROR_LOG (RECORD_TYPE, External_IDENTIFIER, DD_UUID, ERROR_CODE, ERROR_TYPE, ERROR_MESSAGE, API_ENDPOINT, REQUEST_PAYLOAD, RESPONSE_PAYLOAD, BATCH_ID, FILE_NAME, FILE_ID) VALUES (?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?, ?)]
14/04/2026 09:12:02,200 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || com.ing.datadist.dao.ErrorLogDAO || logApiError || Data_Distributor_Error_Log: Error logged successfully for ExternalIdentifier:0500000170, FileId:FILE_1776150720006_a48fcce7
14/04/2026 09:12:02,200 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,200 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@685681096 wrapping oracle.jdbc.driver.T4CConnection@74742899]
14/04/2026 09:12:02,201 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@685681096 wrapping oracle.jdbc.driver.T4CConnection@74742899] after transaction
14/04/2026 09:12:02,201 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || cleanupAfterCompletion || Resuming suspended transaction after completion of inner transaction
14/04/2026 09:12:02,202 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || ERROR || c.i.d.a.service.OrganisationService || processOrganisation || Failed to create organisation for ddUuid: 814753a1-ed9c-48a1-97eb-71bdc716eda0
java.lang.RuntimeException: Create organisation interrupted
	at com.ing.datadist.api.service.OrganisationService.createOrganisation(OrganisationService.java:479)
	at com.ing.datadist.api.service.OrganisationService.processOrganisation(OrganisationService.java:75)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet.processOrganisation(OrganisationSearchApiTasklet.java:226)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet.execute(OrganisationSearchApiTasklet.java:138)
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
	at java.base/java.lang.reflect.Method.invoke(Method.java:580)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:360)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:196)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
	at org.springframework.aop.support.DelegatingIntroductionInterceptor.doProceed(DelegatingIntroductionInterceptor.java:137)
	at org.springframework.aop.support.DelegatingIntroductionInterceptor.invoke(DelegatingIntroductionInterceptor.java:124)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:184)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:728)
	at com.ing.datadist.batch.tasklet.OrganisationSearchApiTasklet$$SpringCGLIB$$0.execute(<generated>)
	at org.springframework.batch.core.step.tasklet.TaskletStep$ChunkTransactionCallback.doInTransaction(TaskletStep.java:383)
	at org.springframework.batch.core.step.tasklet.TaskletStep$ChunkTransactionCallback.doInTransaction(TaskletStep.java:307)
	at org.springframework.transaction.support.TransactionTemplate.execute(TransactionTemplate.java:140)
	at org.springframework.batch.core.step.tasklet.TaskletStep$2.doInChunkContext(TaskletStep.java:250)
	at org.springframework.batch.core.scope.context.StepContextRepeatCallback.doInIteration(StepContextRepeatCallback.java:82)
	at org.springframework.batch.repeat.support.RepeatTemplate.getNextResult(RepeatTemplate.java:369)
	at org.springframework.batch.repeat.support.RepeatTemplate.executeInternal(RepeatTemplate.java:206)
	at org.springframework.batch.repeat.support.RepeatTemplate.iterate(RepeatTemplate.java:140)
	at org.springframework.batch.core.step.tasklet.TaskletStep.doExecute(TaskletStep.java:235)
	at org.springframework.batch.core.step.AbstractStep.execute(AbstractStep.java:230)
	at org.springframework.batch.core.job.SimpleStepHandler.handleStep(SimpleStepHandler.java:153)
	at org.springframework.batch.core.job.AbstractJob.handleStep(AbstractJob.java:403)
	at org.springframework.batch.core.job.SimpleJob.doExecute(SimpleJob.java:127)
	at org.springframework.batch.core.job.AbstractJob.execute(AbstractJob.java:305)
	at org.springframework.batch.core.launch.support.TaskExecutorJobLauncher$1.run(TaskExecutorJobLauncher.java:155)
	at org.springframework.core.task.SyncTaskExecutor.execute(SyncTaskExecutor.java:48)
	at org.springframework.batch.core.launch.support.TaskExecutorJobLauncher.run(TaskExecutorJobLauncher.java:146)
	at com.ing.datadist.batch.schedular.BatchSchedular.runLE(BatchSchedular.java:294)
	at java.base/jdk.internal.reflect.DirectMethodHandleAccessor.invoke(DirectMethodHandleAccessor.java:103)
	at java.base/java.lang.reflect.Method.invoke(Method.java:580)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.runInternal(ScheduledMethodRunnable.java:130)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.lambda$run$2(ScheduledMethodRunnable.java:124)
	at io.micrometer.observation.Observation.observe(Observation.java:498)
	at org.springframework.scheduling.support.ScheduledMethodRunnable.run(ScheduledMethodRunnable.java:124)
	at org.springframework.scheduling.config.Task$OutcomeTrackingRunnable.run(Task.java:87)
	at org.springframework.scheduling.support.DelegatingErrorHandlingRunnable.run(DelegatingErrorHandlingRunnable.java:54)
	at org.springframework.scheduling.concurrent.ReschedulingRunnable.run(ReschedulingRunnable.java:96)
	at java.base/java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:572)
	at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:317)
	at java.base/java.util.concurrent.ScheduledThreadPoolExecutor$ScheduledFutureTask.run(ScheduledThreadPoolExecutor.java:304)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at java.base/java.lang.Thread.run(Thread.java:1583)
Caused by: java.util.concurrent.ExecutionException: DataDistributionApiException(code=400, innerMessage={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}, timeStamp=1776150722177)
	at java.base/java.util.concurrent.CompletableFuture.reportGet(CompletableFuture.java:396)
	at java.base/java.util.concurrent.CompletableFuture.get(CompletableFuture.java:2073)
	at com.ing.datadist.api.service.OrganisationService.createOrganisation(OrganisationService.java:453)
	... 46 common frames omitted
Caused by: DataDistributionApiException(code=400, innerMessage={
  "error" : {
    "code" : 400,
    "message" : "Request not valid",
    "innerMessage" : "Duplicate identifier values exist for the identifier type",
    "timestamp" : "2026-04-14T07:12:02.172Z"
  }
}, timeStamp=1776150722177)
	at com.ing.datadist.api.service.InvolvedPartyOnePamRepository.checkHttpStatusOrThrow(InvolvedPartyOnePamRepository.java:432)
	at com.ing.datadist.api.service.InvolvedPartyOnePamRepository.lambda$createInvolvedParty$0(InvolvedPartyOnePamRepository.java:67)
	at java.base/java.util.concurrent.CompletableFuture$UniApply.tryFire(CompletableFuture.java:646)
	at java.base/java.util.concurrent.CompletableFuture.postComplete(CompletableFuture.java:510)
	at java.base/java.util.concurrent.CompletableFuture.complete(CompletableFuture.java:2179)
	at com.ing.apisdk.toolkit.connectivity.api.Implicits$FinagleServiceBasicOps$$anon$1.$anonfun$apply$2(Implicits.scala:40)
	at com.ing.apisdk.toolkit.connectivity.api.Implicits$FinagleServiceBasicOps$$anon$1.$anonfun$apply$2$adapted(Implicits.scala:40)
	at com.twitter.util.Future.$anonfun$onSuccess$1(Future.scala:1965)
	at com.twitter.util.Future.$anonfun$onSuccess$1$adapted(Future.scala:1964)
	at com.twitter.util.Promise$Monitored.$anonfun$apply$1(Promise.scala:218)
	at scala.runtime.java8.JFunction0$mcV$sp.apply(JFunction0$mcV$sp.scala:18)
	at com.twitter.util.Local$.let(Local.scala:7030)
	at com.twitter.util.Promise$Monitored.apply(Promise.scala:218)
	at com.twitter.util.Promise$WaitQueue.com$twitter$util$Promise$WaitQueue$$$anonfun$runInScheduler$1(Promise.scala:97)
	at com.twitter.util.Promise$WaitQueue$$anonfun$runInScheduler$2.doRun(Promise.scala:97)
	at com.twitter.util.FiberTask.run(FiberTask.scala:14)
	at com.twitter.concurrent.LocalScheduler$Activation.run(Scheduler.scala:167)
	at com.twitter.concurrent.LocalScheduler$Activation.submit(Scheduler.scala:126)
	at com.twitter.concurrent.LocalScheduler.submit(Scheduler.scala:243)
	at com.twitter.concurrent.Scheduler$.submit(Scheduler.scala:78)
	at com.twitter.util.Fiber$$anon$1.submitTask(Fiber.scala:22)
	at com.twitter.util.Promise$WaitQueue.runInScheduler(Promise.scala:97)
	at com.twitter.util.Promise.updateIfEmpty(Promise.scala:825)
	at com.twitter.util.Promise.update(Promise.scala:788)
	at com.twitter.util.Promise.setValue(Promise.scala:764)
	at com.twitter.concurrent.AsyncQueue.offer(AsyncQueue.scala:121)
	at com.twitter.finagle.netty4.transport.ChannelTransport$$anon$2.channelRead(ChannelTransport.scala:169)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.UnpoolHttpHandler$.channelRead(UnpoolHttpHandler.scala:32)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.ClientExceptionMapper$.channelRead(ClientExceptionMapper.scala:35)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.UriValidatorHandler$.channelRead(UriValidatorHandler.scala:30)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at com.twitter.finagle.netty4.http.handler.HeaderValidatorHandler$.channelRead(HeaderValidatorHandler.scala:51)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.codec.MessageToMessageDecoder.channelRead(MessageToMessageDecoder.java:107)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.codec.http.HttpContentDecoder.decode(HttpContentDecoder.java:166)
	at io.netty.handler.codec.http.HttpContentDecoder.decode(HttpContentDecoder.java:48)
	at io.netty.handler.codec.MessageToMessageDecoder.channelRead(MessageToMessageDecoder.java:91)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.CombinedChannelDuplexHandler$DelegatingChannelHandlerContext.fireChannelRead(CombinedChannelDuplexHandler.java:436)
	at io.netty.handler.codec.ByteToMessageDecoder.fireChannelRead(ByteToMessageDecoder.java:361)
	at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:325)
	at io.netty.channel.CombinedChannelDuplexHandler.channelRead(CombinedChannelDuplexHandler.java:251)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:93)
	at com.twitter.finagle.netty4.channel.ChannelRequestStatsHandler.channelRead(ChannelRequestStatsHandler.scala:48)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.ChannelInboundHandlerAdapter.channelRead(ChannelInboundHandlerAdapter.java:93)
	at com.twitter.finagle.netty4.channel.ChannelStatsHandler.channelRead(ChannelStatsHandler.scala:151)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:442)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.handler.ssl.SslHandler.unwrap(SslHandler.java:1519)
	at io.netty.handler.ssl.SslHandler.decodeJdkCompatible(SslHandler.java:1377)
	at io.netty.handler.ssl.SslHandler.decode(SslHandler.java:1428)
	at io.netty.handler.codec.ByteToMessageDecoder.decodeRemovalReentryProtection(ByteToMessageDecoder.java:545)
	at io.netty.handler.codec.ByteToMessageDecoder.callDecode(ByteToMessageDecoder.java:484)
	at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:296)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:444)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:412)
	at io.netty.channel.DefaultChannelPipeline$HeadContext.channelRead(DefaultChannelPipeline.java:1357)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:440)
	at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:420)
	at io.netty.channel.DefaultChannelPipeline.fireChannelRead(DefaultChannelPipeline.java:868)
	at io.netty.channel.epoll.AbstractEpollStreamChannel$EpollStreamUnsafe.epollInReady(AbstractEpollStreamChannel.java:805)
	at io.netty.channel.epoll.EpollEventLoop.processReady(EpollEventLoop.java:501)
	at io.netty.channel.epoll.EpollEventLoop.run(EpollEventLoop.java:399)
	at io.netty.util.concurrent.SingleThreadEventExecutor$4.run(SingleThreadEventExecutor.java:998)
	at io.netty.util.internal.ThreadExecutorMap$2.run(ThreadExecutorMap.java:74)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1144)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:642)
	at com.twitter.finagle.util.BlockingTimeTrackingThreadFactory$$anon$1.run(BlockingTimeTrackingThreadFactory.scala:23)
	at io.netty.util.concurrent.FastThreadLocalRunnable.run(FastThreadLocalRunnable.java:30)
	... 1 common frames omitted
14/04/2026 09:12:02,202 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,202 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [MERGE INTO DD_NOTIFICATION_STATUS dst USING (SELECT ? AS DD_UUID, ? AS FILE_ID FROM dual) src ON (dst.DD_UUID = src.DD_UUID AND dst.FILE_ID = src.FILE_ID) WHEN MATCHED THEN     UPDATE SET         dst.STATUS = (CASE WHEN EXISTS (             SELECT 1 FROM DD_API_STATUS_TBL ap             WHERE ap.DD_UUID = src.DD_UUID               AND ap.FILE_ID = src.FILE_ID               AND ap.RESPONSE_STATUS_CODE >= 400         ) THEN 'FAILED' ELSE 'SUCCESS' END),         dst.UPDATED_TS = SYSTIMESTAMP,         dst.UPDATED_BY = 'DD_USER' WHEN NOT MATCHED THEN     INSERT (DD_UUID, FILE_ID, STATUS, CREATED_TS, CREATED_BY)     VALUES (         src.DD_UUID,         src.FILE_ID,         (CASE WHEN EXISTS (             SELECT 1 FROM DD_API_STATUS_TBL ap             WHERE ap.DD_UUID = src.DD_UUID               AND ap.FILE_ID = src.FILE_ID               AND ap.RESPONSE_STATUS_CODE >= 400         ) THEN 'FAILED' ELSE 'SUCCESS' END),         SYSTIMESTAMP,         'DD_USER'     )]
14/04/2026 09:12:02,223 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.dao.ApiTransactionLogDAO || updateNotificationStatusByUuid || MERGE completed for DD_UUID=814753a1-ed9c-48a1-97eb-71bdc716eda0, FILE_ID=FILE_1776150720006_a48fcce7, rows=1
14/04/2026 09:12:02,223 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.a.service.OrganisationService || processOrganisation || Data_Distributor_Coface_ORG Updated notification status for dd_uuid:814753a1-ed9c-48a1-97eb-71bdc716eda0 after organisation creation failure
14/04/2026 09:12:02,224 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || processOrganisation || Data_Distributor_Coface_LE Successfully Created organisation for uuid:814753a1-ed9c-48a1-97eb-71bdc716eda0
14/04/2026 09:12:02,224 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.b.t.OrganisationSearchApiTasklet || execute || Data_Distributor_Coface_ORG: Processing complete. Total=1, Success=1, Failed=0
14/04/2026 09:12:02,224 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Participating in existing transaction
14/04/2026 09:12:02,224 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,224 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE STEP_EXECUTION_ID = ?
]
14/04/2026 09:12:02,226 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || handleExistingTransaction || Participating in existing transaction
14/04/2026 09:12:02,226 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,226 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION
SET START_TIME = ?, END_TIME = ?, STATUS = ?, COMMIT_COUNT = ?, READ_COUNT = ?, FILTER_COUNT = ?, WRITE_COUNT = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, READ_SKIP_COUNT = ?, PROCESS_SKIP_COUNT = ?, WRITE_SKIP_COUNT = ?, ROLLBACK_COUNT = ?, LAST_UPDATED = ?
WHERE STEP_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:02,227 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:02,228 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:02,229 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,229 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1493036889 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:02,229 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1493036889 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:02,230 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || o.s.batch.core.step.AbstractStep || execute || Step: [organisationSearchApiTaskletStep] executed in 557ms
14/04/2026 09:12:02,230 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.updateExecutionContext]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:02,230 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1297626264 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:02,230 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1297626264 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:02,230 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,231 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE STEP_EXECUTION_ID = ?
]
14/04/2026 09:12:02,232 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,232 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1297626264 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:02,233 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1297626264 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:02,233 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.update]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:02,234 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1491548956 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:02,234 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1491548956 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:02,234 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,235 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_STEP_EXECUTION
SET START_TIME = ?, END_TIME = ?, STATUS = ?, COMMIT_COUNT = ?, READ_COUNT = ?, FILTER_COUNT = ?, WRITE_COUNT = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, READ_SKIP_COUNT = ?, PROCESS_SKIP_COUNT = ?, WRITE_SKIP_COUNT = ?, ROLLBACK_COUNT = ?, LAST_UPDATED = ?
WHERE STEP_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:02,237 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:02,237 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:02,238 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,239 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1491548956 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:02,239 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1491548956 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:02,240 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.updateExecutionContext]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:02,240 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1150306702 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:02,240 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1150306702 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:02,240 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,240 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_JOB_EXECUTION_CONTEXT
SET SHORT_CONTEXT = ?, SERIALIZED_CONTEXT = ?
WHERE JOB_EXECUTION_ID = ?
]
14/04/2026 09:12:02,242 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,242 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1150306702 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:02,242 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1150306702 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:02,244 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || getTransaction || Creating new transaction with name [org.springframework.batch.core.repository.support.SimpleJobRepository.update]: PROPAGATION_REQUIRED,ISOLATION_DEFAULT
14/04/2026 09:12:02,244 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Acquired Connection [HikariProxyConnection@1490537710 wrapping oracle.jdbc.driver.T4CConnection@31723307] for JDBC transaction
14/04/2026 09:12:02,244 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doBegin || Switching JDBC Connection [HikariProxyConnection@1490537710 wrapping oracle.jdbc.driver.T4CConnection@31723307] to manual commit
14/04/2026 09:12:02,245 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:02,245 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT VERSION
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID=?
]
14/04/2026 09:12:02,245 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || query || Executing prepared SQL query
14/04/2026 09:12:02,246 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [SELECT COUNT(*)
FROM BATCH_JOB_EXECUTION
WHERE JOB_EXECUTION_ID = ?
]
14/04/2026 09:12:02,246 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,246 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE BATCH_JOB_EXECUTION
SET START_TIME = ?, END_TIME = ?,  STATUS = ?, EXIT_CODE = ?, EXIT_MESSAGE = ?, VERSION = VERSION + 1, CREATE_TIME = ?, LAST_UPDATED = ?
WHERE JOB_EXECUTION_ID = ? AND VERSION = ?
]
14/04/2026 09:12:02,247 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || processCommit || Initiating transaction commit
14/04/2026 09:12:02,248 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCommit || Committing JDBC transaction on Connection [HikariProxyConnection@1490537710 wrapping oracle.jdbc.driver.T4CConnection@31723307]
14/04/2026 09:12:02,248 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.j.support.JdbcTransactionManager || doCleanupAfterCompletion || Releasing JDBC Connection [HikariProxyConnection@1490537710 wrapping oracle.jdbc.driver.T4CConnection@31723307] after transaction
14/04/2026 09:12:02,250 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || o.s.b.c.l.s.TaskExecutorJobLauncher || run || Job: [SimpleJob: [name=LegalEntityEnrichmentJob]] completed with the following parameters: [{'leChildFileId':'{value=FILE_1776150720966_04b50af6, type=class java.lang.String, identifying=true}','leChildFileName':'{value=CofaceLEChild.csv, type=class java.lang.String, identifying=true}','leParentFileId':'{value=FILE_1776150720006_a48fcce7, type=class java.lang.String, identifying=true}','leParentFileName':'{value=cofaceLEParent.csv, type=class java.lang.String, identifying=true}','run.id':'{value=1776150720979, type=class java.lang.Long, identifying=true}'}] and the following status: [COMPLETED] in 1s124ms
14/04/2026 09:12:02,251 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch completed - PARENT fileSize: 0 B, CHILD fileSize: 0 B, totalRecords: 1, processedRecords: 1, failedRecords: 0
14/04/2026 09:12:02,253 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,253 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE DD_FILE_INGESTION_TBL SET PROCESSED_RECORDS = NVL(?, PROCESSED_RECORDS),     FAILED_RECORDS = NVL(?, FAILED_RECORDS),     SKIPPED_RECORDS = NVL(?, SKIPPED_RECORDS),     UPDATED_BY = 'DD_SYSTEM', UPDATED_TS = SYSTIMESTAMP WHERE FILE_ID = ?]
14/04/2026 09:12:02,254 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.datasource.DataSourceUtils || doGetConnection || Fetching JDBC Connection from DataSource
14/04/2026 09:12:02,255 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.service.FileIngestionService || updateFileProcessingMetrics || File Ingestion Service: Updated processing metrics - fileId: FILE_1776150720006_a48fcce7, processed: 1, failed: 0, skipped: 0
14/04/2026 09:12:02,255 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch completed - Child fileSize: 0 B, CHILD fileSize: 0 B, totalRecords: 4, processedRecords: 1, failedRecords: 0
14/04/2026 09:12:02,255 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,255 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE DD_FILE_INGESTION_TBL SET PROCESSED_RECORDS = NVL(?, PROCESSED_RECORDS),     FAILED_RECORDS = NVL(?, FAILED_RECORDS),     SKIPPED_RECORDS = NVL(?, SKIPPED_RECORDS),     UPDATED_BY = 'DD_SYSTEM', UPDATED_TS = SYSTIMESTAMP WHERE FILE_ID = ?]
14/04/2026 09:12:02,255 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.datasource.DataSourceUtils || doGetConnection || Fetching JDBC Connection from DataSource
14/04/2026 09:12:02,256 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.service.FileIngestionService || updateFileProcessingMetrics || File Ingestion Service: Updated processing metrics - fileId: FILE_1776150720966_04b50af6, processed: 1, failed: 0, skipped: 3
14/04/2026 09:12:02,257 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || update || Executing prepared SQL update
14/04/2026 09:12:02,257 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.JdbcTemplate || execute || Executing prepared SQL statement [UPDATE DD_FILE_INGESTION_TBL SET PROCESSING_END_TS = SYSTIMESTAMP,     FILE_SIZE = NVL(?, FILE_SIZE),     TOTAL_RECORDS = NVL(?, TOTAL_RECORDS),     PROCESSED_RECORDS = NVL(?, PROCESSED_RECORDS),     FAILED_RECORDS = NVL(?, FAILED_RECORDS),     STATUS = CASE         WHEN NVL(FAILED_RECORDS,0) > 0 THEN 'FAILED'         WHEN NVL(PROCESSED_RECORDS,0) = 0 AND NVL(SKIPPED_RECORDS,0) > 0 THEN 'PARTIALLY_COMPLETED'         WHEN NVL(PROCESSED_RECORDS,0) > 0 AND NVL(SKIPPED_RECORDS,0) > 0 THEN 'PARTIALLY_COMPLETED'         ELSE 'COMPLETED'     END,     UPDATED_BY = 'DD_SYSTEM', UPDATED_TS = SYSTIMESTAMP WHERE FILE_ID = ?]
14/04/2026 09:12:02,257 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.datasource.DataSourceUtils || doGetConnection || Fetching JDBC Connection from DataSource
14/04/2026 09:12:02,274 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.StatementCreatorUtils || setNull || JDBC getParameterType call failed - using fallback method instead: java.sql.SQLFeatureNotSupportedException: ORA-17023: Unsupported feature: Could not determine type
https://docs.oracle.com/error-help/db/ora-17023/
14/04/2026 09:12:02,275 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.StatementCreatorUtils || setNull || JDBC getParameterType call failed - using fallback method instead: java.sql.SQLFeatureNotSupportedException: ORA-17023: Unsupported feature: Could not determine type
https://docs.oracle.com/error-help/db/ora-17023/
14/04/2026 09:12:02,275 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.s.jdbc.core.StatementCreatorUtils || setNull || JDBC getParameterType call failed - using fallback method instead: java.sql.SQLFeatureNotSupportedException: ORA-17023: Unsupported feature: Could not determine type
https://docs.oracle.com/error-help/db/ora-17023/
14/04/2026 09:12:02,276 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.service.FileIngestionService || updateFileProcessingEnd || File Ingestion Service: Updated processing end - fileId: FILE_1776150720966_04b50af6, fileSize: 0, totalRecords: [UNCHANGED], processedRecords: null, failedRecords: null
14/04/2026 09:12:02,277 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular finished name:LegalEntityEnrichmentJob status:COMPLETED
14/04/2026 09:12:24,093 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.a.h.i.c.PoolingHttpClientConnectionManager || closeIdleConnections || Closing connections idle longer than 60000 MILLISECONDS
14/04/2026 09:13:00,000 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular started:2026-04-14T09:13:00.000539524
14/04/2026 09:13:00,003 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular flag stopped
14/04/2026 09:13:24,096 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.a.h.i.c.PoolingHttpClientConnectionManager || closeIdleConnections || Closing connections idle longer than 60000 MILLISECONDS
14/04/2026 09:14:00,000 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular started:2026-04-14T09:14:00.000482789
14/04/2026 09:14:00,002 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch still running, skipping this run :2026-04-14T09:14:00.002182489
14/04/2026 09:14:24,097 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.a.h.i.c.PoolingHttpClientConnectionManager || closeIdleConnections || Closing connections idle longer than 60000 MILLISECONDS
14/04/2026 09:15:00,000 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular started:2026-04-14T09:15:00.000337313
14/04/2026 09:15:00,001 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch still running, skipping this run :2026-04-14T09:15:00.001423257
14/04/2026 09:15:01,785 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe Spring-Context-Initialized succeeded
14/04/2026 09:15:01,785 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe AED-Discovery succeeded
14/04/2026 09:15:01,785 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe AccessToken-JWKS succeeded
14/04/2026 09:15:01,786 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe Peertoken-JWKS succeeded
14/04/2026 09:15:01,786 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe WarmupExecutingProbe succeeded
14/04/2026 09:15:24,097 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.a.h.i.c.PoolingHttpClientConnectionManager || closeIdleConnections || Closing connections idle longer than 60000 MILLISECONDS
14/04/2026 09:16:00,000 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch Schedular started:2026-04-14T09:16:00.000265225
14/04/2026 09:16:00,000 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || INFO  || c.i.d.batch.schedular.BatchSchedular || runLE || LegalEntity Batch still running, skipping this run :2026-04-14T09:16:00.000704023
14/04/2026 09:16:01,781 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe Spring-Context-Initialized succeeded
14/04/2026 09:16:01,782 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe AED-Discovery succeeded
14/04/2026 09:16:01,782 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe AccessToken-JWKS succeeded
14/04/2026 09:16:01,782 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe Peertoken-JWKS succeeded
14/04/2026 09:16:01,782 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || c.i.a.m.a.probe.ProbeRegistry || evaluateProbeState || ReadinessProbe WarmupExecutingProbe succeeded
14/04/2026 09:16:24,099 || datadistributorapiservice26266696-7d6f8bc6d-vvg2n || DataDistributorAPIService || DEBUG || o.a.h.i.c.PoolingHttpClientConnectionManager || closeIdleConnections || Closing connections idle longer than 60000 MILLISECONDS
