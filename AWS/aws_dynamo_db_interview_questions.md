# AWS Dynamo DB Interview Questions

## Basic Questions
1. What is Amazon DynamoDB?
    - Answer: Amazon DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability. It is designed to handle large amounts of data and support high-traffic applications.

1. What data models does DynamoDB support?
    - Answer: DynamoDB supports key-value and document data models. It allows for storing data in items (similar to rows) and attributes (similar to columns).

1. What is a primary key in DynamoDB?
    - Answer: A primary key uniquely identifies each item in a table. It can be either a partition key (simple primary key) or a composite primary key (partition key and sort key).

1. What is the difference between a partition key and a sort key?
    - Answer: A partition key is used to distribute data across partitions, while a sort key allows multiple items to be stored under the same partition key and are sorted by the sort key value.

1. What is a secondary index in DynamoDB?
    - Answer: A secondary index allows you to query data using an alternate key, different from the primary key. There are two types: Global Secondary Index (GSI) and Local Secondary Index (LSI).

1. How do you design a DynamoDB table for optimal performance?
    - Answer: Design the table with a well-defined primary key, minimize the use of large attributes, use appropriate indexes, and consider access patterns to optimize for read and write performance.

1. What is the significance of the Throughput setting in DynamoDB?
    - Answer: Throughput settings define the maximum number of read and write operations per second for a table. It ensures that the table can handle the expected load without throttling.

1. What are the different types of data types supported in DynamoDB?
    - Answer: DynamoDB supports various data types, including String, Number, Boolean, Binary, Null, List, Map, and Set.

1. What is a DynamoDB Stream?
    - Answer: DynamoDB Streams is a feature that captures changes to items in a table and provides a time-ordered sequence of these changes. It allows for triggering events in other AWS services like Lambda.

1. What are the best practices for designing a DynamoDB table schema?
    - Answer: Best practices include: understanding access patterns, choosing an appropriate primary key, using indexes wisely, minimizing attribute sizes, and leveraging DynamoDB Streams for real-time processing.

1. How does DynamoDB achieve low latency?
    - Answer: DynamoDB uses solid-state drives (SSDs) for storage, automatic data partitioning, and optimized data access patterns to achieve low-latency performance.

1. What are read and write capacity units in DynamoDB?
    - Answer: Read capacity units (RCUs) measure the number of strongly consistent reads per second, while write capacity units (WCUs) measure the number of writes per second. Each unit allows for reading or writing one item per second.

1. What is the difference between strongly consistent reads and eventually consistent reads?
    - Answer: Strongly consistent reads return the most up-to-date data, while eventually consistent reads may return stale data but are more efficient and consume fewer resources.

1. How can you monitor DynamoDB performance?
    - Answer: You can monitor performance using Amazon CloudWatch metrics, which provide insights into table activity, read/write capacity, throttling, and latency.

1. What is Adaptive Capacity in DynamoDB?
    - Answer: Adaptive Capacity automatically adjusts the provisioned throughput of your table in response to workload patterns, helping to prevent throttling and improve performance.

1. How do you implement fine-grained access control in DynamoDB?
    - Answer: Fine-grained access control can be implemented using IAM policies, enabling specific actions on particular items or attributes within a DynamoDB table.

1. What is a condition expression in DynamoDB?
    - Answer: A condition expression is a logical statement that must evaluate to true for a write operation to succeed, allowing for conditional updates and inserts.

1. How can you ensure data integrity in DynamoDB?
    - Answer: Data integrity can be ensured using transactions, conditional writes, and validating input data before performing operations on the database.

1. What is the purpose of DynamoDB Transactions?
    - Answer: DynamoDB Transactions allow you to perform multiple actions on one or more items as a single, all-or-nothing operation, ensuring consistency and atomicity.

1. How do you handle error retries in DynamoDB?
    - Answer: Error retries can be handled by implementing exponential backoff strategies for throttling errors and catching exceptions for conditional write failures.

1. What is the impact of using transactions on performance?
    - Answer: Using transactions may result in increased latency and reduced throughput compared to single-item operations, due to the overhead of ensuring atomicity and consistency.

1. Can you perform conditional updates with DynamoDB?
    - Answer: Yes, DynamoDB supports conditional updates using condition expressions, allowing updates to occur only if specific conditions are met.

