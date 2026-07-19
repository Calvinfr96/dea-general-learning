# AWS Kinesis Data Stream Interview Questions

## Basic Questions
1. What is Amazon Kinesis Data Streams?
    - Answer: Amazon Kinesis Data Streams is a fully managed service that allows you to collect, process, and analyze real-time, streaming data. It can handle hundreds of thousands of records per second and provides the capability to build real-time applications.

1. What are the main components of Kinesis Data Streams?
    - Answer: The main components include streams, shards, records, and partitions. Streams consist of multiple shards, which store records. Each record contains a data blob, a partition key, and a sequence number.

1. How does Kinesis Data Streams ensure data durability?
    - Answer: Kinesis replicates data across multiple Availability Zones in a region, ensuring that it is durable and highly available. Data is retained for a configurable period, allowing applications to reprocess it if needed.

1. What is a shard in Kinesis Data Streams?
    - Answer: A shard is a uniquely identified group of data records in a Kinesis stream. Each shard has a fixed capacity for ingesting data (up to 1 MB per second) and a maximum of 1,000 records per second for reads.

1. What is a record in Kinesis Data Streams?
    - Answer: A record is the basic unit of data in Kinesis. It consists of a data blob (up to 1 MB), a partition key, and a sequence number. Records are stored in shards.

1. How do you ingest data into Kinesis Data Streams?
    - Answer: Data can be ingested using the AWS SDKs, the Kinesis Data Streams API, AWS CLI, or third-party libraries. Data producers send records to a specified stream.

1. What is a partition key, and how does it affect data distribution?
    - Answer: A partition key is a string used to group related records within a shard. Kinesis uses the partition key to determine which shard a record belongs to by hashing the key. This ensures that records with the same partition key are sent to the same shard.

1. What are the advantages of using Kinesis Data Streams for real-time data ingestion?
    - Answer: Advantages include high throughput, scalability, low-latency processing, integration with other AWS services, and the ability to replay and reprocess data.

1. What is the maximum retention period for records in Kinesis Data Streams?
    - Answer: The maximum retention period is 365 days, with the minimum being 24 hours. You can configure the retention period based on your application's requirements.

1. How can you monitor data ingestion in Kinesis Data Streams?
    - Answer: You can monitor data ingestion using Amazon CloudWatch metrics, which provide insights into the number of records ingested, read/write latency, and shard iterator age.

1. What are the different ways to process data from Kinesis Data Streams?
    - Answer: Data can be processed using AWS Lambda, Kinesis Data Firehose, Amazon Kinesis Data Analytics, or custom consumers built using the Kinesis Client Library (KCL).

1. How does Kinesis Data Streams support real-time analytics?
    - Answer: Kinesis Data Streams allows you to process and analyze data in real-time, enabling you to create applications that respond immediately to data changes, such as alerting systems or dashboard updates.

1. What is the purpose of the `GetRecords` API call in Kinesis?
    - Answer: The `GetRecords` API call retrieves data records from a specified shard in a Kinesis stream. It returns a batch of records along with a next shard iterator for continued reading.

1. How do you handle duplicate records in Kinesis Data Streams?
    - Answer: Applications should implement logic to deduplicate records, such as using unique identifiers in the records and maintaining state in a database or cache to track processed records.

1. What factors determine the number of shards in a Kinesis Data Stream?
    - Answer: Factors include the expected data ingestion rate (in records/second), the size of the records, and the read throughput requirements. Each shard can handle up to 1 MB/s for writes and 2 MB/s for reads.

1. How can you increase the throughput of a Kinesis Data Stream?
    - Answer: Throughput can be increased by adding more shards to the stream, optimizing the partition keys to achieve even data distribution, and scaling the application processing the data.

1. What is the maximum number of shards allowed in a Kinesis Data Stream?
    - Answer: The default limit is 500 shards per stream, but this can be increased by requesting a service limit increase from AWS.

1. What is the role of the `DescribeStream` API call?
    - Answer: The `DescribeStream` API call retrieves the details of a specified Kinesis stream, including its status, the number of shards, and the shard iterator types.

