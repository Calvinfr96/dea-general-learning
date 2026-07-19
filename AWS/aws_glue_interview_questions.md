# AWS Glue Interview Questions

## Basic Questions
1. What is AWS Glue?
    - Answer: AWS Glue is a fully managed extract, transform, and load (ETL) service that simplifies data preparation for analytics. It automates the process of discovering, cataloging, and transforming data.

1. What are the key components of AWS Glue?
    - Answer: The key components of AWS Glue include:
        - Data Catalog: A centralized repository to store metadata.
        - ETL Jobs: Scripts to extract, transform, and load data.
        - Crawlers: Services that automatically scan data sources and populate the Data Catalog.
        - Triggers: Events that start jobs based on schedules or other events.

1. How does AWS Glue Data Catalog work?
    - Answer: The Glue Data Catalog stores metadata for data assets, allowing users to define tables, partitions, and data types. It enables data discovery and schema management.

1. What is the purpose of a crawler in AWS Glue?
    - Answer: A crawler scans data sources, identifies data formats, and populates the Glue Data Catalog with metadata such as tables, schemas, and partitions.

1. What types of data sources can AWS Glue connect to?
    - Answer: AWS Glue can connect to various data sources, including Amazon S3, Amazon RDS, Amazon Redshift, Amazon DynamoDB, and other databases through JDBC.

1. What programming languages does AWS Glue support for writing ETL jobs?
    - Answer: AWS Glue supports ETL jobs written in Python and Scala. It also provides a visual interface for job creation through AWS Glue Studio.

1. What is a Glue job?
    - Answer: A Glue job is a script that performs the ETL process, extracting data from sources, transforming it as needed, and loading it into target destinations.

1. What are the different types of AWS Glue jobs?
    - Answer: There are two types of Glue jobs:
        - Spark Jobs: Distributed processing for large datasets.
        - Python Shell Jobs: For smaller workloads that don't require Spark.

1. How can you schedule AWS Glue jobs?
    - Answer: AWS Glue jobs can be scheduled using triggers. Triggers can be based on a schedule (cron-based) or based on events from other AWS services.

1. What is AWS Glue Studio?
    - Answer: AWS Glue Studio is a visual interface that simplifies the creation, monitoring, and management of AWS Glue ETL jobs, allowing users to design jobs using a drag-and-drop interface.

1. How can you handle schema evolution in AWS Glue?
    - Answer: Glue supports schema evolution by allowing users to update the schema in the Data Catalog. It can accommodate changes in data structure and manage different versions of the schema.

1. How do you convert a dynamic frame to a Spark DataFrame in AWS Glue?
    - Answer: You can convert a dynamic frame to a Spark DataFrame using the `toDF()` method, like so:
`dataframe = dynamic_frame.toDF()`.

1. What are Glue bookmarks, and how do they help in ETL processes?
    - Answer: Glue bookmarks keep track of processed data in previous job runs, allowing you to load only new or changed data in subsequent runs, thus optimizing ETL workflows.

1. Can you perform data validation in AWS Glue?
    - Answer: Yes, you can perform data validation using custom Python or PySpark code within your Glue jobs to check data quality and integrity before processing.

1. What is the purpose of the Glue ETL library?
    - Answer: The Glue ETL library provides pre-defined functions and utilities to simplify common ETL tasks, such as transforming data, loading it into data stores, and logging.

1. How do you handle errors in AWS Glue jobs?
    - Answer: Errors in AWS Glue jobs can be handled using error handling constructs in the code, logging mechanisms, and retry configurations in job definitions.

1. What is a Glue DataBrew?
    - Answer: AWS Glue DataBrew is a visual data preparation tool that allows users to clean and transform data without writing code, providing a user-friendly interface for data analysts and data scientists.

1. What is partitioning in AWS Glue, and why is it important?
    - Answer: Partitioning is the process of dividing large datasets into smaller, manageable pieces based on specific keys (e.g., date). It improves query performance and reduces costs by allowing queries to only scan relevant partitions.

1. How does AWS Glue support data lakes?
    - Answer: AWS Glue helps manage data lakes by providing a unified Data Catalog, enabling data discovery, ETL processes, and schema management for diverse data sources.

1. What is the role of AWS Glue in data migration scenarios?
    - Answer: AWS Glue can facilitate data migration by extracting data from legacy systems, transforming it to match the target schema, and loading it into new systems or databases.

1. How does AWS Glue handle connections to databases?
    - Answer: AWS Glue uses connection definitions to connect to databases, specifying parameters such as connection strings, JDBC URLs, and authentication credentials stored securely in AWS Secrets Manager.

1. How do you control access to AWS Glue resources?
    - Answer: Access to AWS Glue resources is controlled using AWS IAM policies. You can grant or deny permissions to users, roles, or services for Glue jobs, crawlers, and Data Catalog.