1. What is the maximum size of a single item in DynamoDB?
    - Answer: The maximum size of a single item in DynamoDB is 400 KB, including all attribute names and values.

1. What are the different ways to query data in DynamoDB?
    - Answer: You can query data using the Query operation, Scan operation, and using secondary indexes. Queries retrieve items based on primary key values, while scans examine all items in a table.

1. What is a Query operation in DynamoDB?
    - Answer: The Query operation retrieves items from a table using the partition key and can filter results using the sort key or other attributes.

1. What is a Scan operation in DynamoDB?
    - Answer: The Scan operation examines every item in a table and can filter the results. It is less efficient than a Query, as it reads all items regardless of the primary key.

1. How do you filter results in a Query or Scan operation?
    - Answer: Results can be filtered using FilterExpression parameters, which apply conditions to limit the items returned from a Query or Scan.

1. What is the maximum number of items returned in a single Query or Scan request?
    - Answer: A single Query or Scan request can return a maximum of 1 MB of data, and if more data is available, you need to paginate the results.

1. What are the common error codes in DynamoDB?
    - Answer: Common error codes include `ProvisionedThroughputExceededException`, `ConditionalCheckFailedException`, `ResourceNotFoundException`, and `ThrottlingException`.

1. How can you troubleshoot performance issues in DynamoDB?
    - Answer: Troubleshooting can be done by monitoring CloudWatch metrics for read/write capacity, analyzing throttling events, reviewing query execution times, and adjusting throughput settings.

1. What is the significance of Throttling in DynamoDB?
    - Answer: Throttling occurs when requests exceed the provisioned capacity. It results in slower performance and can lead to errors if not managed properly.

1. What strategies would you use to optimize read performance in DynamoDB?
    - Answer: Strategies include using GSIs for alternative query patterns, caching frequently accessed items, minimizing item size, and optimizing data access patterns.

1. How can you minimize costs when using DynamoDB?
    - Answer: Minimize costs by using on-demand capacity for variable workloads, optimizing data models, using caching strategies, and setting up auto-scaling for provisioned capacity.

1. What is the difference between on-demand and provisioned capacity modes?
    - Answer: On-demand capacity automatically adjusts to your workload, charging per request, while provisioned capacity requires you to set read/write limits, charging based on those settings.

1. What are DynamoDB backups and how do they work?
    - Answer: DynamoDB backups create point-in-time snapshots of tables for data recovery. You can create on-demand backups or enable continuous backups for recovery options.

1. How can you restore data from a backup in DynamoDB?
    - Answer: Data can be restored from a backup by creating a new table from the backup or restoring the table to its original state if continuous backups are enabled.

1. What is DynamoDB Accelerator (DAX)?
    - Answer: DynamoDB Accelerator (DAX) is an in-memory caching service for DynamoDB that improves read performance for applications that require low-latency data access.

1. How can you implement caching for DynamoDB queries?
    - Answer: Caching can be implemented using DAX for in-memory caching or using external caching solutions like Redis or Amazon ElastiCache to store frequently accessed data.

1. What is auto-scaling in DynamoDB?
    - Answer: Auto-scaling automatically adjusts the provisioned read and write capacity of DynamoDB tables based on application traffic patterns and defined scaling policies.

1. How does data partitioning work in DynamoDB?
    - Answer: Data partitioning in DynamoDB distributes items across multiple partitions based on the partition key, allowing for horizontal scaling and efficient data retrieval.

1. What factors affect DynamoDB throughput?
    - Answer: Factors affecting throughput include the chosen primary key design, read/write patterns, the use of indexes, and the size of items being processed.

1. What is the importance of a good partition key design?
    - Answer: A good partition key design ensures even distribution of data across partitions, avoiding hot spots and improving overall performance and scalability.

1. How do you estimate the required read and write capacity for DynamoDB?
    - Answer: Capacity can be estimated by analyzing the expected number of read/write operations per second, item sizes, and access patterns to define appropriate throughput settings.

1. What is eventual consistency, and how does it work in DynamoDB?
    - Answer: Eventual consistency means that changes to data will propagate to all copies over time, and reads may return stale data temporarily. It provides better performance compared to strong consistency.

