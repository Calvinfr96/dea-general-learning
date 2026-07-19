# AWS DMS Interview Questions

## Basic Questions
1. What is AWS DMS?
    - Answer: AWS Database Migration Service (DMS) is a cloud service that helps you migrate databases to AWS easily and securely. It supports migrations from various database sources to AWS database services, including Amazon RDS, Amazon Aurora, and Amazon Redshift.

1. What types of migrations does AWS DMS support?
    - Answer: AWS DMS supports homogenous migrations (same database engine) and heterogeneous migrations (different database engines).

1. What are the main components of AWS DMS?
    - Answer: The main components include:
        - Replication Instances: The compute resources that run the migration tasks.
        - Endpoints: Source and target database endpoints that define the databases involved in migration.
        - Migration Tasks: The tasks that define what data to migrate.

1. What types of source databases can AWS DMS connect to?
    - Answer: AWS DMS can connect to various source databases, including MySQL, PostgreSQL, Oracle, SQL Server, MongoDB, Amazon S3, and many more.

1. What are replication tasks in AWS DMS?
    - Answer: Replication tasks define the data migration process, including the source and target endpoints, migration type (full load, CDC, or both), and other settings like transformation rules.

1. What is the difference between full load and change data capture (CDC) in AWS DMS?
    - Answer: A full load migration transfers all data from the source database to the target database, while CDC continuously captures and replicates changes made to the source database after the initial load.

1. What is the purpose of the AWS DMS replication instance?
    - Answer: The replication instance performs the actual migration tasks, processes the data, and manages connections between source and target databases.

1. Can AWS DMS perform ongoing replication?
    - Answer: Yes, AWS DMS can perform ongoing replication by using CDC to capture changes continuously after the initial data load.

1. What is a transformation rule in AWS DMS?
    - Answer: A transformation rule allows you to modify data during migration, such as changing data types, renaming tables or columns, or filtering rows.

1. How does AWS DMS handle schema conversion?
    - Answer: AWS DMS provides the AWS Schema Conversion Tool (SCT) to assist with converting the database schema from the source database to the target database.

1. What is the minimum requirement for a replication instance?
    - Answer: The minimum requirement for a replication instance is at least 1 vCPU and 2 GB of RAM, but this may vary based on the expected load and size of the database.

1. How do you create endpoints in AWS DMS?
    - Answer: Endpoints are created by specifying the source or target database type, providing the connection details (such as server name, port, username, password), and testing the connection.

1. How can you monitor the performance of AWS DMS?
    - Answer: You can monitor DMS performance using Amazon CloudWatch metrics, AWS DMS console, and by checking the logs of replication tasks.

1. What metrics should you monitor for AWS DMS replication tasks?
    - Answer: Key metrics include:
        - Replication lag
        - Change data capture (CDC) lag
        - Throughput (records per second)
        - Error counts

1. What is the significance of replication lag in AWS DMS?
    - Answer: Replication lag indicates the time it takes for changes in the source database to be reflected in the target database, helping assess the efficiency of the migration process.

1. How can you optimize data migration performance in AWS DMS?
    - Answer: Performance can be optimized by selecting the right instance size, increasing the number of replication tasks, enabling multi-AZ deployments, and using parallel processing.

1. What are best practices for AWS DMS migration?
    - Answer: Best practices include:
        - Assessing source and target compatibility
        - Using the AWS Schema Conversion Tool (SCT)
        - Testing migrations in a development environment
        - Ensuring adequate network bandwidth

1. What common issues might arise during AWS DMS migrations?
    - Answer: Common issues include connectivity problems, insufficient permissions, schema mismatches, data type incompatibilities, and network latency.

1. What does the status 'Creating' mean for a DMS replication task?
    - Answer: The 'Creating' status indicates that the task is being initialized and the required resources are being provisioned.

1. What does the 'Stopped' status mean for a DMS replication task?
    - Answer: The 'Stopped' status indicates that the replication task has been manually stopped or has encountered an error that requires attention.

1. How can you handle data type conversion errors in AWS DMS?
    - Answer: Data type conversion errors can be handled by adjusting transformation rules, using the Schema Conversion Tool (SCT) to identify and resolve issues, or modifying the target schema.

1. How does AWS DMS ensure data encryption during migration?
    - Answer: AWS DMS supports TLS for data in transit and allows enabling encryption for data at rest in the target database.