1. How does Kinesis Data Streams handle back pressure in data processing?
    - Answer: Kinesis can apply back pressure by allowing consumers to slow down processing if they can't keep up with incoming data. Consumers can control their read rate and use throttling to manage back pressure.

1. How do you change the retention period of records in Kinesis Data Streams?
    - Answer: You can change the retention period using the AWS Management Console, AWS CLI, or SDKs by modifying the stream's retention configuration.

1. What happens when the retention period expires for records in Kinesis Data Streams?
    - Answer: Once the retention period expires, the records are automatically deleted from the stream and are no longer accessible for processing.

1. How can you reprocess data from Kinesis Data Streams?
    - Answer: You can reprocess data by using a new application instance that reads from the stream using an earlier shard iterator or by leveraging Kinesis Data Firehose to send data to a destination for later analysis.

1. What is the purpose of the `GetShardIterator` API call?
    - Answer: The `GetShardIterator` API call returns a shard iterator, which is a pointer to the position in the shard where data can be read. It allows consumers to fetch records starting from a specific position.

1. How do you handle late-arriving data in Kinesis Data Streams?
    - Answer: Late-arriving data can be managed by implementing windowing logic in Kinesis Data Analytics or by storing the data in a persistent store for later processing.

1. What encryption options are available for Kinesis Data Streams?
    - Answer: Kinesis Data Streams supports server-side encryption using AWS KMS, which encrypts data at rest. Additionally, data can be encrypted in transit using HTTPS.

1. How can you ensure data privacy in Kinesis Data Streams?
    - Answer: Data privacy can be ensured by encrypting data at rest and in transit, using IAM policies to control access, and auditing access logs for monitoring.

1. How do you manage data retention and compliance in Kinesis Data Streams?
    - Answer: Data retention can be configured according to compliance requirements, and periodic audits can ensure that data is retained or deleted according to policies.

1. What is the difference between Kinesis Data Streams and Kinesis Data Firehose?
    - Answer: Kinesis Data Streams is used for real-time data processing, while Kinesis Data Firehose is a fully managed service for loading streaming data into data lakes and analytics services. Think of Data Streams as a highway and Data Firehose as an off-ramp.

1. How do you handle errors in data processing with Kinesis Data Streams?
    - Answer: Errors can be managed by implementing retries in the consumer application, logging failed records, and potentially sending problematic records to a dead-letter queue for further investigation.

1. What are some common metrics to monitor in Kinesis Data Streams?
    - Answer: Common metrics include Incoming Records, Incoming Bytes, Read Provisioned Throughput Exceeded, Write Provisioned Throughput Exceeded, and Iterator Age.

1. What is the significance of Iterator Age in Kinesis Data Streams?
    - Answer: Iterator Age measures the time that records remain in the stream before being read by consumers. High iterator age indicates that consumers are lagging in processing data.

1. What is a dead-letter queue (DLQ), and how does it relate to Kinesis Data Streams?
    - Answer: A dead-letter queue is a queue that receives messages that could not be processed successfully. It can be used in conjunction with Kinesis to store problematic records for later analysis.

1. What is Enhanced Fan-Out in Kinesis Data Streams?
    - Answer: Enhanced Fan-Out allows multiple consumers to read from a single shard in parallel without affecting the read throughput of other consumers. Each consumer gets its own dedicated read throughput.

1. How can you implement schema evolution in Kinesis Data Streams?
    - Answer: Schema evolution can be managed by using a versioning strategy for data records and processing applications that can handle different schema versions.

1. What is the significance of the sequence number in Kinesis Data Streams?
    - Answer: The sequence number is a unique identifier for each record within a shard. It helps maintain the order of records and allows consumers to track processing progress.

1. How do you implement batching in Kinesis Data Streams?
    - Answer: Batching can be implemented in consumers by aggregating multiple records into a single batch before processing, reducing overhead and improving throughput.