1. What is the maximum number of items you can have in a DynamoDB table?
    - Answer: There is no hard limit on the number of items in a DynamoDB table; you can scale it to accommodate billions of items as long as you provision sufficient capacity.

1. How do you handle large items that exceed the 400 KB limit in DynamoDB?
    - Answer: Large items can be split into multiple smaller items or stored as pointers in DynamoDB that reference data stored in Amazon S3 or other storage solutions.

1. What is the significance of item collections in DynamoDB?
    - Answer: Item collections allow for grouping related items under the same partition key but different sort keys, enabling efficient queries and data organization.

1. How can you ensure optimal read and write patterns in your DynamoDB design?
    - Answer: Optimal patterns can be ensured by analyzing access patterns, designing efficient primary keys, using secondary indexes, and caching frequently accessed data.

1. What is the purpose of the `UpdateItem` operation?
    - Answer: The `UpdateItem` operation modifies an existing item's attributes without replacing the entire item, allowing for incremental changes to be made.

1. How can you implement pagination in DynamoDB queries?
    - Answer: Pagination can be implemented using the `LastEvaluatedKey` returned by a Query or Scan operation, allowing subsequent requests to continue from where the last operation left off.

1. What is the `ConditionExpression` parameter in DynamoDB operations?
    - Answer: `ConditionExpression` is used to specify conditions that must be met for the operation to proceed, allowing for conditional writes and updates.

1. How do you handle duplicates in DynamoDB?
    - Answer: Duplicates can be handled by using unique identifiers as primary keys and employing conditional writes to check for existing items before insertion.

1. What are some potential pitfalls when using DynamoDB?
    - Answer: Pitfalls include improper primary key design, underestimating data access patterns, neglecting capacity planning, and misunderstanding eventual consistency.

## Scenario-Based Questions
1. You created a table for 'UserLogs' with Timestamp as the Primary Key. Why is this a terrible design for DynamoDB?
    - The Answer: Using a generic Timestamp as a Partition Key creates a Hot Partition (or Heat Map issue).
    - The Logic: DynamoDB partitions data based on the Partition Key. If the key is 'current time', all new writes hit the same partition (the 'current second' partition) while older partitions sit idle.
    - The Error: This creates a bottleneck. You are hammering one node while paying for the capacity of the whole table.
    - The Fix: We should use a Composite Key.
        1. Partition Key: UserID (Spread writes across many users).
        1. Sort Key: Timestamp (Order events for that user).
        1. This distributes writes evenly across the cluster.

 

1. What is the difference between a Scan and a Query? Why did your lead engineer ban the use of Scan in production?
    - The Answer: It comes down to Cost and Performance.
    - Query: Efficient. It goes directly to a specific Partition Key (like looking up a word in a dictionary index). It pays only for the data it reads.
    - Scan: Inefficient. It reads every single item in the entire table, regardless of filters.
    - Scenario: If you Scan a 1TB table to find 1 user, you pay to read 1TB of data. It is slow and burns through your Read Capacity Units (RCU) instantly.
    - Use Case: We only use Scans for full table exports (e.g., backups) or when we genuinely need to process 100% of the records.

 

1. We need to delete old logs after 30 days. Writing a script to `DeleteItem` every night is too expensive. Is there a free way?
    - The Answer: Yes, we use Time To Live (TTL).
    - The Feature: We define a specific attribute (e.g., `expiry_timestamp`) as the TTL attribute.
    - How it works: DynamoDB's background workers check this field. If `current_time > expiry_timestamp`, AWS deletes the item automatically.
    - The 'Free' Part: These background deletions do not consume Write Capacity Units (WCU). It is essentially free housekeeping.

1. You need to query your Users table by Email instead of UserID. You proposed adding a Local Secondary Index (LSI) now. Why did the deployment fail?
    - The Answer: **LSIs cannot be added to an existing table.**
    - LSI (Local): Must be created at table creation time. It shares the same Partition Key as the main table but uses a different Sort Key. It shares the WCU/RCU of the main table.
    - GSI (Global): Can be added any time. It copies data to a separate partition space with its own WCU/RCU settings.
    - The Fix: Since the table already exists, we must create a Global Secondary Index (GSI) on the Email column.

 

