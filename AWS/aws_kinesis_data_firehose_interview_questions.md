# AWS Kinesis Data Firehose Interview Questions

## Basic Questions
1. What is AWS Kinesis Data Firehose?
    - Answer: AWS Kinesis Data Firehose is a fully managed service that automatically collects, transforms, and loads streaming data into data lakes, data stores, and analytics services, such as Amazon S3, Amazon Redshift, and Amazon Elasticsearch Service.

1. What are the main use cases for Kinesis Data Firehose?
    - Answer: Common use cases include real-time analytics, log and event data collection, data lake ingestion, and data transformation for analytics.

1. How does Kinesis Data Firehose differ from Kinesis Data Streams?
    - Answer: Kinesis Data Firehose is focused on delivering data to storage solutions without requiring manual management of data processing, while Kinesis Data Streams allows for custom processing of streaming data.

1. What are the benefits of using Kinesis Data Firehose?
    - Answer: Benefits include ease of use, automatic scaling, real-time data delivery, built-in data transformation capabilities, and seamless integration with AWS services.

1. What data sources can you stream to Kinesis Data Firehose?
    - Answer: Data can come from various sources, including IoT devices, web applications, and other AWS services like Kinesis Data Streams and AWS Lambda.

1. How do you create a Kinesis Data Firehose delivery stream?
    - Answer: You can create a delivery stream using the AWS Management Console, AWS CLI, or AWS SDKs by specifying the source, destination, and optional transformation settings.

1. What destinations are supported by Kinesis Data Firehose?
    - Answer: Supported destinations include Amazon S3, Amazon Redshift, Amazon Elasticsearch Service, and custom HTTP endpoints.

1. Can Kinesis Data Firehose deliver data to multiple destinations?
    - Answer: No, Kinesis Data Firehose can deliver data to a single destination per delivery stream.

1. What is the maximum data retention period for Kinesis Data Firehose?
    - Answer: Kinesis Data Firehose does not have a data retention period for the delivery stream itself, but it stores data temporarily while delivering to the specified destination.

1. How do you configure buffering in Kinesis Data Firehose?
    - Answer: Buffering can be configured by specifying the buffer size (in MB) and buffer interval (in seconds) to control how much data Firehose accumulates before sending it to the destination.

1. What is data transformation in Kinesis Data Firehose?
    - Answer: Data transformation allows you to modify or enrich the data before it is delivered to the destination, using AWS Lambda functions.

1. How do you implement data transformation in a Firehose delivery stream?
    - Answer: You can specify a Lambda function in the Firehose configuration to process incoming records for transformation before they are sent to the destination.

1. What is the maximum timeout for Lambda functions used in Kinesis Data Firehose?
    - Answer: The maximum timeout for Lambda functions invoked by Kinesis Data Firehose is 300 seconds (5 minutes).

1. Can you perform multiple transformations on the same record in Kinesis Data Firehose?
    - Answer: No, Kinesis Data Firehose supports only one transformation function per delivery stream.

1. How do you handle failed transformations in Kinesis Data Firehose?
    - Answer: Failed transformations can be routed to a designated Amazon S3 bucket as a dead-letter queue for further analysis.

1. How do you monitor a Kinesis Data Firehose delivery stream?
    - Answer: Monitoring can be done using Amazon CloudWatch, which provides metrics like Incoming Bytes, Delivery Success, Delivery Failure, and more.

1. How can you enable logging for Kinesis Data Firehose?
    - Answer: You can enable server-side logging by configuring an Amazon S3 bucket to store logs related to data delivery and processing.

1. What IAM permissions are required to interact with Kinesis Data Firehose?
    - Answer: Required permissions include actions like `firehose:CreateDeliveryStream`, `firehose:PutRecord`, `firehose:DescribeDeliveryStream`, and `firehose:ListDeliveryStreams`.

1. How do you secure data in Kinesis Data Firehose?
    - Answer: Data can be secured using encryption at rest (S3 server-side encryption) and in transit (TLS), along with IAM policies for access control.

1. What data formats does Kinesis Data Firehose support for delivery?
    - Answer: Supported formats include JSON, CSV, Apache Parquet, and Apache ORC.