1. What IAM policies are required for AWS DMS?
    - Answer: IAM policies must allow actions like `dms:CreateReplicationInstance`, `dms:CreateEndpoint`, `dms:CreateReplicationTask`, and permissions to access source and target databases.

1. How can you set up a secure connection for AWS DMS?
    - Answer: Secure connections can be set up by using SSL/TLS for database endpoints, configuring security groups to limit access, and applying IAM roles for authentication.

1. What is AWS DMS CDC?
    - Answer: Change Data Capture (CDC) allows AWS DMS to capture and replicate ongoing changes in the source database after the initial full load has completed.

1. Can AWS DMS perform data validation during migration?
    - Answer: Yes, AWS DMS can perform data validation to ensure that the data in the source and target databases are consistent after migration.

1. What is the AWS DMS console?
    - Answer: The AWS DMS console is the web-based user interface for creating and managing DMS resources, monitoring migration tasks, and viewing logs and metrics.

1. How is AWS DMS priced?
    - Answer: AWS DMS pricing is based on the instance size of the replication instance, the amount of data transferred, and the number of replication tasks running.

1. What factors can affect the cost of using AWS DMS?
    - Answer: Factors include the size of the replication instance, the duration of the migration, the volume of data migrated, and whether additional features like CDC are utilized.

1. Can you estimate the cost of an AWS DMS migration project?
    - Answer: Cost estimation can be done by calculating the expected duration of the migration, the instance size needed, and any data transfer charges involved.

1. What are some cost-saving strategies when using AWS DMS?
    - Answer: Cost-saving strategies include selecting the appropriate instance size, using multi-AZ deployments only when necessary, and optimizing data transfer rates.

1. How can you optimize the cost of AWS DMS when migrating large datasets?
    - Answer: Optimizing costs can involve breaking large migrations into smaller tasks, utilizing parallel tasks, and reducing the amount of data transferred by filtering unnecessary data.

1. What encryption options does AWS DMS support?
    - Answer: AWS DMS supports SSL/TLS for data in transit and enables server-side encryption for data at rest in the target database.

1. Can AWS DMS comply with data protection regulations?
    - Answer: Yes, AWS DMS can be configured to meet data protection regulations by implementing encryption, access controls, and auditing mechanisms.

1. How can you secure the replication instance in AWS DMS?
    - Answer: Security can be enhanced by assigning appropriate IAM roles, using security groups to restrict access, and deploying the instance in a private subnet.

1. How does AWS DMS handle sensitive data?
    - Answer: Sensitive data can be managed using encryption, access controls, and data masking techniques to protect data during migration.

1. What is the importance of logging in AWS DMS?
    - Answer: Logging is vital for auditing, monitoring performance, diagnosing issues, and ensuring compliance with regulatory requirements.

1. How can AWS DMS assist in disaster recovery scenarios?
    - Answer: AWS DMS can facilitate disaster recovery by replicating data to a standby database, ensuring minimal downtime and data loss.

1. What are some examples of heterogeneous database migrations?
    - Answer: Examples include migrating from Oracle to Amazon Aurora, SQL Server to PostgreSQL, or MongoDB to Amazon DynamoDB.

1. How can you integrate AWS DMS with a microservices architecture?
    - Answer: AWS DMS can feed data into various microservices, enabling real-time updates and ensuring data consistency across services.

1. What role does AWS DMS play in data lake architectures?
    - Answer: AWS DMS can move data from multiple sources into data lakes, such as Amazon S3, enabling analytics and machine learning applications.

1. What is the blue/green migration strategy with AWS DMS?
    - Answer: The blue/green migration strategy involves running two identical environments, allowing a seamless switch from the old to the new system after successful migration.

1. How do you perform a phased migration using AWS DMS?
    - Answer: Phased migration can be accomplished by breaking the migration into smaller, manageable tasks, migrating less critical data first, and progressively moving more critical datasets.

## Scenario-Based Questions
1. What is the difference between a 'Full Load' and 'CDC' task? When would you use one over the other?
    - The Answer: They represent the two phases of migration.
    - Full Load: This is a one-time snapshot. DMS reads all existing rows from the source and inserts them into the target. It's like copying a file.
    - CDC (Change Data Capture): This is ongoing replication. DMS reads the Transaction Logs (Binlog, WAL, Redo Log) of the source database to capture `INSERT`, `UPDATE`, and `DELETE` events as they happen and applies them to the target.
    - Usage: For a production migration with minimal downtime, we use 'Full Load + CDC'. We let the Full Load finish, then let CDC catch up on changes that happened during the load, keep the systems in sync, and then cut over.

 