1. How can you secure data in AWS Glue?
    - Answer: You can secure data in AWS Glue by using IAM roles for authentication, encrypting data at rest and in transit, and restricting access through fine-grained IAM policies.

1. What is a Glue Connection, and how is it secured?
    - Answer: A Glue Connection defines the properties needed to connect to a data store (e.g., database credentials). It can be secured using AWS Secrets Manager to store sensitive information like usernames and passwords.

1. How do you audit AWS Glue activities?
    - Answer: AWS Glue activities can be audited using AWS CloudTrail, which logs API calls made to Glue, allowing you to track changes and access patterns.

1. What encryption options are available in AWS Glue?
    - Answer: AWS Glue supports encryption at rest using AWS KMS keys and encryption in transit using TLS for data moving between AWS Glue and data stores.

1. How can you manage sensitive data in AWS Glue jobs?
    - Answer: Sensitive data can be managed by using AWS Secrets Manager for credentials, enabling encryption for data at rest, and restricting access using IAM policies.

1. How can you monitor AWS Glue jobs?
    - Answer: AWS Glue jobs can be monitored using AWS CloudWatch, which provides logs, metrics, and alarms for job executions, allowing you to track performance and identify issues.

1. How do you debug AWS Glue jobs?
    - Answer: Debugging can be done by reviewing CloudWatch Logs generated by Glue jobs, checking for error messages, and using print statements within the ETL scripts for additional logging.

1. What are some best practices for optimizing AWS Glue job performance?
    - Answer: Best practices include:
        - Utilizing partitioning to reduce data scans.
        - Configuring appropriate worker types and DPU allocation.
        - Writing efficient ETL scripts.
        - Using AWS Glue DynamicFrames for handling data transformations.

1. What is the maximum number of DPUs you can allocate for an AWS Glue job?
    - Answer: As of now, the maximum number of DPUs you can allocate for a single Glue job is 100 DPUs for Spark jobs. The limits can vary, so it’s advisable to check the latest AWS documentation.

1. What is a Glue job bookmark, and how does it work?
    - Answer: A Glue job bookmark keeps track of the last processed data, allowing subsequent job runs to only process new or changed data, enhancing efficiency in ETL workflows.

1. What is a Glue Workflow?
    - Answer: A Glue Workflow is a way to manage and orchestrate multiple Glue jobs and crawlers, allowing you to define dependencies and the order in which they should run.

1. How do you manage data lineage in AWS Glue?
    - Answer: Data lineage can be managed by tracking job runs, transformations, and data sources in the Glue Data Catalog, allowing users to see the flow of data through various ETL processes.

1. What is the Glue API, and how can it be used?
    - Answer: The Glue API provides programmatic access to AWS Glue features, allowing developers to create, manage, and monitor Glue resources through SDKs or AWS CLI.

1. What is the importance of using Glue versioning?
    - Answer: Glue versioning allows users to manage different versions of Glue ETL jobs, ensuring that changes can be rolled back if needed and maintaining stability in production environments.

1. How do you implement version control for Glue ETL scripts?
    - Answer: Version control for Glue ETL scripts can be implemented by storing scripts in AWS CodeCommit or other version control systems, allowing for collaborative development and change tracking.

1. What are Glue Data Quality Rules?
    - Answer: Glue Data Quality Rules are customizable rules that allow users to define and enforce data quality checks on datasets, ensuring data integrity during the ETL process.

1. How can you create a custom transform in AWS Glue?
    - Answer: Custom transforms can be created using AWS Glue's ETL library by defining functions in Python or Scala scripts that implement specific data transformation logic.

1. What are the common data formats supported by AWS Glue?
    - Answer: AWS Glue supports various data formats including CSV, JSON, Parquet, ORC, and Avro, making it versatile for different data sources.

1. How does AWS Glue handle large-scale data processing?
    - Answer: AWS Glue uses Apache Spark under the hood for distributed processing, allowing it to efficiently handle large-scale data transformations across multiple nodes.

1. What are Glue job metrics, and how can they help optimize jobs?
    - Answer: Glue job metrics provide insights into execution time, resource utilization, and data processed. Analyzing these metrics can help identify bottlenecks and improve job performance.

1. How does AWS Glue pricing work?
    - Answer: AWS Glue pricing is based on the number of Data Processing Units (DPUs) consumed per hour for job runs, as well as charges for crawlers and Data Catalog storage.

1. What are some strategies for minimizing costs when using AWS Glue?
    - Answer: Strategies include:
        - Optimizing job configurations and using the appropriate DPU allocation.
        - Scheduling jobs to run during off-peak hours.
        - Leveraging Glue bookmarks to avoid processing the same data multiple times.