1. Can Kinesis Data Firehose deliver compressed data?
    - Answer: Yes, Firehose supports gzip, snappy, and bzip2 compression formats for data delivery.

1. What is the maximum size of a record that Kinesis Data Firehose can handle?
    - Answer: The maximum size of a single record is 1,000 KB for data sent to Firehose.

1. What happens if a record exceeds the maximum size limit?
    - Answer: Records that exceed the size limit will be dropped, and you will receive an error message.

1. How can you specify the prefix for objects in an S3 bucket when using Kinesis Data Firehose?
    - Answer: You can specify the S3 prefix in the delivery stream configuration, allowing you to organize files into specific folders based on data attributes or timestamps.

1. How does Kinesis Data Firehose handle scaling?
    - Answer: Kinesis Data Firehose automatically scales to match the incoming data volume without requiring manual intervention.

1. What is the maximum throughput for Kinesis Data Firehose?
    - Answer: Kinesis Data Firehose can handle a maximum throughput of 5,000 records per second and 1,000 MB per second for data delivery.

1. How does Firehose manage back pressure when data inflow exceeds capacity?
    - Answer: Firehose buffers incoming data until it can successfully deliver to the destination, applying back pressure when necessary.

1. What are the best practices for optimizing Kinesis Data Firehose performance?
    - Answer: Best practices include configuring appropriate buffer sizes and intervals, minimizing record sizes, and monitoring delivery metrics to adjust settings as needed.

1. What are the limits on the number of delivery streams in Kinesis Data Firehose?
    - Answer: As of now, you can have up to 100 delivery streams per AWS Region by default, but this can be increased by requesting a service limit increase.

1. What is the significance of buffering hints in Kinesis Data Firehose?
    - Answer: Buffering hints control how data is collected and sent to the destination, impacting performance, latency, and delivery efficiency.

1. How can you use Kinesis Data Firehose to enable serverless architectures?
    - Answer: Kinesis Data Firehose simplifies data ingestion and delivery in serverless architectures by eliminating the need for managing infrastructure while processing streaming data.

1. What are the common patterns for implementing Kinesis Data Firehose?
    - Answer: Common patterns include collecting application logs, processing IoT device data, and streaming user activity data for analytics.

1. How can you integrate Kinesis Data Firehose with other AWS services for end-to-end solutions?
    - Answer: Kinesis Data Firehose can be integrated with AWS Lambda for data transformation, Amazon S3 for storage, and analytics services like Amazon Redshift and Athena for querying.

1. What is the role of retries in Kinesis Data Firehose?
    - Answer: Kinesis Data Firehose automatically retries failed delivery attempts to destinations, enhancing reliability and ensuring data is not lost.

1. What are the best practices for designing Kinesis Data Firehose delivery streams?
    - Answer: Best practices include setting appropriate buffer sizes and intervals, enabling data transformation if needed, monitoring delivery metrics, and securing data appropriately.

1. How can you ensure the reliability of data delivery in Kinesis Data Firehose?
    - Answer: Reliability can be ensured through monitoring, setting up dead-letter queues, and using retries for failed deliveries.

1. What is the recommended approach to manage costs when using Kinesis Data Firehose?
    - Answer: To manage costs, monitor usage closely, adjust buffer sizes and intervals based on data patterns, and leverage AWS Cost Explorer for insights.

1. How do you maintain and update a Kinesis Data Firehose delivery stream?
    - Answer: Updates can be made via the AWS Management Console, AWS CLI, or SDKs, allowing changes to configurations such as buffer settings and destination parameters.

1. What common errors might you encounter when using Kinesis Data Firehose?
    - Answer: Common errors include delivery failures due to destination issues, data size limits being exceeded, and transformation errors when using Lambda functions.

1. How does Kinesis Data Firehose fit into the AWS data ecosystem?
    - Answer: Kinesis Data Firehose integrates with other AWS services for data collection, transformation, and storage, playing a crucial role in building real-time data pipelines.

1. Can Kinesis Data Firehose be used for batch processing?
    - Answer: Kinesis Data Firehose is primarily designed for streaming data, but it can be configured to batch data before sending it to the destination based on buffer settings.