1. How do you optimize the performance of Kinesis Data Streams?
    - Answer: Performance can be optimized by carefully choosing partition keys to distribute load evenly, tuning the number of shards based on expected throughput, and minimizing record sizes.

1. What are the trade-offs between using Kinesis Data Streams and Apache Kafka?
    - Answer: Kinesis is a fully managed service with built-in integrations and less operational overhead, while Kafka offers greater flexibility and custom configurations. The choice depends on specific use cases and team expertise.

1. How do you manage and monitor shard splitting in Kinesis Data Streams?
    - Answer: Shard splitting can be monitored using CloudWatch metrics and managed through the AWS Management Console or CLI, enabling scaling of shards based on throughput demands.

1. What is the role of the `PutRecord` API call?
    - Answer: The `PutRecord` API call is used to add a single data record to a specified Kinesis Data Stream, providing the data blob, partition key, and optional sequence number.

1. How does Kinesis Data Streams handle scaling when there are sudden spikes in traffic?
    - Answer: Kinesis Data Streams can be manually scaled by adding shards in anticipation of spikes. Enhanced Fan-Out can also help manage increased read traffic.

1. What are common reasons for throttling in Kinesis Data Streams?
    - Answer: Throttling can occur when the read or write throughput limits for shards are exceeded, which can be due to sudden spikes in traffic or insufficient shard capacity.

1. How do you manage the lifecycle of Kinesis Data Streams?
    - Answer: The lifecycle is managed by configuring retention periods, monitoring shard usage, and periodically cleaning up unused streams to avoid unnecessary costs.

1. What are the implications of running multiple consumers on a single Kinesis Data Stream?
    - Answer: Running multiple consumers can increase processing throughput, but they may also compete for resources, potentially leading to throttling if the stream's capacity is exceeded.

1. How can you identify and resolve processing bottlenecks in Kinesis Data Streams?
    - Answer: Bottlenecks can be identified by analyzing CloudWatch metrics, looking for high iterator ages or throttling events, and optimizing the processing logic or increasing shard capacity.

1. How can you optimize shard utilization in Kinesis Data Streams?
    - Answer: Shard utilization can be optimized by evenly distributing partition keys, adjusting the number of shards based on throughput demands, and avoiding hot shards.

1. What is the impact of small record sizes on Kinesis Data Streams performance?
    - Answer: Small record sizes may lead to inefficient use of shards, as the overhead of managing many small records can increase processing costs. Batching records can improve efficiency.

1. How do you handle large data records in Kinesis Data Streams?
    - Answer: Large records can be handled by splitting them into smaller chunks before ingestion, or using Amazon S3 to store larger objects and sending metadata to Kinesis.

1. What is the importance of choosing the right partition key?
    - Answer: Choosing the right partition key ensures even data distribution across shards, preventing hot spots and ensuring optimal read and write throughput.

1. How can you tune the read capacity of a Kinesis Data Stream?
    - Answer: Read capacity can be tuned by adding shards to the stream and implementing Enhanced Fan-Out to allow multiple consumers to read from the same shard concurrently.

1. What are the recommended practices for managing Kinesis Data Streams costs?
    - Answer: Recommended practices include monitoring shard utilization, optimizing record sizes, avoiding excessive data retention, and using Kinesis Data Firehose for optimized storage solutions.

1. How do you design a Kinesis Data Stream application for high availability?
    - Answer: High availability can be achieved by distributing shards across multiple Availability Zones, implementing retries in processing logic, and using monitoring and alerting.

1. What is the significance of throughput limits in Kinesis Data Streams?
    - Answer: Throughput limits define the maximum data ingestion and consumption capacity of shards, guiding architects to provision resources appropriately based on expected workloads.

1. How do you implement data versioning in Kinesis Data Streams?
    - Answer: Data versioning can be implemented by including version identifiers in the record data or by maintaining separate streams for different data versions.

1. What are the best practices for data serialization in Kinesis Data Streams?
    - Answer: Best practices include using efficient serialization formats like Avro or Protocol Buffers, minimizing payload size, and ensuring backward compatibility.