1. How do you handle large data volumes in AWS Glue?
    - Answer: Large data volumes can be handled by using distributed processing with Spark, optimizing data partitioning, and configuring Glue jobs to process data in chunks.

1. What are the advantages of using Spark with AWS Glue?
    - Answer: Spark provides distributed processing capabilities, allowing AWS Glue to handle large datasets efficiently. It also supports complex data transformations and machine learning integration.

1. What are the best practices for writing efficient ETL scripts in AWS Glue?
    - Answer: Best practices include:
        - Minimizing data movement.
        - Using appropriate data formats (e.g., Parquet).
        - Implementing error handling and logging.
        - Reusing code through functions.

1. How can you optimize AWS Glue jobs for speed and efficiency?
    - Answer: Optimization can be achieved by adjusting Spark configurations, minimizing data reads and writes, using in-memory processing, and leveraging Glue dynamic frames for efficient transformations.

1. How can you ensure data quality with AWS Glue?
    - Answer: Data quality can be ensured by implementing validation rules in ETL scripts, using Data Quality Rules in Glue, and monitoring data integrity through the Data Catalog.

1. How does AWS Glue support compliance with data privacy regulations?
    - Answer: AWS Glue supports compliance by allowing encryption of data, enforcing access controls through IAM policies, and providing auditing capabilities via CloudTrail for tracking data access and changes.

1. What is data lineage, and how is it tracked in AWS Glue?
    - Answer: Data lineage tracks the flow of data through ETL processes. In AWS Glue, it is tracked through the Data Catalog, which records job runs, transformations, and source/target mappings.

1. How can AWS Glue help with GDPR compliance?
    - Answer: AWS Glue can help with GDPR compliance by providing data access controls, auditing features, and enabling encryption for sensitive data, ensuring that personal data is handled securely.

1. What are some challenges of data governance in data lakes, and how does Glue address them?
    - Answer: Challenges include data quality, security, and compliance. AWS Glue addresses these by providing a unified Data Catalog, ETL capabilities, and integration with AWS services for security and monitoring.

1. How does AWS Glue facilitate data sharing within an organization?
    - Answer: AWS Glue facilitates data sharing through its Data Catalog, which allows teams to discover, access, and collaborate on datasets while enforcing access controls.

1. How can you track changes to data schemas in AWS Glue?
    - Answer: Changes to data schemas can be tracked through versioning in the Glue Data Catalog, which maintains a history of schema updates and allows users to revert to previous versions.

1. What are some common use cases for AWS Glue?
    - Answer: Common use cases include:
        - Data warehousing and analytics.
        - Data migration between systems.
        - Real-time data processing and streaming analytics.
        - Building data lakes.

1. How can AWS Glue be used for data transformation in a machine learning pipeline?
    - Answer: AWS Glue can prepare and transform data for machine learning by cleaning, normalizing, and aggregating data before feeding it into ML algorithms or models.

1. What is a practical example of using AWS Glue to integrate data from multiple sources?
    - Answer: An example could be extracting sales data from an RDS database, customer information from a CSV file in S3, transforming and joining them, and loading the results into a Redshift data warehouse.

1. How can you use AWS Glue for data archiving?
    - Answer: AWS Glue can process and transform active datasets into lower-cost storage formats (like Parquet) and move them to Amazon S3 for long-term archiving.

1. How can you leverage AWS Glue for batch processing scenarios?
    - Answer: AWS Glue can be used for batch processing by scheduling ETL jobs to run at specified intervals, processing large volumes of data efficiently using Spark.

1. What is a typical workflow using AWS Glue for a data pipeline?
    - Answer: A typical workflow involves:
        1. Data ingestion using Glue crawlers.
        1. ETL job execution for transformation.
        1. Storing processed data in S3 or a data warehouse.
        1. Setting up triggers for automated workflows.

1. How does AWS Glue support data versioning in a data lake?
    - Answer: AWS Glue supports data versioning by tracking changes in the Data Catalog and allowing users to maintain historical versions of datasets for auditing and compliance.

1. What strategies can you use to manage data sprawl in AWS Glue?
    - Answer: Strategies include implementing a robust Data Cataloging process, using tagging for resource management, and enforcing data governance policies to ensure consistent access controls.

1. How can you implement a data quality framework using AWS Glue?
    - Answer: A data quality framework can be implemented by defining quality rules, integrating validation checks in ETL jobs, and monitoring data quality metrics through AWS Glue and CloudWatch.

1. What are the limitations of AWS Glue?
    - Answer: Limitations include constraints on the number of concurrent jobs, maximum DPU allocation, and potential latency issues with real-time processing for specific use cases.