1. You started a migration task, but it failed immediately with a 'Schema Missing' error. Does DMS not create the schema for you?
    - The Answer: No, DMS is not a Schema Migration tool; it is a Data Migration tool.
    - The Limitation: DMS can create basic tables (if you enable 'Create tables on target'), but it does not migrate complex objects like Secondary Indexes, Foreign Keys, Stored Procedures, or Views.
    - The Fix: We must use the AWS Schema Conversion Tool (SCT) or native tools (like pg_dump or SSMS) to migrate the schema DDL to the target before starting the DMS task.

 
1. We are migrating to Redshift. Why do we need an S3 bucket in the middle?
    - The Answer: This is an architectural requirement for DMS when Redshift is the target.
    - The Mechanism: DMS does not write INSERT statements directly to Redshift (which is slow for single rows).
    - The Flow:
        1. DMS writes data to an Intermediate S3 Bucket as CSV files.
        1. DMS triggers the Redshift COPY command to bulk-load those CSVs into the Redshift cluster.
        1. Performance: This is significantly faster than row-by-row inserts.

1. Your migration is failing on a table that has a 'Description' column containing large text (2MB per row). The error mentions 'LOB truncation'. What is happening?
    - The Answer: This is the Large Object (LOB) Mode setting.
    - Limited LOB Mode (Default): DMS is fast but assumes LOBs are small (e.g., < 32KB). If a row exceeds this limit, DMS truncates the data (cuts it off) and might flag a warning or error.
    - Full LOB Mode: DMS migrates the entire LOB, no matter the size. However, it is extremely slow because it fetches LOBs one by one via a separate lookup.
    - The Fix: We use 'Limited LOB Mode' but increase the Max LOB Size to slightly larger than the largest LOB in our DB (e.g., 5MB). This gives us speed without truncation.

1. The business requires 100% confidence that the data in AWS matches the On-Prem DB. How do you prove this without writing manual SQL scripts?
    - The Answer: I would enable DMS Data Validation.
    - The Feature: It is a setting in the DMS Task.
    - How it works:
        1. After migrating a batch of records, DMS issues a query to both Source and Target.
        1. It calculates a checksum/hash of the data on both sides.
        1. If they match, it marks the table as Validated. If not, it records the mismatch in a awsdms_validation_failures table on the target.
    - Performance Impact: Note that this slows down the migration significantly, so we usually **only enable it for critical tables**.

 
1. Your CDC replication was running fine, but suddenly the latency spiked to 4 hours. The Source DB is an Oracle system doing a massive 'End of Month' batch update. Why is DMS lagging?
    - The Answer: DMS is single-threaded by default when applying changes to the target.
    - The Bottleneck: The Source (Oracle) might be processing 50,000 transactions/sec using parallel threads. The DMS Target applicator is trying to replay those transactions serially. It can't keep up.
    - The Fix: Enable Parallel Apply (Batch Apply) on the target endpoint.
    - This tells DMS to group transaction batches and apply them using multiple threads on the target database, drastically increasing throughput.

 
1. You are migrating a 10TB database. The Full Load takes 3 weeks. By the time it finishes, the CDC logs (WAL/Binlogs) from 3 weeks ago have rotated off the source server. The task fails. How do you fix this?
    - The Answer: This is a storage retention issue on the Source.
    - The Cause: CDC requires the logs to be available from the start of the Full Load. If the Full Load takes longer than the log retention period (e.g., 24 hours), DMS cannot find the old logs to resume sync.
    - The Fix:
        - Increase Retention: Temporarily increase log retention on the Source DB to cover the full load duration.
        - Parallel Load: Speed up the Full Load by using Parallel Load (splitting the large table into ranges using a filter-segment rule) to finish in 2 days instead of 3 weeks.

 
1. We noticed that DMS is causing performance issues on our Production Primary Database (Source) during the Full Load. The DBA is angry. How do we mitigate this?
    - The Answer: We should shift the load to a Read Replica or Standby.
    - Strategy:
        1. Instead of pointing DMS to the Primary Writer, point it to a Read Replica (e.g., RDS Read Replica or Oracle Active Data Guard).
        1. CDC Impact: Note that for CDC, DMS usually still needs access to the transaction logs, which are generated on the primary, but fetching the Full Load data (SELECT *) from the replica saves the Primary's CPU.
    - Alternative: Use the safeguard setting in DMS to pause the task if the Source CPU exceeds 80%.