## Scenario-Based Questions
1. You used Kinesis Data Streams. Why not just use SQS (Simple Queue Service)? It's cheaper and easier.
    - The Answer: The decision came down to Real-Time Analytics and Multiple Consumers.
    - Multiple Consumers: SQS is 'Work Queue' style. Once a worker reads a message, it deletes it. Only one person gets the letter. Kinesis is 'Pub/Sub'—multiple apps (Analytics, Archival, Dashboard) can all read the same stream of data simultaneously.
    - Ordering: Kinesis guarantees order within a shard. SQS (Standard) does not guarantee order. SQS FIFO does, but has lower throughput limits.
    - Simple Analogy: SQS is like a checklist; once a task is done, it's crossed off. Kinesis is like a CCTV tape recording; multiple people can watch the replay, pause, or rewind it independently.

1. What is a 'Shard' in Kinesis, and how did you decide how many you needed?
    - The Answer: A Shard is the base unit of throughput. It's like a 'lane' on a highway.
    - The Math: One Shard provides:
        - Write: 1 MB/sec or 1,000 records/sec.
        - Read: 2 MB/sec.
    - Calculation: We estimated our peak ingestion rate. If we expect to ingest 4.5 MB of data per second, we need at least 5 Shards ($4.5 / 1 = 4.5$, round up).
    - Real World: We monitored the IncomingBytes metric. If it got close to the limit, we split the shards to add more lanes.

1. What happens to the data if your consumer application crashes for an hour? Is the data lost?
    - The Answer: No, the data is safe because of the Retention Period.
    - Default: Kinesis stores data for 24 hours by default.
    - Configurable: We can extend this up to 365 days (though usually 7 days is enough).
    - Recovery: When our consumer app restarts, it looks at its 'Checkpoint' (managed by KCL/DynamoDB), realizes it is 1 hour behind, and starts reading from where it left off to catch up.

1. We are seeing a 'Hot Shard' issue where one shard is throttled while others are empty. What caused this, and how do you fix it?
    - The Answer: This is caused by a Poor Partition Key.
    - The Cause: If we used `customer_id` as the partition key, and one huge customer (e.g., 'Amazon') sends 90% of the traffic, all that data goes to Shard #1. It gets overwhelmed (`WriteProvisionedThroughputExceeded`), while Shard #2 and #3 sit idle.
    - The Fix:
        1. Immediate: Split the hot shard into two (Re-sharding) to double the capacity for that key range.
        1. Long Term: Change the Partition Key to something with higher cardinality (more randomness), like transaction_id or append a random suffix to the `customer_id` (cust123-1, cust123-2) to distribute the load evenly.

1. Did you use the Kinesis SDK (`PutRecord`) or the Kinesis Producer Library (KPL)? Why?
    - The Answer: We used the KPL for efficiency.
    - The Problem: Sending one HTTP request for every tiny log line (e.g., 50 bytes) is inefficient and expensive due to network overhead.
    - The KPL Solution:
        1. Aggregation: It packs multiple user records into one Kinesis record.
        1. Collection: It buffers records and sends them in a multi-record batch.
    - The Trade-off: It introduces a slight delay (latency) while buffering, but it drastically increases throughput and lowers cost.

1. What is `IteratorAgeMilliseconds`? Why is it the most critical metric for a Data Engineer?
    - The Answer: It measures Consumer Lag.
    - Definition: It is the difference between 'Time the record was created' and 'Time the record was processed'.
    - Scenario: If `IteratorAge` is 0, we are real-time. If it spikes to 3,600,000 ms (1 hour), it means our Lambda/Consumer is too slow and falling dangerously behind.
    - Action: If this spikes, we need to either optimize the consumer code (make it faster) or increase the number of shards and consumers (parallelize).