1. How can you troubleshoot performance issues in AWS Glue jobs?
    - Answer: Performance issues can be troubleshot by analyzing CloudWatch Logs, reviewing job metrics, checking data partitioning, and optimizing Spark configurations.

1. What best practices should you follow when using AWS Glue?
    - Answer: Best practices include:
        - Properly defining schemas and using partitioning.
        - Regularly updating and maintaining the Data Catalog.
        - Monitoring job metrics and costs.
        - Implementing robust error handling in ETL scripts.

1. How can you ensure the reliability of AWS Glue jobs?
    - Answer: Reliability can be ensured by implementing error handling, using retries for failed jobs, scheduling regular maintenance, and monitoring job status via CloudWatch.

1. What is the difference between AWS Glue and traditional ETL tools?
    - Answer: AWS Glue is serverless, fully managed, and integrates seamlessly with other AWS services, whereas traditional ETL tools may require more manual configuration, provisioning, and maintenance.

## Scenario-Based Questions
1. You mentioned using AWS Glue. Why did you choose Glue over setting up your own Spark cluster on EC2 or using AWS EMR?
    - The Answer: We chose AWS Glue primarily because it is serverless.
    - Simple Explanation: Imagine renting a car (EMR) where you have to decide the model, fuel it, and drive it, versus taking a taxi (Glue) where you just say 'take me there' and pay for the ride.
    - Technical Detail: With EMR or EC2, we have to manage the underlying infrastructure (patching OS, configuring Spark, managing cluster scaling). Glue abstracts all of that away. We only pay for the seconds the job runs. It integrates natively with the AWS ecosystem (like S3 and IAM), reducing the operational overhead significantly.

1. What exactly is a 'DynamicFrame' in Glue, and why didn't you just use a standard Spark DataFrame?
    - The Answer: A DynamicFrame is Glue’s proprietary data structure, specifically designed for messy data.
    - Simple Explanation: A standard Spark DataFrame assumes the data is perfect (like a strictly organized Excel sheet). If a column suddenly has a string where a number should be, Spark might crash or drop the data. A DynamicFrame is more flexible. It treats data like a flexible document, allowing it to hold unexpected formats without breaking.
    - Real-world Scenario: We had JSON logs where the schema changed frequently. DynamicFrames allowed us to process this data without constantly rewriting the code. However, we usually convert it back to a Spark DataFrame at the end of the script to use standard SQL transformations.

1. How does AWS Glue know what data is available in your S3 buckets?
    - The Answer: We use the AWS Glue Data Catalog and Crawlers.
    - Simple Explanation: Think of the Data Catalog as a library card catalog. It doesn't hold the books (the data), but it knows exactly where they are and what they are about. The 'Crawler' is a robot that goes through our storage (S3), reads the files, figures out the schema (columns/types), and updates the catalog.
    - Technical Detail: The Crawler runs periodically to detect new partitions or schema changes. Our ETL jobs then query the Catalog, not the raw files directly.

1. In a production environment, we receive new data every day. How did you ensure your Glue job only processed the new data and not the entire history?
    - The Answer: We utilized Job Bookmarks.
    - Simple Explanation: Just like a bookmark in a physical book tells you where you stopped reading, a Glue Job Bookmark tracks the last file it processed. When the job runs again, it checks the bookmark and only picks up files added since the last run.
    - Technical Detail: This is enabled in the job configuration. It stores states in a hidden internal bucket. If we ever need to reprocess everything (backfill), we can explicitly 'reset' the bookmark. This is critical for keeping our run times and costs low.

1. We often face the 'Small Files Problem' in big data. Did you encounter this, and how did you handle it in Glue?
    - The Answer: Yes, having thousands of tiny kilobytes-sized files (often from Kinesis Firehose) kills Spark performance because of the overhead in opening/closing files.
    - The Fix: We used the Glue Grouping feature.
    - Simple Explanation: Instead of asking the workers to pick up one grain of sand at a time, we tell Glue to 'group' them into a bucket first, then pick up the bucket.
    - Technical Detail: When creating the DynamicFrame, we set groupFiles: 'inPartition' and specified a target size (e.g., 50MB). This instructs the Glue driver to merge these small files in memory before sending them to the executor nodes for processing.

1. How did you configure your workers? What is a DPU?
    - The Answer: A Data Processing Unit (DPU) is the measure of processing power.
    - Simple Explanation: One DPU is roughly equivalent to 4 vCPUs and 16GB of RAM. It's the 'engine size' of our job.
    - Technical Detail:
        - Standard: Good for basic startup, but slow.
        - G.1X: The standard for memory-intensive jobs (1 DPU per worker).
        - G.2X: Double the power (2 DPUs per worker). We used G.1X for most ETL jobs. However, for memory-heavy joins where we saw OOM (Out of Memory) errors, we switched to G.2X or enabled Autoscaling (Glue 3.0/4.0 feature) so Glue could add workers dynamically if the load increased.