1. Your Lambda function, triggered by DynamoDB Streams, is processing the same record twice. How is this possible?
    - The Answer: DynamoDB Streams + Lambda has 'At Least Once' delivery.
    - The Scenario: The Lambda processed the record successfully but failed to report 'Success' back to the stream (network blip) or timed out right at the end. The Stream thinks it failed and re-sends the record.
    - The Fix: The Lambda logic must be Idempotent.
    - We check if `event_id` was already processed (e.g., in a separate Redis/DynamoDB table) before running the business logic. Alternatively, use `BatchItemFailures` to only retry specific failed messages in a batch.

1. You are using On-Demand Capacity. Suddenly, your writes are being Throttled (ProvisionedThroughputExceeded). I thought On-Demand scales infinitely?
    - The Answer: On-Demand scales, but not instantly.
    - The Limit: It can handle up to 2x your previous peak traffic immediately.
    - The Crash: If you go from 0 to 50,000 writes/second in 1 second (a massive spike), DynamoDB cannot split partitions fast enough. It takes up to 30 minutes to warm up new partitions.
    - The Fix: For known spikes (like a marketing launch), switch to Provisioned Mode and pre-warm the table, or introduce a queue (SQS) to smooth out the spike.

1. Explain 'Write Sharding'. When would you use it in a Data Pipeline?
    - The Answer: Write Sharding is used to solve the Hot Partition problem for high-cardinality aggregation.
    - The Problem: We want to count 'Votes' for 'Candidate A'. If we increment the key Candidate_A 10,000 times/sec, that single key becomes a hot spot (limit is 1,000 WCU/sec per partition).
    - The Solution: We append a random suffix (0-9) to the key: Candidate_A_0, Candidate_A_1... Candidate_A_9.
    - The Write: We randomly pick one shard to increment (dividing load by 10).
    - The Read: To get the total, we read all 10 shards and sum them up.

 

1. You have a Global Table replicating data from US-East to EU-West. A user updates their profile in US-East, then immediately refreshes the page (routed to EU-West) and sees old data. Why?
    - The Answer: Global Tables use Replication Latency (Eventual Consistency).
    - The Mechanism: DynamoDB asynchronously replicates changes to other regions. It usually takes 1-2 seconds.
    - The Race Condition: If the user moves faster than the speed of light (or network latency), they beat the replication.
    - The Fix:
        - UX: Show a 'Saving...' spinner for 2 seconds.
        - Architecture: Use 'Read-Your-Writes' consistency strategies (e.g., stick the user session to the region they wrote to for 5 minutes).

1. We are storing large JSON blobs (400KB) in DynamoDB. It's expensive and slow. How do you optimize this without changing the database?
    - The Answer: We should use the S3 Pointer Pattern (Claim Check Pattern).
    - The Issue: DynamoDB charges by 1KB chunks. A 400KB item costs 400 WCUs to write!
    - The Optimization:
        1. Store the actual 400KB JSON in S3.
        1. Store only the S3 Key (Metadata) in DynamoDB.
        1. The client reads the metadata from DynamoDB, gets the S3 path, and fetches the payload from S3.
    - Result: The DynamoDB write becomes 1KB (1 WCU), reducing costs by 400x.

 

1. Your application was read-heavy, so you enabled DAX (DynamoDB Accelerator) to cache reads. It worked great. Then, you noticed your Write Latency increased slightly (e.g., from 5ms to 8ms). The developer complains: 'I thought DAX makes everything faster?'
    - The Answer: DAX is a Write-Through Cache.
    - The Logic: When you write to DAX, it does two things:
    - Writes to the backend DynamoDB table.
    - Updates the item in the cache.
    - The Cost: DAX only returns 'Success' when both operations are done. This adds a tiny bit of overhead to writes in exchange for ensuring the cache is immediately consistent.
    - Takeaway: DAX speeds up Reads (microseconds), but it does not speed up Writes.

1. A junior dev accidentally deleted the production Users table. Panic ensues. You have Point-In-Time Recovery (PITR) enabled. You run the restore command to bring the table back. The application still crashes with `TableNotFoundException`. Why?
    - The Answer: DynamoDB Restores always create a New Table.
    - The Trap: You cannot restore data into the existing (or deleted) table name. AWS forces you to choose a new name (e.g., Users-Restored).
    - The Fix:
        1. Wait for the restore to finish.
        1. Update your application config to point to Users-Restored.
        1. Alternatively (slower), Create a script to copy data from Users-Restored back to a new table named Users.