1. What is the significance of schema evolution in data delivery?
    - Answer: Schema evolution is important as data formats change over time, ensuring that data delivered remains compatible with the analytics services consuming it.

1. How can Kinesis Data Firehose handle different data formats in a single stream?
    - Answer: Kinesis Data Firehose can handle different data formats by specifying the expected format for incoming records and ensuring transformations accommodate those formats.

1. What is the importance of data retention policies when using Kinesis Data Firehose?
    - Answer: Data retention policies define how long data is retained in the destination (e.g., S3), impacting compliance, analytics, and data management strategies.

1. How do you troubleshoot failed data deliveries in Kinesis Data Firehose?
    - Answer: Troubleshooting involves checking CloudWatch metrics, reviewing delivery stream logs, and validating IAM permissions for the destination.

1. What steps would you take if you encounter high delivery failure rates?
    - Answer: Steps include reviewing destination health, adjusting buffer settings, monitoring data transformation functions, and validating record formats.

1. How can you optimize data delivery to Amazon S3 using Kinesis Data Firehose?
    - Answer: Optimization can be achieved by configuring buffer sizes appropriately, using compression, and organizing data using prefixes for efficient retrieval.

1. What is the role of retry intervals in Kinesis Data Firehose?
    - Answer: Retry intervals determine how long Kinesis Data Firehose waits before retrying failed delivery attempts, impacting overall data delivery reliability.

1. How do you implement a failover strategy for Kinesis Data Firehose?
    - Answer: A failover strategy can be implemented by using dead-letter queues, directing failed records to alternative S3 buckets, or integrating with alerting systems.

1. How can you ensure compliance when using Kinesis Data Firehose?
    - Answer: Compliance can be ensured by implementing encryption, access controls, and logging mechanisms to track data movement and transformations.

1. What considerations are there for data privacy in Kinesis Data Firehose?
    - Answer: Considerations include encrypting sensitive data, controlling access through IAM, and complying with regulations like GDPR or CCPA.

1. How do you handle sensitive information in Kinesis Data Firehose?
    - Answer: Sensitive information can be handled by encrypting data in transit and at rest, applying access controls, and using transformations to mask sensitive fields.

1. What are the security best practices for using Kinesis Data Firehose?
    - Answer: Best practices include using IAM policies for fine-grained access control, enabling encryption, monitoring access logs, and applying least privilege principles.

1. What programming languages are commonly used with Kinesis Data Firehose?
    - Answer: Common programming languages include Python, Java, and Node.js, particularly for AWS Lambda functions used in data transformation.

1. How do you handle schema management with Kinesis Data Firehose?
    - Answer: Schema management can be handled by using schema registries or defining schema expectations in the transformation logic to ensure compatibility.

1. What are the limits on the number of records per second for Kinesis Data Firehose?
    - Answer: Kinesis Data Firehose has a limit of 5,000 records per second for incoming data, and this can be increased by requesting a service limit increase.

1. What challenges might arise when using Kinesis Data Firehose in production?
    - Answer: Challenges may include handling high data volumes, ensuring low latency, managing schema changes, and monitoring for delivery failures.

1. What is the difference between Kinesis Data Firehose and AWS Data Pipeline?
    - Answer: Kinesis Data Firehose is designed for real-time streaming data delivery, while AWS Data Pipeline is used for batch data processing and orchestration.

1. How does Kinesis Data Firehose manage schema evolution?
    - Answer: Kinesis Data Firehose allows for the configuration of transformations that can handle schema changes over time, ensuring compatibility with downstream systems.

1. What is the importance of data quality in Kinesis Data Firehose?
    - Answer: Data quality is crucial as it impacts the accuracy and reliability of analytics derived from the streamed data, necessitating validation and cleaning processes.

1. How can you optimize costs when using Kinesis Data Firehose?
    - Answer: Costs can be optimized by adjusting buffer settings, minimizing record sizes, and monitoring usage patterns for better resource allocation.

1. What is the significance of the data transformation feature in Firehose?
    - Answer: Data transformation allows for preprocessing and enhancing the data before it reaches its destination, improving the relevance and usability of the data.