1. AWS Glue can get expensive. What specific strategies did you implement to optimize costs?
    - The Answer: Cost in Glue is a function of DPUs * Time. We attacked both variables:
        - Flex Execution: For non-urgent (SLA-insensitive) jobs, we used 'Flex' execution. It allows Glue to run on spare capacity (similar to Spot Instances) for up to a 35% discount.
        - Auto Scaling: Instead of statically provisioning 50 workers, we enabled Glue Auto Scaling. The job might start with 5 workers, scale up to 50 during the heavy shuffle/sort phase, and drop back to 5. We stop paying for idle workers.
        - Timeout Tuning: The default timeout is 48 hours. We reduced this to 1 hour to prevent 'zombie jobs' (stuck jobs) from running all weekend and racking up bills.

1. How did you handle Schema Evolution? For example, what happens if the source system adds a new column or changes a data type?
    - The Answer: We handled this at the Crawler level and the ETL level.
    - Crawler Configuration: We configured the Crawler to 'Update the table definition in the data catalog' when it sees a change, but strict policies were set on conflicts.
    - The 'ResolveChoice' method: In the ETL code, if a column suddenly changes from an INT to a STRING, Spark usually fails. We used the Glue method ResolveChoice:
        - Option 1 (Cast): Force everything to the new type.
        - Option 2 (Make Struct): Keep both the old int and new string in a structure.
        - Real World: We typically cast to a stronger type (like String) to ensure no data loss, then let downstream data quality checks flag the anomaly.

1. Describe a scenario where you faced an OOM (Out of Memory) exception in Glue and how you debugged it.
    - The Answer: We faced OOM errors when doing a Join operation on two large tables where the data was skewed (one key had 90% of the data).
    - Debugging: We enabled Glue Continuous Logging and looked at the CloudWatch metrics. We saw that one specific Executor had spiked to 100% memory usage while others were idle—a classic sign of Data Skew.
    - The Solution:
        - We couldn't just increase DPUs (vertical scaling) because the skew would still overload that one node.
        - We implemented Salted Keys. We added a random number to the join key to distribute that massive 'hot key' across multiple nodes, performed the aggregation, and then aggregated again.
        - Alternatively, for smaller lookups, we used Broadcast Joins to send the smaller table to all nodes rather than shuffling the massive table.

1. How did you schedule your Glue jobs? Did you use standard cron schedules, or something more complex?
    - The Answer: We used AWS Glue Workflows (or Step Functions).
    - Simple Explanation: A simple cron schedule (e.g., 'run at 9 AM') is risky. What if the source data hasn't arrived by 9 AM? The job would fail.
    - The Better Way: We used Event-Based Triggers:
        1. Sensor: We set up an S3 Event. When a file lands in the input/ folder, it triggers a Lambda/Workflow.
        1. Chaining: We created a dependency chain: Crawler runs first → If successful, Job A runs → If Job A succeeds, Job B runs.
    - Real-world Scenario: Our 'Daily Sales' report relied on three different tables updating. We used a Glue Workflow to ensure the final aggregation job only started once all three source jobs finished successfully.

1. How do you handle passwords and database credentials in your Glue script? Surely you don't hardcode them.
    - The Answer: Absolutely not. We used AWS Secrets Manager integrated with Glue Connections.
    - Simple Explanation: Hardcoding a password in a script is a security violation. Instead, we store the password in a secure digital vault (Secrets Manager).
    - Technical Detail: In Glue, I create a 'Connection' (e.g., MyRDSConnection) that references the secret. In my script, I just call `glueContext.create_dynamic_frame.from_options(connection_type=mysql, connection_options={useConnectionProperties: true, connectionName: MyRDSConnection})`. Glue handles the fetching of credentials securely behind the scenes.

1. Explain 'PushDown Predicates' in Glue. Why are they critical for performance?
    - The Answer: PushDown Predicates are the single most important optimization for reading partitioned data.
    - Simple Explanation: Imagine you need a book from the library about '1990 history':
        - Without PushDown: You bring every single book from the library to your desk, then look at the dates one by one to find 1990.
        - With PushDown: You ask the librarian to only bring you the books from the '1990' shelf.
    - Technical Detail:
        - If I write datasource.filter(x => x['year'] == '2023'), Spark reads everything first, then filters.
        - If I use `push_down_predicate = (year == '2023')`, Glue filters the files at S3 before they are even read into memory. This saves massive amounts of IO and cost.
    - Real-world Scenario: We had a 5-year dataset. Without PushDown predicates, the job took 2 hours. With `push_down_predicate=(year=='2024' and month=='01')`, it took 5 minutes.