1. You are using Provisioned Capacity. Traffic spikes, and you get throttled. You relied on Auto-Scaling to handle this, but it reacted too slowly. The throttle lasted for 10 minutes. Why?
    - The Answer: Auto-Scaling has a Warm-Up Time.
    - The Mechanism: CloudWatch alarms trigger Auto-Scaling. It typically waits for a few data points (e.g., 5-15 minutes of high usage) before triggering.
    - The Scale: Once triggered, it takes time to provision new capacity.
    - The Fix: For predictable spikes (e.g., TV commercials), use Scheduled Scaling. For unpredictable, spiky workloads, switch to On-Demand Mode, which reacts instantly.

 

1. You have a Main Table (Provisioned: 10,000 WCUs). You have a Global Secondary Index (GSI) on that table (Provisioned: 5 WCUs). You start a massive write job to the Main Table. Suddenly, writes to the Main Table fail with `ProvisionedThroughputExceeded`. But the Main Table has plenty of capacity! Why?
    - The Answer: This is GSI Backpressure.
    - The Rule: To maintain data consistency between the Table and the Index, if the GSI cannot keep up with the writes (because it only has 5 WCUs), DynamoDB throttles the Main Table.
    - The Logic: If it didn't throttle, the GSI would fall hopelessly behind, breaking the replication contract.
    - The Fix: Ensure GSI capacity always **matches or exceeds** the write capacity of the Main Table.