1. We have 5 different teams wanting to read the same stream (Analytics, Fraud, Marketing, Backup, Logs). We are hitting `ReadProvisionedThroughputExceeded`. How do we solve this without duplicating the data?
    - The Answer: We need to enable Enhanced Fan-Out (EFO).
    - The Problem: Standard consumers share the 2 MB/sec read limit of a shard. If you have 5 consumers, they each get only 0.4 MB/sec, causing throttling.
    - The Solution: EFO gives each registered consumer its own dedicated 2 MB/sec pipe.
    - Mechanism: It pushes data over HTTP/2 directly to the consumer, reducing latency to ~70ms.
    - Cost: It costs extra, but it isolates the teams. The Marketing team's heavy read load will no longer impact the Fraud team's detection speed.

1. How does the Kinesis Client Library (KCL) track which records have been processed? What happens if the tracking fails?
    - The Answer: KCL uses a DynamoDB Table for check-pointing.
    - Mechanism: For every app, KCL creates a DynamoDB table. It stores the ShardID and the SequenceNumber (checkpoint) of the last processed record.
    - Lease Management: Workers use this table to 'lease' shards. If Worker A dies, it stops updating the lease. Worker B sees the lease expire in DynamoDB and takes over that shard.
    - Production Risk: If the DynamoDB table is provisioned too low, KCL gets throttled on writes. The application will crash or process duplicate data because it can't save its checkpoint. **We must always set DynamoDB to On-Demand mode for KCL tables**.

1. Explain the 'Re-sharding' process. Is it instantaneous? Does it interrupt the stream?
    - The Answer: Re-sharding (Splitting or Merging) is not instantaneous.
    - The State: When we split Parent Shard A into Child Shards B and C:
        1. Shard A becomes 'Closed' (Read-only).
        1. Data flows into B and C.
        1. The consumer must finish reading all data left in A before it starts reading B and C to maintain order.
    - Impact: There is no interruption to ingestion (writers keep writing), but consumers might see a brief blip in latency as they switch from the parent to child shards.
    - Limit: We can't just 'double' capacity instantly. Re-sharding is a sequential API operation.

1. You have experience with Apache Kafka. Why would a company choose AWS Kinesis over running Kafka on EC2 or using Amazon MSK (Managed Streaming for Kafka)?
    - The Answer: It usually comes down to Operational Overhead vs. Control.
    - Kinesis (Serverless): I don't manage servers, brokers, or disk space. I just say 'I need 5 shards,' and it works. It is easier to set up and integrates natively with Lambda.
    - Kafka/MSK (Cluster-based): Gives you more control (longer retention, custom configuration), but you still have to manage 'brokers' and storage scaling.
    - Decision: For a team of Data Engineers who want to focus on code and not infrastructure, Kinesis is the better choice. If the company is already migrated from an on-premise Kafka cluster, MSK might be better to avoid rewriting code.

1. How do you ensure the data inside the stream is encrypted? We are dealing with PII (Personally Identifiable Information).
    - The Answer: We enable Server-Side Encryption (SSE) using AWS Key Management Service (KMS).
    - How it works: When a producer sends data (`PutRecord`), Kinesis encrypts it before writing it to disk. When a consumer reads it, Kinesis decrypts it.
    - Important Note: This encryption happens at rest. For data in transit (moving from producer to Kinesis), we rely on HTTPS/TLS endpoints, which are standard for AWS SDKs.

1. Your Lambda function processes data from Kinesis. The processing logic is slow (complex math), causing the iterator age to spike. You can't add more shards because the data volume doesn't justify it. How do you speed up the Lambda processing?
    - The Answer: I would use Parallelization Factor.
    - The Constraint: By default, only one Lambda instance processes a shard at a time to guarantee order.
    - The Feature: Parallelization Factor allows Kinesis to launch multiple concurrent Lambda instances (up to 10) for a single shard.
    - How it works: It’s like opening multiple checkout counters for a single line of customers.
    - Trade-off: It maintains order by 'Key' but processes different keys in parallel. This is a quick way to increase throughput without the cost/complexity of re-sharding.