1. What are the best practices for configuring buffering in Kinesis Data Firehose?
    - Answer: Best practices include balancing buffer sizes and intervals based on data flow patterns and destination performance requirements.

1. How do you ensure the durability of data in Kinesis Data Firehose?
    - Answer: Durability is ensured by utilizing Amazon S3 as a delivery destination, which provides high durability for stored objects.

1. What are some performance tuning techniques for Kinesis Data Firehose?
    - Answer: Performance tuning techniques include adjusting buffer settings, optimizing data formats, and ensuring efficient use of transformation functions.

## Scenario-Based Questions
1. You used Kinesis Firehose in your project. Why didn't you use Kinesis Data Streams instead? What is the main difference?
    - The Answer: The main difference is Custom Processing vs. Delivery.
    - Kinesis Data Streams (KDS): It is a storage pipe. It holds data for 24 hours, and you must write custom code (Consumer) to read it. It is for sub-second, complex real-time analytics.
    - Kinesis Firehose: It is a Managed Delivery Service. I don't write code to read from it. I just configure it by saying 'Dump this data into S3'.
    - Why I chose Firehose: I simply needed to archive logs to S3. Writing a custom consumer for that would be over-engineering. Firehose handles the batching, compression, and encryption automatically.

1. Firehose is 'Near Real-Time', not 'Real-Time'. What does that mean? How fast does data appear in S3?
    - The Answer: It means there is a minimum latency (delay).
    - Buffering: Firehose doesn't write every single record to S3 the moment it arrives (that would create millions of tiny files). Instead, it buffers them.
    - The Config: We configure a Buffer Size (e.g., 5 MB) and Buffer Interval (e.g., 300 seconds).
    - The Behavior: Firehose waits until either it has 5 MB of data or 300 seconds have passed, whichever comes first. So, at worst, the data will appear in S3 5 minutes after ingestion. This is 'Near Real-Time'.

1. Can Firehose write data to a database directly, like MySQL or PostgreSQL?
    - The Answer: No, Firehose has a limited set of supported destinations.
    - Supported: Amazon S3, Amazon Redshift, Amazon OpenSearch (Elasticsearch), Splunk, and generic HTTP Endpoints (Datadog, MongoDB Cloud).
    - Not Supported: It cannot write directly to RDS (MySQL/Postgres) or DynamoDB. For that, we would need to trigger a Lambda function or use Kinesis Data Streams.

1. We want to query our logs in S3 using Amazon Athena. To save costs, we need the data in 'Parquet' format, but the source sends 'JSON'. How did you handle this?
    - The Answer: We used the built-in Record Format Conversion feature in Firehose.
    - The Problem: Converting JSON to Parquet usually requires running a Spark/Glue job, which adds cost and latency.
    - The Solution: In the Firehose settings, I enabled 'Convert record format'. I pointed Firehose to an AWS Glue Table schema so it knows the field names.
    - The Result: Firehose automatically converts the streaming JSON into Parquet files before writing to S3. This made our Athena queries 10x faster and cheaper because Parquet is columnar.

1. The source data contains PII (e.g., Social Security Numbers) that we cannot store in S3. How do you remove it before Firehose writes the file?
    - The Answer: I configured a Lambda Transformation.
    - How it works: Firehose can invoke a Lambda function for every batch of data it buffers.
    - The Logic:
        1. Firehose sends a batch of raw records to Lambda.
        1. The Lambda code parses the JSON, masks the SSN (replaces it with ***), or drops the field entirely.
        1. Lambda returns the clean records to Firehose.
        1. Firehose writes the clean data to S3.
    - Benefit: We scrub sensitive data in flight without needing a staging bucket.

1. What happens if the Lambda Transformation fails (e.g., a bug in the code)? Do we lose that data?
    - The Answer: No, we configured a Source Record Backup bucket.
    - Configuration: In Firehose settings, we enable 'Backup Mode'. We can choose 'All records' or 'Failed records only'.
    - Scenario: If the Lambda transformation fails or the data format is bad, Firehose writes the original raw record to a separate 'ProcessingFailed' folder in S3.
    - Recovery: We can later run a repair script to fix and re-ingest those failed records.