1. The migration failed with Foreign Key Violation errors during the Full Load. I thought you said DMS doesn't migrate Foreign Keys?
    - The Answer: Correct, DMS doesn't create FKs, but if you created them on the Target beforehand (using schema export), they are active.
    - The Conflict: DMS loads tables in parallel (alphabetical or random order). It might load the Orders table before the Customers table.
    - The Error: Inserting an Order fails because the Customer ID doesn't exist yet on the target.
    - The Fix:
        1. Disable FKs: Drop or disable Foreign Keys on the target database during the Full Load.
        1. Re-enable: Re-enable them only after the Full Load is complete and before Cut-over.

 
1. You used DMS to migrate from Oracle to Postgres. Did you use DMS to migrate the schema (tables/indexes) as well?
    - The Answer: No, I did not. DMS is not a Schema Migration tool; it is a Data Migration tool.
    - The Reason: DMS creates basic tables if they don't exist, but it does not migrate Secondary Indexes, Foreign Keys, Stored Procedures, or Triggers.
    - The Process: I used the AWS Schema Conversion Tool (SCT) first to convert the DDL (schema) from Oracle to Postgres. I applied that schema to the target, then I started the DMS task to move the data.

1. What is the difference between 'Full Load' and 'CDC', and how do they work together?
    - The Answer: They are the two phases of a migration:
    - Full Load: A one-time bulk copy of existing data. It's like a SELECT * from Source and INSERT to Target.
    - CDC (Change Data Capture): Ongoing replication. DMS reads the source's Transaction Logs (WAL for Postgres, Redo Logs for Oracle, Binlog for MySQL) to capture changes that happen after the Full Load started.
    - Combined: In production, we almost always use 'Full Load + CDC'. This minimizes downtime by letting the Full Load finish while CDC catches up on the delta, allowing for a seamless cut-over.

1. Your migration failed immediately with a 'Primary Key Violation' on the target. You checked the source, and there are no duplicates. What happened?
    - The Answer: This usually happens if the Full Load was restarted but the Target wasn't cleaned.
    - The Scenario: I ran a Full Load. It failed halfway. I restarted the task.
    - The Error: If the 'Target Table Preparation Mode' is set to 'Do nothing', DMS tries to insert rows that were already migrated in the first failed run, causing PK collisions.
    - The Fix: Change the setting to 'Drop tables on target' (for a fresh start) or 'Truncate' before restarting the Full Load.

1. You are migrating from Oracle to PostgreSQL. The migration fails because of a 'Numeric Overflow' error. The data fits in Oracle. Why does it fail in Postgres?
    - The Answer: This is a classic Data Type Mismatch in heterogeneous migrations.
    - The Cause: Oracle's NUMBER type is very flexible. Postgres is stricter.
    - Oracle might have NUMBER without precision, holding a huge value.
    - DMS maps this to a Postgres NUMERIC or DOUBLE with a specific precision that might be too small.
    - The Fix: I would use a Transformation Rule in the DMS Table Mapping. I can explicitly change the data type for that specific column to a larger type (e.g., STRING) during migration to ensure it fits, or fix the schema in the SCT tool before migration.

 
1. We are migrating a massive table (500 million rows). The Full Load takes too long (3 days). If we restart, we lose 3 days. How do we make this faster and resilient?
    - The Answer: We should use Parallel Load with Ranges.
    - The Strategy:
        1. Instead of one task reading the whole table, we set up Table Settings to split the table into logical segments (e.g., by Partition Key or ID ranges).
        1. DMS spins up multiple threads, each reading a chunk (e.g., ID 1-1M, ID 1M-2M) simultaneously.
    - Resilience: If one chunk fails, we only reload that specific range, not the whole table.

## Error-Based Questions
1. You set up a DMS task to move data from an on-premise Oracle DB to AWS RDS. The 'Test Connection' fails immediately. You checked the username/password and they are correct. What is the most common networking mistake?
    - The Answer: It is almost always a Security Group or Firewall issue.
    - The Check:
        - Replication Instance SG: Does the DMS Replication Instance have an outbound rule allowing traffic to the Oracle IP on port 1521?
        - Source Firewall: Does the corporate firewall allow inbound traffic from the private IP of the DMS Replication Instance?
        - The error: Often, people whitelist their own laptop IP but forget to whitelist the DMS Instance's IP.
    - The fix: Add the DMS Security Group ID to the allowed list on the database side.

 