1. Kinesis provides 'At-Least-Once' delivery. What does that mean for your downstream SQL database? How do you handle it?
    - The Answer: It means Duplicate Records are possible.
    - Scenario: A worker processes a record, writes to the DB, but crashes before it can tell Kinesis 'I finished'. Kinesis thinks the job failed and re-sends the same record to a new worker.
    - The Impact: If I blindly insert into the database, I might count a sale twice.
    - The Solution (Idempotency):
        1. Unique Keys: Use the Kinesis `SequenceNumber` or a business ID (like `OrderID`) as the Primary Key in the target DB. An `INSERT` attempt will fail if it exists (or we use `UPSERT`).
        1. Logic Check: In the code, check if `record_id` exists: skip else: write.

1. You are getting a `ProvisionedThroughputExceededException` on the Write side. You check the graphs, and you are only sending 500 KB/sec (limit is 1 MB/sec). Why are you being throttled?
    - The Answer: We are likely hitting the Records Per Second (RPS) limit.
    - The Limits: A shard has two write limits:
        - Bandwidth: 1 MB/sec.
        - Count: 1,000 records/sec.
    - The Scenario: If our application sends thousands of tiny messages (e.g., 50 bytes each), we will hit the 1,000 RPS limit long before we hit the 1 MB bandwidth limit.
    - The Fix: We must implement Aggregation (using KPL or manual buffering) to combine multiple small records into one larger Kinesis record (e.g., 100 small logs into one 5KB record). This drops the RPS count drastically.

## Error-Based Questions
1. You wrote a Python script to push logs to Kinesis. It works fine on your laptop. When you deploy it to production (where traffic is 10x higher), the logs are full of `ProvisionedThroughputExceededException`. You are only sending 500 records per second. Why is it failing?
    - The Answer: You are hitting the Shard Limits.
    - The Rule: One Shard supports 1 MB/sec OR 1,000 records/sec for writing.
    - The Catch: Even if you are below the 1,000 records limit, if your log messages are large (e.g., 2KB each), 500 records * 2KB = 1 MB. You hit the bandwidth limit.
    - The Immediate Fix:: Implement Retries with Exponential Backoff in the producer code.
    - Scale: Increase the number of shards (Re-sharding) to provide more 'lanes' for the traffic.

1. You are trying to send a large JSON object (900KB) to Kinesis. The documentation says the limit is 1MB. However, the PutRecord call fails saying the payload is too large. Why?
    - The Answer: The 1MB limit includes the Partition Key and the Base64 Encoding overhead.
    - The Math: When you send binary data, encoding it to Base64 increases the size by ~33%. A 900KB file becomes ~1.2MB on the wire.
    - The Fix: Compress: GZIP the data before sending it.
    - Split: If it's still too big, store the data in S3 and just send the S3 URL (Reference Pointer) through Kinesis.

1. You are monitoring your pipeline. The `GetRecords.IteratorAgeMilliseconds` metric jumps from 0 to 3,600,000 (1 hour) and keeps rising. The consumer is not crashing; it's just 'slow'. What is the risk?
    - The Answer: This is Consumer Lag, and the risk is Data Loss.
    - The Concept: Iterator Age measures how old the last processed record is. If it hits the Retention Period (default 24 hours), the oldest data at the front of the stream will expire and disappear before your consumer can read it.
    - The Fix:
        - Parallelize: Increase the number of shards and run more consumer instances (1 consumer per shard).
        - Optimize Code: The process logic (e.g., writing to DB) is too slow. Use batch writes or async processing.

1. You have 10 shards. You configured the Partition Key to be the Customer_ID. One specific shard (Shard-004) is constantly throttled on writes, while the other 9 are empty. Why?
    - The Answer: You have a Data Skew issue caused by a 'Whale' customer.
    - The Cause: If one customer ('Amazon') generates 90% of your traffic, and you partition by Customer_ID, all that data goes to Shard-004. That single lane is jammed, while others are empty.
    - The Fix:
        - Randomize (Short term): Append a random suffix to the Partition Key (Amazon-1, Amazon-2) to spread that customer's data across multiple shards.
        - Split: Explicitly split Shard-004 into two new shards to double its capacity.