1. Explain exactly how Firehose loads data into Redshift. Does it run an INSERT statement for every record?
    - The Answer: No, doing INSERTs for streaming data would kill Redshift's performance.
    - The Mechanism: Firehose uses a Two-Step Process.
        - Step 1: Firehose writes the data to an Intermediate S3 Bucket first.
        - Step 2: Once the file is written, Firehose issues a `COPY` command to Redshift.
    - Why: The `COPY` command is the most efficient way to bulk-load data into Redshift (parallel loading).
    - Implication: If the `COPY` command fails (e.g., data type mismatch), the data stays in S3, and Firehose logs an error in the 'Manifest' file. It does not retry indefinitely to avoid blocking the pipe.

1. We have a requirement to store data in S3 folders based on the 'Event Type' inside the JSON (e.g., `s3://bucket/Login/` and `s3://bucket/Purchase/`). Firehose usually just partitions by Date. How do you fix this?
    - The Answer: We used Dynamic Partitioning.
    - Standard Behavior: Firehose partitions by time: YYYY/MM/DD/HH.
    - Advanced Feature: We enabled Dynamic Partitioning using 'Inline Parsing' (JQ) or Lambda.
    - Configuration: We tell Firehose to look at the JSON field `event_type`.
    - Result: Firehose creates custom prefixes like `event_type=Login/year=2024/...` on the fly.    - 
    - Warning: We must be careful about High Cardinality. If the `event_type` has 10,000 unique values (like User_ID), Firehose will create 10,000 tiny files and buffers, reducing performance and increasing S3 PUT costs.

1. You are being throttled. Firehose is throwing `ThroughputExceeded` errors. Is it just a setting, or do we need to re-architect?
    - The Answer: It depends on the region and current limits, but Firehose scales differently than Streams.
    - The Limits: By default, Firehose can ingest around 5,000 records/sec or 5 MB/sec (varies by region).
    - The Scaling: unlike Kinesis Streams where I have to manually add shards, Firehose Auto-Scales... to a point.
    - The Solution: If we hit the soft limit, we just open a support ticket to raise the quota. However, if we are doing massive throughput, we might need multiple Firehose streams because Firehose doesn't have the concept of 'Shards' that we can control directly.

1. You have a Firehose stream writing to S3. You notice that you are getting many small files (e.g., 5 KB each), even though your Buffer Size is set to 128 MB. Why is Firehose ignoring your size limit?
    - The Answer: It is likely hitting the Buffer Interval limit first.
    - The Logic: Firehose flushes data when either the Size limit (128 MB) OR the Time limit (e.g., 60 seconds) is reached.
    - The Scenario: If traffic is low, you won't accumulate 128 MB in 60 seconds. Firehose respects the timer and flushes whatever small amount of data it has to keep the stream 'fresh'.
    - The Fix: If file size is more important than latency (e.g., for historical archiving), increase the Buffer Interval to the maximum of 900 seconds (15 minutes).

1. What is the maximum size of a single record you can send to Firehose? How does this differ from Kinesis Data Streams?
    - The Answer: The record size limit for Firehose is 1,000 KB (1 MB).
    - Comparison: Kinesis Data Streams also has a 1 MB limit per record.
    - The Gotcha: While the input record is 1 MB, if you use a Lambda Transformation that increases the data size (e.g., enriching a log with extra metadata), the transformed record payload sent back to Firehose generally cannot exceed 6 MB.

1. We are using Dynamic Partitioning to group data by `customer_id`. One specific customer is sending malformed JSON that crashes the partitioning logic. Does this block the entire pipe for everyone else?
    - The Answer: No, if configured correctly, it won't block the pipe, but it can create an 'Error Bucket' mess.
    - The Mechanism: Firehose attempts to parse the JSON. If it fails (Parse Error) or the key is missing, it sends that specific record to the S3 Error Prefix (e.g., error/).
    - The Risk: If you don't monitor the Error Prefix, you might silently lose data for that customer.
    - Best Practice: Set up a CloudWatch Alarm on the `ParsingErrors` metric so we know immediately if a bad deployment or data source change is causing mass failures.