1. What is the difference between 'Glue Context' and standard 'Spark Context'?
    - The Answer: Glue Context is a wrapper around the Spark Context that adds AWS-specific capabilities.
    - Simple Explanation: Spark Context is the standard engine. Glue Context adds the 'AWS plugins'.
    - Key Differences:
        - DynamicFrames: Only Glue Context can create DynamicFrames (the flexible data structure we discussed earlier).
        - S3 Interactions: Glue Context has optimized readers/writers for S3 that handle listing files faster than standard Spark.
        - Catalog Integration: Glue Context connects directly to the Glue Data Catalog methods (`create_dynamic_frame.from_catalog`).

1. How do you handle 'Data Quality' issues automatically? For example, if a mandatory column arrives with NULL values?
    - The Answer: We implemented AWS Glue Data Quality (based on Deequ).
    - Simple Explanation: Before processing the data, we run a 'health check'. If the data is 'sick' (too many nulls), we quarantine it.
    - Technical Detail: We added a transform in the Glue job that evaluates rules like:
        - IsComplete customer_id (Check for nulls)
        - ColumnValues age between 18 and 100
    - Action: If the quality score drops below 95%, we configured the job to either fail immediately (to prevent bad data from hitting the warehouse) or tag the data as 'suspect' and send an SNS alert to the engineering team.