1. Your migration task status says 'Running with errors'. You check the 'Table Statistics' tab, and one table shows 'Error'. How do you find out why it failed?
    - The Answer: The console status just says 'Error', which is useless. We must check the CloudWatch Logs.
    - The Workflow:
        1. Click on the 'View CloudWatch logs' link for the task.
        1. Search for the table name or the keyword `]E`: (which stands for Error in DMS logs).
        1. Common Findings: It might say ORA-00942: table or view does not exist (permissions) or invalid byte sequence (encoding issue). Without reading the raw log, we are guessing.

1. You are doing a Full Load. It fails halfway through with a 'Foreign Key Violation' error. Why does this happen if the data is valid on the source?
    - The Answer: DMS loads tables in Parallel (and unordered), not in dependency order.
    - The Scenario: You have Orders and Customers.
    - The Failure: DMS tries to insert an Order for 'Customer ID 500'. However, the Customers table hasn't finished loading yet. The database rejects the Order because 'Customer 500' doesn't exist yet.
        1. The Fix:
        1. Disable Foreign Keys on the target database before starting the migration.
        1. Run the Full Load.
        1. Re-enable Foreign Keys after the load is complete.

1. The business team complains that the data in AWS is 'cut off'. A Comments column that should have 5,000 characters only has exactly 32kb of text. What setting caused this?
    - The Answer: This is the default Limited LOB Mode.
    - The Logic: DMS tries to be fast. Large Objects (LOBs) like long text or JSON blobs slow it down. So, by default, DMS truncates any LOB larger than 32KB.
    - The Fix:
        1. Stop the task.
        1. Change the setting to Limited LOB Mode with a higher limit (e.g., 1024KB) if you know the max size.
        1. Or switch to Full LOB Mode (slower, but guarantees full data capture).
        1. Reload the affected tables.