1. You are sending data to an HTTP Endpoint (e.g., Datadog or MongoDB Cloud). The destination is down (returning 500 errors). How long does Firehose retry before giving up?
    - The Answer: Firehose retries based on the Retry Duration setting.
    - Default: For HTTP endpoints, the default retry duration is usually 300 seconds (5 minutes), but it can be increased.
    - Exponential Backoff: It uses exponential backoff during retries.
    - Final Destination: If the endpoint is still down after the duration expires, the data is sent to the S3 Backup Bucket (if configured). If S3 Backup is disabled, the data is permanently lost. This is why S3 Backup is non-negotiable for production.

1. Explain the 'Lambda Payload Limit' in Firehose Transformations. What happens if your Lambda returns a payload larger than 6MB?
    - The Answer: The entire batch of records sent to Lambda and returned must fit within the 6 MB response limit.
    - The Failure: If the returned batch exceeds 6 MB, Firehose considers the transformation failed.
    - The Behavior: It treats the entire batch as 'ProcessingFailed' and dumps the original raw records to the processing-failed/ folder in S3.
    - The Fix: In the Firehose configuration, we must tune the Buffer Size for the Lambda trigger to ensure the input batch is small enough (e.g., 1-2 MB) so that even after enrichment, the output stays under 6 MB.

1. How do you handle 'Schema Evolution' in Firehose when converting JSON to Parquet? What happens if the incoming JSON gets a new field that isn't in the Glue Schema?
    - The Answer: Firehose relies on the AWS Glue Data Catalog for the schema.
    - Missing Field: If the JSON has a new `field x` but the Glue Schema doesn't, Firehose generally ignores/drops that field in the resulting Parquet file (depending on the SerDe).
    - Missing Value: If the Glue Schema requires a `field y` but the JSON doesn't have it, the conversion might fail or insert NULL.
    - Production Strategy: We must implement a 'Schema Registry' check upstream. If a developer changes the log format, they must update the Glue Table definition before deploying the app, otherwise, new data fields will silently disappear from the data lake.

## Error-Based Questions
1. You created a Firehose stream to dump logs into an S3 bucket. The stream status is ACTIVE. However, no data is appearing in S3. The Firehose CloudWatch logs show: `S3.AccessDenied`. You checked the IAM Role, and it has `S3FullAccess`. What is missing?
    - The Answer: The IAM Role permissions are likely correct, but the Trust Policy or Bucket Policy is blocking it.
    - Trust Policy: Does the IAM Role explicitly trust the Firehose Service (`firehose.amazonaws.com`) to assume it? If not, Firehose cannot 'put on the hat' to use the permissions.
    - Bucket Policy: Does the Destination Bucket have a policy that denies writes from outside the Bucket Owner's account (if cross-account) or requires specific encryption headers?
    - The Fix: Ensure the Role trusts the service, and the Bucket Policy allows the Role ARN.

1. Your developer complains: 'I sent the log to Firehose 2 minutes ago, but it's not in S3 yet! The service is broken.' You check the config: Buffer Size = 128 MB, Buffer Interval = 300 seconds. Is it broken?
    - The Answer: No, it is working as designed.
    - The Logic: Firehose buffers data to write larger files. It waits until either the size limit (128 MB) is met OR the time limit (300s / 5 mins) is passed.
    - The Explanation: If traffic is low, it won't hit 128 MB quickly. It will wait the full 5 minutes before flushing.
    - The Fix: If they need faster access, lower the Buffer Interval to 60 seconds (the minimum). Note that this creates more small files.

1. You use a Lambda function to enrich data in Firehose (e.g., add Geo-IP location). Suddenly, Firehose delivery lags by hours. You check the Lambda metrics: Duration has spiked to 5 minutes (max) and Errors are high. What is happening to the Firehose stream?
    - The Answer: The Lambda is blocking the Firehose delivery.
    - The Mechanism: Firehose invokes Lambda synchronously. If Lambda times out, Firehose retries.
    - The Bottleneck: If every batch times out, Firehose pauses delivery to retry the failed batches. The backlog grows.
    - The Fix: Figure out why the Lambda is slow and fix it (e.g., The Geo-IP API it calls is down).
    - Circuit Breaker: Update Lambda to catch the timeout/error and return the original record with a status `ProcessingFailed` instead of letting it time out. This tells Firehose 'This record failed, dump it to the error bucket and move on,' unblocking the pipe.