1. Your Kinesis Consumer (KCL) keeps crashing and restarting. The logs show: `ProvisionedThroughputExceededException` from DynamoDB. Why is Kinesis talking to DynamoDB?
    - The Answer: The Kinesis Client Library (KCL) uses a DynamoDB Lease Table to track which records it has processed (Check-pointing).
    - The Cause: If your consumer processes records very quickly and checkpoints too frequently (e.g., after every single record), it spams DynamoDB with write requests, exceeding the table's capacity.
    - The Fix:
        - Tune Check-pointing: Only checkpoint periodically (e.g., every 100 records or every 1 minute), not every record.
        - Scale Dynamo: Switch the DynamoDB table to On-Demand Capacity mode.

1. Your fraud detection system flagged the same transaction twice. You checked the producer logs: it sent the record once. You checked the consumer logs: it processed it twice. How did Kinesis duplicate the data?
    - The Answer: Kinesis guarantees At-Least-Once delivery. Duplicates usually happen during Consumer Failure.
    - The Sequence:
        1. Consumer reads Record A.
        1. Consumer processes Record A (saves to DB).
        1. Consumer Crashes before it can update the Checkpoint in DynamoDB.
        1. Consumer Restarts -> Reads the last Checkpoint (which is before Record A) -> Reads Record A again.
    - The Fix: You must design the consumer to be Idempotent. Use the `SequenceNumber` or `TransactionID` as a Primary Key in your database so the second write fails or overwrites harmlessly.

1. You split a Shard (Parent) into two new Shards (Children). Your consumer application suddenly stops receiving new data for 5 minutes, then resumes. Why was there a pause?
    - The Answer: This is correct KCL behavior to preserve Order.
    - The Logic: When a shard splits, data exists in the 'Parent' (old) and 'Children' (new).
    - The Rule: The KCL must finish processing all records in the Parent Shard before it opens the Children Shards.
    - The Pause: If your consumer was lagging behind on the Parent Shard, it spends 5 minutes clearing that backlog. During this time, it refuses to touch the new data in the Child shards to ensure Record 1 (Parent) is processed before Record 2 (Child).

1. The producer team decided to use Kinesis Producer Library (KPL) to improve performance. The consumer team (using a standard Python Lambda) immediately complains that the incoming data looks like binary garbage characters (]...).
    - The Answer: The producer enabled Aggregation, but the consumer is not De-aggregating.
    - The Mechanism: KPL bundles multiple user records into one Kinesis record (using Google Protocol Buffers) to save costs.
    - The Fix: The consumer cannot just read the payload string. They must use a library (like aws-kinesis-agg in Python) to 'unpack' the Protobuf wrapper and extract the individual records inside.

1. A downstream system was down for 30 hours. You fixed it, brought it back up, and it started reading from Kinesis. However, the business team says 6 hours of data is missing completely. The Stream Retention is set to the default.
    - The Answer: The default retention period is 24 hours.
    - The Issue: Since the consumer was down for 30 hours, the first 6 hours of data (Hours 0-6) expired and were deleted by Kinesis before the consumer could come back online to read them.
    - The Fix: You cannot recover that data (unless you had a backup in S3/Firehose). To prevent this in the future, increase the Data Retention Period to 7 days (or up to 365 days) using the `IncreaseStreamRetentionPeriod` API.

1. You set up a Lambda function to process Kinesis records. If the processing is successful, the Lambda writes the result to Stream B. However, you accidentally configured the Lambda to write back to Stream A (the source). What happens?
    - The Answer: You created an Infinite Feedback Loop.
    - The Cycle:
        1. Lambda reads Record 1 from Stream A.
        1. Lambda writes Result 1 to Stream A.
        1. This 'Write' is a new event -> Triggers Lambda again.
        1. Lambda reads Result 1 -> Writes Result 1 (Copy) to Stream A.
    - The Impact: Your shard throughput will max out instantly (`WriteProvisionedThroughputExceeded`), and your costs will explode.
    - The Fix: Immediately disable the Lambda trigger (Event Source Mapping) to stop the bleeding, then fix the destination stream ARN in the code.