1. We enabled 'Data Validation' to prove the migration worked. One table shows 'Mismatched Records'. How do we see which rows failed?
    - The Answer: DMS doesn't show the mismatched data in the console (for security). It writes it to a table in the target database.
    - The Location: Look for a table named `awsdms_control.awsdms_validation_failures_v1` on the target (e.g., Redshift or Aurora).
    - The content: This table contains the Primary Key of the bad row and the type of error (e.g., `RECORD_DIFF`).
    - The Action: I would query the source and target using that Primary Key to manually inspect the difference (often it's a timezone conversion issue or trailing whitespace).

1. Your CDC task is running. You see 'Target Latency' spiking to 1 hour. 'Source Latency' is 0. What does this tell you?
    - The Answer: This is a Target Bottleneck.
    - Diagnosis:
        1. Source Latency = 0: DMS is reading from the source perfectly fine.
        1. Target Latency = High: DMS has the data in memory but cannot write it to the Target fast enough.
        1. Common Causes: The Target database lacks Indexes (making updates slow), has no Primary Key, or is under-provisioned (CPU high).
    - The Fix: Enable Batch Apply in the DMS task settings. This groups thousands of updates into a single transaction, drastically speeding up writes to targets like Redshift or Postgres.

 

1. The CDC task failed with this error: `ERROR: replication slot dms_slot is active for PID 123`. You cannot restart the task. How do you recover?
    - The Answer: This is a classic PostgreSQL Zombie Slot issue.
    - The Context: When DMS connects to Postgres, it creates a 'Replication Slot' to read the WAL logs.
    - The Error: The task crashed, but the Postgres process holding the slot didn't die. Postgres thinks DMS is still connected, so it rejects the new DMS connection.
    - The Fix:
        1. Log into the Source Postgres DB.
        1. Run select * from pg_replication_slots;.
        1. Kill the zombie process using pg_terminate_backend(pid).
        1. Now restart the DMS task.

 

1. You are migrating a high-traffic Oracle database. The task crashes with 'Log sequence number not found'. What happened?
    - The Answer: The Source Database deleted the transaction logs before DMS could read them.
    - The Mechanism: DMS reads Archive Logs. If the database generates 50GB of logs per hour, but your retention policy deletes them after 30 minutes, and DMS pauses for 45 minutes... the log is gone.
    - The Result: DMS looks for Log 100, but the disk only has Log 102. It cannot resume.
    - The Fix:
        - Short Term: You must perform a full reload of the tables (painful).
        - Long Term: Increase the Archive Log Retention on the source Oracle server (e.g., keep logs for 24 hours).

1. The Replication Instance is running out of Memory (RAM) and swapping to disk, causing massive slowness. We are migrating 500 tables. Do we just buy a bigger instance?
    - The Answer: Not necessarily. We might be overloading the specific instance with too many Concurrent Tasks.
    - The Architecture: Each DMS Task consumes memory for buffers. If you run one giant task for 500 tables, or 50 tasks for 10 tables each, you fragment memory.
    - The Fix:
        - Split the workload: Move large, heavy tables to their own dedicated Task (and even their own Replication Instance).
        - Memory Limit: Check the MemoryLimitTotal setting in DMS. Ensure we aren't allocating buffers that exceed the physical RAM of the box.

1. You started a Full Load task with the setting 'Target Table Preparation Mode: Do Nothing'. The task failed immediately with a TableError. The logs say Table 'Users' already exists. Why did it fail instead of just appending the data?
    - The Answer: 'Do Nothing' assumes the target table structure matches the source exactly and is empty or ready for data.
    - The Error: If the existing table on the target has a Primary Key constraint and you try to load duplicate IDs from the source, the database rejects the insert, causing a task failure.
    - The Fix:
        - If you want a fresh start: Change mode to 'Drop tables on target'.
        - If you want to keep existing data: Ensure the source data doesn't violate PK constraints, or use 'Truncate' mode to clear data but keep the schema.

1. You are migrating to Amazon Redshift. The task fails during initialization with: `S3 Bucket creation failed` or `AccessDenied`. You didn't configure an S3 bucket in the settings; you just selected Redshift as the target. Why is it asking for S3?
    - The Answer: DMS requires an intermediate S3 bucket to load data into Redshift efficiently (using the COPY command).
    - The Mechanism: DMS writes files to S3 -> Redshift reads from S3.
    - The Error: DMS tries to automatically create a bucket named `dms-endpoint-<random-string>`. If the Service Role (dms-access-for-endpoint) lacks permission to `s3:CreateBucket` or `s3:PutObject`, the task fails.
    - The Fix: Either grant the DMS IAM Role full S3 permissions or pre-create a bucket yourself and specify it in the 'S3 Bucket Name' setting of the Redshift Endpoint.

1. Your CDC task for an Oracle source has been running fine for months. Suddenly, it fails with: ORA-01291: missing logfile or [SOURCE_CAPTURE] E: Sequence 12345 does not exist. You resume the task, but it fails again instantly.
    - The Answer: DMS lost track of the Redo Logs (Archived Logs) on the Oracle server.
    - The Cause: The task was paused (or latency spiked), and during that time, Oracle's internal maintenance scripts deleted the old Archived Logs from the disk to save space.
    - The Reality: DMS needs Log private channel to continue, but it's gone forever.
    - The Fix: You cannot simply 'Resume'. You must:
    - Resync: Perform a full reload of the affected tables.
    - Prevent Recurrence: Increase the Archive Log Retention period on the Oracle Source (e.g., from 24 hours to 3 days) to handle future DMS pauses.

1. You stopped a DMS task migrating from PostgreSQL 2 weeks ago. Today, the DBA calls you screaming that the Production Postgres Disk is Full. You check, and the disk is filled with `pg_wal` (Write Ahead Logs). How is a stopped DMS task causing disk usage on the source?
    - The Answer: DMS uses Logical Replication Slots on Postgres.
    - The Trap: When you stop a DMS task, the Replication Slot on the Source DB remains active by default.
    - The Impact: Postgres thinks, 'I must keep all WAL logs until this Slot confirms it has read them.' Since DMS is stopped, it never reads them. So Postgres keeps the logs forever, filling up the disk.
    - The Fix: Log into Postgres and manually drop the slot: `SELECT pg_drop_replication_slot('dms_slot_name');`.

1. You used a Transformation Rule to rename a schema from `SALES_PROD` to `SALES` on the target. The Full Load works. But CDC fails. New tables created in `SALES_PROD` on the source are not appearing in `SALES` on the target. Instead, DMS is creating a new schema SALES_PROD on the target.
    - The Answer: You likely hit the DDL Routing limitation.
    - The Logic: Transformation rules for renaming schemas often apply to the initial table mapping. However, for DDL events (like CREATE TABLE), DMS might miss the rename rule if not explicitly configured to handle DDL scoping.
    - The Fix: Ensure your Transformation Rule includes 'Rename Schema' scope for `%` (all tables) and check if the 'Source Filter' correctly captures the DDL. Often, it's safer to pre-create the table on the target or use the MapTo setting in the table mapping JSON manually.