1. You configured Firehose to load data into Redshift. Data is arriving in the Intermediate S3 Bucket, but it is not showing up in the Redshift table. There are no errors in Firehose CloudWatch logs. Where do you look?
    - The Answer: You must check the `STL_LOAD_ERRORS` table inside Redshift.
    - The Workflow: Firehose first writes to S3, then issues a `COPY` command to Redshift.
    - The Error: If the `COPY` command fails (e.g., a string is too long for a `VARCHAR(10)` column), Redshift rejects the row silently (from the Firehose perspective) but logs it internally.
    - The Fix: Query `SELECT * FROM stl_load_errors` to find the specific column mismatch, then `ALTER TABLE` in Redshift to fix the schema.

1. You enabled Dynamic Partitioning to group data by `customer_id`. It works fine for 500 customers. Suddenly, you onboard a client with 10,000 unique device IDs sending data simultaneously. Firehose starts failing with `ThroughputExceeded`. You are well below the MB/sec limit. What limit did you hit?
    - The Answer: You hit the Active Partition Limit (Memory Buffer limit).
    - The Limit: Firehose can only actively buffer around 500 unique partitions simultaneously in memory.
    - The Crash: If 10,000 unique keys arrive in the same second, Firehose tries to open 10,000 buffers. It runs out of memory and throttles the request.
    - The Fix: Dynamic Partitioning is NOT for high-cardinality keys like DeviceID or UserID. It is for low-cardinality keys like Region or Hour. You must disable Dynamic Partitioning for this use case and handle partitioning in a post-processing step (e.g., regular Glue Job).

1. You have a Firehose stream writing to an encrypted S3 bucket. The stream status is Active. But the Firehose logs show: K`MS.NotFoundException` or `KMS.DisabledException`. You checked the KMS Key ID in the Firehose config, and it matches the key on the bucket. The key is enabled.
    - The Answer: The KMS Key likely belongs to a Different Region or the Firehose Role is missing 'GenerateDataKey'.
    - The Nuance: S3 Server-Side Encryption requires the writer (Firehose) to have permission to use the key.
    - The Trap: If you just allow `kms:Decrypt`, it will fail. Firehose needs `kms:GenerateDataKey` to write encrypted files.
    - The Fix: Update the KMS Key Policy to allow the Firehose IAM Role to perform `kms:GenerateDataKey` and `kms:Encrypt`.

1. You are converting JSON to Parquet using a Glue Schema. You added a new column `discount_code` to your JSON data. You updated the Glue Table Schema to include `discount_code`. However, Firehose is still writing Parquet files without the new column 2 hours later. Why?
    - The Answer: Firehose caches the Glue Schema definition.
    - The Mechanism: To save performance, Firehose doesn't check the Glue Catalog for every single record. It caches the schema version.
    - The Fix: You usually need to disable and re-enable the Format Conversion setting (or update the stream configuration) to force Firehose to refresh its schema cache immediately. Otherwise, it can take time to pick up the change.

1. You have a Kinesis Data Stream (KDS) feeding into Firehose. The KDS is handling the traffic fine (no Write Throttling). But Firehose is lagging behind by 30 minutes. You check Firehose limits, and you are well below the 5,000 records/sec limit. Why is Firehose slow?
    - The Answer: Firehose is being throttled on the Read side of the Kinesis Data Stream.
    - The Constraint: Firehose acts as a standard consumer. It shares the 2MB/sec read limit of the KDS shard with other consumers.
    - The Diagnosis: Check the Kinesis Data Stream metric `ReadProvisionedThroughputExceeded`.
    - The Cause: If you have 5 other apps reading from that KDS, Firehose is starving.
    - The Fix: Since Firehose doesn't support Enhanced Fan-Out (EFO) natively yet (in all contexts), you might need to scale up the number of KDS shards to provide more read bandwidth.