1. You are using Single Table Design. You have a User item (PK=USER#1) and Order items (PK=USER#1, SK=ORDER#A). You delete the User item using DeleteItem. However, the Order items remain in the database. Now you have orphaned data. How do you fix this?
    - The Answer: DynamoDB does not support Cascade Deletes (unlike SQL Foreign Keys).
    - The Solution: You must delete the children manually.
        1. Query: Query PK=USER#1 to find all related orders.
        1. Batch Delete: Collect all the Sort Keys (USER#1, ORDER#A, ORDER#B...) and issue a BatchWriteItem (or loop DeleteItem) to remove them all.
        1. Automation: Alternatively, rely on DynamoDB Streams to detect the 'User Delete' event and trigger a Lambda to clean up the children asynchronously.

1. A Lambda function triggered by DynamoDB Streams is crashing on a specific malformed record. The stream processing has stopped completely. New records are piling up, and the IteratorAge metric is skyrocketing. Why did the whole stream stop for one bad record?
    - The Answer: Streams are Ordered.
    - The Mechanism: DynamoDB guarantees order. It cannot skip Record A to process Record B, because Record B might depend on A.
    - The Block: If the Lambda fails for Record A, it retries... and retries... forever (until the data expires in 24 hours).
    - The Fix:
        1. Bisect on Failure: Configure the Event Source Mapping to split the batch to isolate the bad record.
        1. On-Failure Destination (DLQ): Configure the Lambda to send failed records to an SQS DLQ after X retries, allowing the stream to move on.

1. The 'Lost Update' Race Condition
    - The Scenario: Two admins open the same User Profile at the same time.
        1. Admin A changes 'Role' to 'Editor'.
        1. Admin B changes 'Status' to 'Inactive'.
        1. Admin A clicks Save.
        1. Admin B clicks Save. Result: Admin A's change is overwritten and lost. How do you prevent this in DynamoDB?
    - The Answer: Use Optimistic Locking with Conditional Writes.
    - The Setup: Add a version attribute to every item (initially 1).
    - The Write: When Admin A saves, the query is: UpdateItem SET role='Editor', version=2 WHERE version=1.
    - The Conflict: Admin A succeeds (Version becomes 2). When Admin B tries to save, his condition is WHERE version=1. This fails (`ConditionalCheckFailedException`) because the version is now 2.
    - The UX: The app tells Admin B: 'Data has changed. Please refresh and try again.'

1. The 'Transaction' Limit
    - The Scenario: You need to save an Order Header and 50 Order Items atomically. You use `TransactWriteItems`. It fails with `ValidationException`. Why?
    - The Answer: DynamoDB Transactions are limited to 100 items (formerly 25) in a single request.
    - The Scenario: If you have 1 Header + 50 Items, that's 51 items. It fits.
    - The Real Error: It fails if any of those items are in the same table and modified multiple times in the same transaction.
    - Also: If the total size exceeds 4MB.
    - The Fix: If you have > 100 items, you cannot use a single ACID transaction. You must break it into batches and handle consistency manually (e.g., using a 'Saga Pattern' with a 'Status=Pending' flag).

1. You chose Customer_ID as your Partition Key. One customer is huge (Amazon.com). They have millions of orders. Writes start failing for just that customer. You check throughput—it's fine. What is the hard limit you hit?
    - The Answer: You hit the 10GB Partition Size Limit.
    - The Constraint: In DynamoDB, a single Partition Key (and all its items combined) generally cannot exceed 10GB if the collection contains Local Secondary Index (LSI).
    - Without LSI: If you don't use LSI, partitions can split indefinitely, so size isn't a hard limit, but you might create a Hot Partition if you query it too much.
    - With LSI: If you have an LSI, the 10GB limit is strict. Once the Customer_ID collection hits 10GB, you cannot write new items.
    - The Fix: Remove the LSI (requires table recreation) or archive old data for that customer.

## Error-Based Questions
1. You deployed a new application. It worked fine in testing. In production, users are reporting 'Service Unavailable' errors, and your logs show `ProvisionedThroughputExceededException`. You checked the DynamoDB settings, and it says 'Write Capacity: 5'. What is happening, and how do you fix it quickly?"
    - The Answer: "You are driving faster than the speed limit you paid for.
    - The Cause: DynamoDB in 'Provisioned Mode' has a hard limit. You set it to 5 Write Capacity Units (WCU). This means you can only write 5KB of data per second. If 10 users try to save data at the same second, requests 6-10 get rejected (throttled).
    - The Fix:
        - Immediate: Switch the table to 'On-Demand Mode'. This instantly allows the table to handle any amount of traffic (you pay per request).
        - Long-term: If On-Demand is too expensive, calculate your actual traffic and increase the Provisioned Capacity to a safe number (e.g., 50 or 100) with Auto-Scaling enabled."

1. You are storing user profiles. A specific user updates their profile, and the application crashes with `ValidationException`: Item size has exceeded the maximum allowed size. Other users are fine. Why is this happening?"
    - The Answer: "DynamoDB has a strict 400KB limit for a single item (row).
    - The Cause: That specific user probably has a huge amount of data in one attribute (e.g., a list of 'History' that grew too long, or a base64 encoded image stored directly in the text field).
    - The Fix: S3 Offloading (Claim Check Pattern).
    - Store the large data (image/history) in an S3 Bucket.
    - In DynamoDB, store only the S3 Link/URL (pointer).
    - This keeps the DynamoDB item tiny (under 1KB) and fast."

 

1. You wrote a script to find all users from 'New York'. You used the Scan operation. It worked when the table had 100 users. Now the table has 1 million users, and the script times out or takes forever. Why?"
    - The Answer: "Scans are the enemy of performance.
    - The Cause: A Scan reads every single item in the table, one by one, to find the data. It's like reading a whole library to find one book. As the table grows, the Scan takes longer and costs more.
    - The Fix: Change the code to use a Query.
    - Ideally, you should have designed the table with City as a Key (or GSI). A Query jumps directly to 'New York' partitions and ignores the rest of the data. It is O(1) vs O(N)."

1. You have a table with 10,000 Provisioned Write Units (WCU). That's a lot. However, you are seeing Throttling even though you are only writing 500 items per second (well below the limit). Your Partition Key is Date (e.g., '2023-10-27'). Why are you being throttled?"
    - The Answer: "You have created a Hot Key.
    - The Logic: DynamoDB splits your data across many servers (partitions). If your Key is Date, 100% of your write traffic today is hitting one single partition (the 'Today' partition).
    - The Limit: A single partition cannot handle 10,000 WCUs. It is usually capped at 1,000 WCUs. The other 9,000 units are sitting idle on other servers (storing old dates).
    - The Fix: Change the Partition Key to something with High Cardinality (randomness), like UserID or OrderID. This spreads the traffic evenly across all 10,000 units."

1. You have a Main Table (Users) and a Global Secondary Index (GSI) on 'Email'. You provisioned the Main Table with 1,000 WCUs. You provisioned the GSI with only 10 WCUs (to save money). Suddenly, writes to the Main Table are failing. Why would a low setting on the Index break the Main Table?"
    - The Answer: "This is GSI Backpressure.
    - The Rule: DynamoDB guarantees that if a write succeeds, it will eventually appear in the GSI.
    - The Failure: If the GSI is too small (10 WCUs), it cannot keep up with the Main Table's speed. To prevent the GSI from falling days behind, DynamoDB throttles the Main Table to slow it down to the GSI's speed.
    - The Fix: Ensure the GSI capacity matches or exceeds the Main Table's write capacity."

 

1. You are trying to query a table. You want to filter where Name = 'John'. You run the query, and it fails with a syntax error saying Name is a reserved word. How do you query a column that has a reserved name?"
    - The Answer: "You must use Expression Attribute Names (Aliases).
    - The Cause: DynamoDB has reserved keywords (like NAME, DATE, STATUS, VALUE). You cannot use them directly in a query string.
    - The Fix:
    1. Define a placeholder: #nm maps to Name.
    1. Write the query using the placeholder: KeyConditionExpression: "#nm = :val".
    1. Pass the mapping in the API call."

1. You have DynamoDB Streams triggering a Lambda function. The Lambda processes the stream to update a search index. One 'bad' record (malformed JSON) enters the stream. The Lambda crashes when processing it. The Impact: The entire pipeline stops. No new records are processed for hours. The 'Iterator Age' metric spikes. Why did one bad record stop everything?"
    - The Answer: "DynamoDB Streams are Ordered.
    - The Logic: AWS ensures you process Record A before Record B. If Record A crashes the Lambda, DynamoDB retries Record A indefinitely (until it expires). It cannot skip to Record B.
    - The Fix:
        - BisectBatchOnFunctionError: Enable this setting. AWS will split the batch to isolate the bad record.
        - On-Failure Destination (DLQ): Configure the Lambda to send the failed record to an SQS Dead Letter Queue after X retries, and then move on, unblocking the stream."

1. You have an existing table designed with a Local Secondary Index (LSI). One of your customers is a 'Power User' with millions of orders. Suddenly, you cannot add any more orders for just that customer. The error is `ItemCollectionSizeLimitExceeded`. Everyone else is fine."
    - The Answer: "You hit the 10GB Partition Limit for LSIs.
    - The Constraint: If a table has an LSI, the collection of items sharing the same Partition Key (e.g., Customer-A) cannot exceed 10GB. This is a hard limit.
    - The Mistake: **Using LSIs is often considered a legacy anti-pattern for this exact reason.**
    - The Fix: You cannot remove an LSI from an existing table. You must:
    - Create a New Table without the LSI (use GSIs instead, which don't have this limit).
    - Migrate the data.
    - Switch the app to the new table."

1. You are using `TransactWriteItems` to update two tables atomically (Debit User A, Credit User B). The transaction fails frequently with `TransactionCanceledException: Conflict`. You checked, and nobody else is modifying User A. What is causing the conflict?"
    - The Answer: "It could be a Idempotency Token or GSI Contention."
    - Reason A (Contention): Even if User A isn't being modified, if you are updating an item that is part of a Hot Partition on a GSI, the transaction might fail due to lock contention on the index.
    - Reason B (Repeated Request): If your client retries the transaction too quickly with the same ClientRequestToken, and the first one is still 'Pending', the second one will fail with a Conflict.
    - The Fix: Implement exponential backoff (jitter) in your retry logic."

1. A user updates their account balance from $50 to $100. The application confirms 'Success'. The user immediately refreshes the page, and it shows $50. They refresh again 1 second later, and it shows $100. The user thinks the system is buggy. What is happening?"
    - The Answer: "You are using the default Eventual Consistency read model.
    - The Mechanism: When you write to DynamoDB, it acknowledges the write once it hits one storage node. It then replicates to the other two nodes in the background (usually takes < 100ms).
    - The Error: Your 'Read' request hit a node that hadn't received the update yet.
    - The Fix: For critical paths (like banking balance), use Strongly Consistent Reads (ConsistentRead=True in the API). This forces DynamoDB to check the leader node, guaranteeing the latest data (but costs 2x the Read Capacity)."

1. You enabled Time To Live (TTL) to delete old logs after 24 hours. You set the expiry timestamp correctly. However, you query the table and see thousands of items that expired 3 hours ago. Is TTL broken?"
    - The Answer: "No, TTL is not real-time.
    - The SLA: DynamoDB's background workers delete expired items within 48 hours of expiration. It is a 'best effort' background process to avoid consuming your provisioned throughput.
    - The Trap: You cannot rely on TTL for application logic (e.g., "If it exists, it's valid").
    - The Fix: Your application must filter the data itself: `if current_time > item.expiry: ignore_item()`."

1. You wrote a script to export data using Scan. The table has 5MB of data. Your script calls scan(). It returns 1MB of data. Your script assumes it's done because it got a list of items. The Error: You missed 80% of the table. Why?"
    - The Answer: "DynamoDB Operations are Paginated by 1MB limits.
    - The Mechanism: A single Scan/Query response returns a maximum of 1MB of data.
    - The Fix: You must check for the `LastEvaluatedKey` in the response.
        - If `LastEvaluatedKey` is present, it means there is more data.
        - You must loop and call scan() again, passing that key as `ExclusiveStartKey` to get the next page."

1. Your Lambda function works fine locally. You deploy it to a VPC (Private Subnet) to access RDS. Suddenly, your DynamoDB calls start timing out (ConnectTimeout). You checked Security Groups, and Outbound is set to All. Why?"
    - The Answer: "Lambda in a VPC loses internet access by default.
    - The Cause: DynamoDB is a public AWS service. To reach it, traffic must go out to the internet. If your Private Subnet has no NAT Gateway, the traffic drops.
    - The Fix: Instead of paying for a NAT Gateway, create a VPC Gateway Endpoint for DynamoDB. It's free and adds a route to your Route Table (pl-xxxx) allowing direct private access to DynamoDB from within the VPC."

1. You have a Global Table (Active-Active) in US and EU.
    - Scenario:
        - User A (in US) updates Item_1 setting Status='Pending'.
        - User B (in EU) updates Item_1 setting Status='Approved' at the exact same second. What happens? Does DynamoDB merge them?"
    - The Answer: "DynamoDB uses Last Writer Wins resolution.
    - The Logic: Global Tables do not have sophisticated merge logic (like git). It relies on timestamps.
    - The Result: Whichever update has the slightly later timestamp (even by microseconds) overwrites the other completely.
    - The Risk: If User A modified field 'Status' and User B modified field 'Name', the entire item is replaced. User B's update might wipe out User A's changes if not careful.
    - The Fix: Design your schema to avoid concurrent updates to the same item across regions, or use specific Conflict-free Replicated Data Type (CRDT) strategies in the app layer."

1. You rely on Burst Capacity to handle morning spikes. Usually, your table is idle at night, building up credits. One morning, the spike hits, and you get throttled immediately. No burst credits were used. What happened the night before?"
    - The Answer: "You might have performed a Background Maintenance Task.
    - The Concept: DynamoDB allows you to burst up to 300 seconds of unused capacity.
    - The Trap: If you ran a nightly backup script, a migration job, or a heavy scan just before the morning spike, you consumed all your 'banked' burst credits.
    - The Fix: Separate 'Operational' traffic from 'Analytics' traffic (e.g., export to S3 for analytics instead of scanning the live table) to preserve burst capacity for real users."

 

1. You have a table that is heavily throttled on one specific Partition Key (PK='Product_A'). You decide to double the Provisioned WCU for the table (from 1,000 to 2,000). The throttling does not stop. Why?"
    - The Answer: "Increasing Table Capacity does not always fix Single Partition Heat.
    - The limit: A single physical partition is hard-capped (e.g., 3,000 RCUs / 1,000 WCUs).
    - The Situation: Even if you provision 1,000,000 WCUs for the table, if all traffic is directed at Product_A (which lives on one node), you are limited by the physical hardware of that one node.
    - The Fix: You must implement Write Sharding (e.g., Product_A_1, Product_A_2) to split the hot key across multiple physical partitions."