1. How did you implement CI/CD (Continuous Integration/Deployment) for your Glue jobs? How do you move code from Dev to Prod?
    - The Answer: We moved away from manual console edits to Infrastructure as Code (IaC).
    - The Problem: Manually copying code from Dev to Prod is error-prone. You might forget to change the database name or S3 bucket path.
    - The Solution:
        1. Git Repository: All Glue scripts (Python/Scala) are stored in Git.
        1. IaC Tool (Terraform/CDK): We define the Glue Job resource (memory, timeout, script location) in Terraform.
        1. Pipeline: When we push code to the main branch:
            - A Jenkins/GitLab pipeline copies the script to a versioned S3 bucket (e.g., s3://my-bucket/scripts/v1.2/job.py).
            - Terraform updates the Glue Job definition to point to this new script.
    - Real-world Scenario: This allowed us to roll back instantly. If v1.2 failed in production, we just re-ran the Terraform pipeline pointing back to v1.1.

1. We have a requirement for 'Near Real-Time' data. Can Glue handle streaming, or do we need Kinesis Analytics?
    - The Answer: Glue can handle streaming. We used Glue Streaming ETL.
    - Simple Explanation: Instead of a job that starts and stops (Batch), Glue Streaming runs continuously, listening to a stream (like Kinesis or Kafka) and processing data in small 'micro-batches' (e.g., every 10 seconds).
    - Technical Detail:
        - It uses Spark Structured Streaming under the hood.
        - We enabled check-pointing in S3 so if the job crashes, it remembers exactly which record it read last.
    - Trade-off: Glue Streaming has a startup latency (cold start). If you need sub-second latency, Kinesis Data Analytics (Flink) is better. If 1-2 minute latency is acceptable, Glue is easier because we can reuse our existing Python logic.

1. How do you handle PII (Personally Identifiable Information) in Glue to ensure GDPR/CCPA compliance?
    - The Answer: We implemented Pattern Matching and Hashing during the ingestion phase.
    - The Strategy: PII should never land in the raw data lake in plain text if possible.
    - Implementation:
        1. Detection: We used Glue's 'FindMatches' ML transform (or simple regex) to identify columns that look like SSNs or Emails.
        1. Anonymization: In the DynamicFrame, we apply a hashing function (SHA-256) to the email column before writing to the target S3 bucket.
        1. Encryption: We enabled S3 Server-Side Encryption (SSE-S3) and Glue Security Configurations to ensure that temporary data spilled to disk during the job is also encrypted.

## Error-Based Questions
1. Your Glue Job failed with an `AnalysisException : cannot resolve ‘column_name’`, but you checked the source CSV file in S3, and the column is definitely there! Why can’t Glue see it?
    - The Answer: This is usually a Crawler or Metadata issue.
    - The Cause: If you added a new column to the CSV file after the Glue crawler last ran, the Data Catalog doesn’t know about it yet. Glue reads the catalog definition, not the raw file header dynamically (unless configured otherwise).
    - The Fix: Rerun the Glue Crawler to update the table definition. Alternatively, in the script, use o`ption(mergerSchema, true)` if reading directly from S3 without the catalog.

1. A simple job that usually takes 10 minutes has been running for 48 hours and is still stuck. What happened?
    - The Answer: This is often a 'Zombie' Task or Infinite Loop.
    - The Cause: It could be a join operation on a massive dataset causing data skew, where one worker is stuck processing 99% of the data while others are idle. Or, the job might be waiting for a resource (like a database connection) that never responds.
    - The Fix: Immediate: Kill the job manually.
    - Prevention: Always set a Timeout in the job properties (e.g., 60 minutes) so it fails fast instead of burning money for 2 days.
    - Debug: Check CloudWatch logs for the 'straggler' task.

1. You wrote a script to read from `s3://source-bucket` and write to `s3://target-bucket`. The job fails saying it cannot write to the target. You checked the IAM Role, and it has `S3FullAccess`. What is missing?
    - The Answer: It could be a KMS Encryption Key issue.
    - The Nuance: Even if you have access to the Bucket, if the bucket is encrypted with a custom KMS Key, your IAM Role also needs the `kms:GenerateDataKey` and `kms:Decrypt` permissions for that specific key.
    - Another possibility: The Bucket Policy on the target bucket might explicitly deny your role, which overrides your IAM `S3FullAccess`.

1. Your job runs fine on Monday (1GB data) but crashes on Friday (1.5GB data) with the container killed by YARN for exceeding memory limits. You already upgraded to G.2X workers, but it still fails. What do you look for?
    - The Answer: This screams Data Skew.
    - The Explanation: Increasing memory (vertical scaling) doesn't fix skew. If you join on a key like country_code and 'US' has 90% of the data, all that data goes to one worker. That single worker will always run out of RAM, no matter how big the cluster is.
    - The Fix:
        - Visualize: Check the Glue UI monitoring to see if one executor bar is red/high usage while others are empty.
        - Salt the Key: Add a random number to the join key to distribute the 'US' data across multiple workers, then aggregate later.
        - Broadcast Join: If joining a huge table with a small table, force a Broadcast Join to send the small table to all nodes instead of shuffling the huge one.

1. Your Glue job tries to connect to an RDS database. The job fails after a long wait with a Connection Timed Out error. The username/password are correct.
    - The Answer: This is a Security Group / VPC configuration error.
    - The Cause: Glue runs in its own VPC managed by AWS by default. It cannot reach your private RDS unless you set up a Glue Connection.
    - The Debug Checklist:
        1. Did you create a 'Glue Connection' object with the VPC/Subnet details?
        1. Does the Security Group of the RDS allow 'Inbound' traffic from the Security Group of the Glue job on port 3306 (MySQL)? This 'Self-Referencing' rule is often missed.

1. You know how to fix an Executor crash (add workers). But what if the Driver node itself runs out of memory? The logs stop abruptly. Why does this happen?
    - The Answer: Driver OOM happens when you try to bring too much data back to the 'brain' of the operation.
    - Common Error: Using `collect()` on a large DataFrame. This forces all distributed workers to send their data to the single Driver node.
    - Another Cause: Too many partitions. If you have 1 million partitions, the Driver stores the map of where all those partitions are. This metadata can fill up the Driver's RAM.
    - The Fix:
        - Never use `collect()` in production; use `.take(10)` for debugging.
        - Increase `spark.driver.memory`.
        - Compact your S3 files to reduce the partition count.

1. Your Glue job is writing massive amounts of data to S3 using highly parallelized workers. It starts failing with 503 Slow Down errors from S3.
    - The Answer: You are exceeding S3 Request Rate Limits (3,500 PUTs/sec per prefix).
    - The Cause: All your Spark workers are trying to write to `s3://bucket/output/year=2024/...` at the exact same second.
    - The Fix:
        - Reduce Parallelism: Lower the number of concurrent writers using `coalesce()`.
        - Randomize Prefixes: (Legacy fix) Add random hashes to file prefixes.
        - Retry Logic: Ensure the AWS SDK retry strategy is set to 'Adaptive' mode to handle back-pressure automatically.

1. You need to use a specific version of pandas (e.g., 1.5.0) because your code relies on a deprecated feature. But Glue keeps loading a newer version, breaking your code. You uploaded a `.whl` file, but it’s ignored.
    - The Answer: This is a path precedence issue.
    - The Problem: Glue has pre-installed libraries. If you just `pip install` or upload a wheel, Glue might still prioritize its internal system path.
    - The Fix: You need to pass the `--additional-python-modules` parameter correctly.
    - Expert Fix: If that fails, standard Python practice applies: use a Virtual Environment (venv). Zip up the entire venv and pass it to Glue, forcing it to use your isolated environment instead of the system default.

1. You ran a Glue job yesterday, and it processed 100 files successfully. Today, you realized there was a logic error in your code. You fixed the code and re-ran the job against the same files. The job finished in 5 seconds and processed 0 records. Why?
    - The Answer: This is the Job Bookmark doing its job too well.
    - The Cause: Glue remembers that it has already processed those specific files (based on timestamps and file sizes). It thinks, 'I have nothing new to do,' and shuts down.
    - The Fix: You must Reset (Rewind) the Job Bookmark.
        - In the AWS Console: Action -> 'Reset Job Bookmark':
        - In Script: pass the argument --job-bookmark-option job-bookmark-disable for that specific run to force a full re-process.

1. You uploaded a clean CSV file to S3. You ran a Glue Crawler to create the table. The Crawler finished, but the table classification is Unknown or txt, and the columns are just col0, col1... instead of your actual headers.
    - The Answer: The Crawler failed to infer the CSV format.
    - Common Cause 1 (Quotes): You have an unclosed quote in the data (e.g., 123 Main St, Apt 4). This breaks the CSV parser, so Glue falls back to treating it as a raw text file.
    - Common Cause 2 (Mixed Delimiters): Your header uses commas, but line 50 uses a tab or pipe.
    - The Fix: Open the file in a text editor (or use head in CLI) to inspect for malformed rows. If the data is messy, create the table manually in Athena utilizing the OpenCSVSerDe (which is more forgiving) instead of relying on the Crawler.

1. The job runs for an hour and then fails with `org.apache.spark.shuffle.FetchFailedException`. The logs show that Stage 5 failed. Is this a memory issue?
    - The Answer: Not necessarily. This is a Network/Shuffle issue.
    - The Meaning: 'Node A' tried to fetch data from 'Node B' (as part of a Sort or Join), but 'Node B' was unreachable or unresponsive.
    - Likely Cause:
        - Spot Instances: 'Node B' was a Spot worker that AWS took back suddenly.
        - GC Pause: 'Node B' was so busy doing Garbage Collection (cleaning RAM) that it didn't respond to the network request in time (Time out).
    - The Fix:
        - If using Spot, enable Glue Spark UI to see if executors were lost.
        - Relax the timeout: Increase `spark.network.timeout`.
        - If it happens during a massive Join, handle the data skew (which causes the GC pause).

1. Your Glue job reads JSON logs. It works fine for months. Suddenly it fails because 'Column price is incompatible'. It turns out the upstream app started sending price: 10.50 (string) instead of price: 10.50 (double).
    - The Answer: Spark hates schema changes at runtime. It expects one type.
    - The Fix: Use the Glue `ResolveChoice` class. Force everything to double, converting strings if possible:
        - `df_resolved = df.resolveChoice(specs = [('price', 'cast:double')])`
    - Alternative: Use `make_struct` to keep both values (a struct with an int field and a string field) so you don't lose data, then clean it up later in the ETL logic.

1. The job fails with `java.io.IOException: No space left on device`. You are confused because you know S3 has infinite storage. Where is the space running out?
    - The Answer: It is running out of Local Disk Space (Shuffle Spill) on the worker node.
    - The Cause: When Spark runs out of RAM, it 'spills' data to the local hard drive of the executor (the /mnt directory). If you are using Standard or G.1X workers, they have limited disk space (~50GB). A massive sort/join can fill this up quickly.
    - The Fix:
        - Upgrade Worker: Switch to G.2X worker type (which provides more SSD storage).
        - Optimize: Tune the query to reduce spilling (filter data earlier, reduce skew).

1. Your job uses `push_down_predicate` to filter partitions, so it should be fast. But it fails during initialization with `EntityNotFoundException` or `ThrottlingException` related to the Glue Data Catalog.
    - The Answer: You are DDoSing the Glue Catalog Service API, not S3.
    - The Cause: If your table has millions of partitions (e.g., partitioned by minute: year/month/day/hour/minute), even a simple query forces Glue to make thousands of API calls to the Catalog to retrieve partition metadata.
    - The Fix:
        - Partition Indexes: Enable 'Partition Indexes' on the Glue table. This allows Glue to fetch specific partitions via a direct index lookup rather than listing everything.
        - Redesign: Change partitioning strategy to be coarser (e.g., just Year/Month/Day). Partitioning by 'Minute' is almost always an anti-pattern in Big Data.

1. Your Glue Job is in Account A. The S3 Data is in Account B. You gave the Glue Role in Account A permission to `s3:*` on Bucket B. You checked Bucket B's policy, and it allows Account A. It still fails with 403 Access Denied. Why?
    - The Answer: You forgot the KMS Key Trust Policy.
    - The Hidden Lock: If Bucket B is encrypted with a custom KMS key (in Account B), simply allowing access to the Bucket is not enough. You must also update the Key Policy of that KMS Key in Account B to allow the IAM Role from Account A to use `kms:Decrypt`.
    - Summary: Cross-account access always requires Three Keys to Turn:
        - Identity Policy (My Role).
        - Resource Policy (Target Bucket).
        - Encryption Policy (Target KMS Key).