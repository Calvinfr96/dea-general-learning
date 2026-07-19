# AWS SQS Interview Questions

## Basic Questions
1. What is AWS SQS?
    - Answer: Amazon Simple Queue Service (SQS) is a fully managed message queuing service that enables decoupling and scaling of microservices, distributed systems, and serverless applications. It allows you to send, store, and receive messages between services without losing them.

1. What are the two types of SQS queues?
    - Answer: The two types are Standard Queues (which offer high throughput with **at-least-once** delivery and best-effort ordering) and FIFO Queues (which guarantee **exactly-once** processing and strict message ordering).

1. How does SQS guarantee message delivery?
    - Answer: For Standard Queues, SQS guarantees at-least-once delivery, meaning messages might be delivered more than once but never lost. For FIFO Queues, SQS ensures exactly-once processing.

1. What is the maximum size of a message in SQS?
    - Answer: The maximum size of a single message is 256 KB in SQS. However, you can send larger payloads using the SQS Extended Client Library that stores payloads in S3 and uses SQS to reference them.

1. What is the default retention period for an SQS message?
    - Answer: The default retention period for messages in an SQS queue is 4 days. It can be adjusted to anywhere between 1 minute and 14 days.

1. What is the maximum retention period for SQS messages?
    - Answer: The maximum retention period is 14 days.

1. What is the visibility timeout in SQS?
    - Answer: The visibility timeout is the time period during which a message is invisible to other consumers after a consumer retrieves it. If the consumer doesn’t process and delete the message within this period, it becomes visible again.

1. How does dead-letter queue (DLQ) work in SQS?
    - Answer: Dead-letter queues are used to store messages that couldn't be processed successfully after a set number of retries. Messages are sent to the DLQ after exceeding the maximum receive count.

1. What is message deduplication in FIFO queues?
    - Answer: Message deduplication ensures that no duplicate messages are sent to a FIFO queue. SQS uses a Message Deduplication ID (or content-based deduplication) to identify and remove duplicates.

1. What are SQS message attributes?
    - Answer: Message attributes are key-value pairs that provide additional structured metadata about the message, such as timestamps, tags, or user-defined data. These attributes don't affect the message body.

1. What is long polling in SQS, and why is it useful?
    - Answer: Long polling reduces the number of empty responses by allowing the ReceiveMessage action to wait until a message is available or the long-polling timeout expires. It saves costs by reducing API requests when no messages are available.

1. How does short polling differ from long polling in SQS?
    - Answer: Short polling returns immediately, even if no messages are available in the queue, leading to potentially more API calls. Long polling waits up to the specified duration for messages, reducing unnecessary responses and cost.

1. What is a delay queue in SQS?
    - Answer: A delay queue postpones the delivery of messages for a specified period. When a message is sent to a delay queue, it won’t be visible to consumers until the delay period elapses.

1. What is the maximum message delay in SQS delay queues?
    - Answer: The maximum message delay for an SQS delay queue is 15 minutes (900 seconds).

1. What is the maximum number of messages that can be received at once in an SQS queue?
    - Answer: You can retrieve a maximum of 10 messages per request using the ReceiveMessage API.

1. How does message sequencing work in FIFO queues?
    - Answer: FIFO queues use Message Group IDs to ensure that messages with the same ID are processed in the exact order they were sent. Messages in different groups can be processed in parallel.

1. What are the throughput limits for SQS Standard and FIFO queues?
    - Answer: Standard queues offer unlimited throughput. FIFO queues support up to 300 transactions per second (TPS) by default (send, receive, delete) but can be increased to 3,000 TPS with batching.

1. How can you increase throughput in FIFO queues?
    - Answer: You can increase throughput by using Message Group IDs to process multiple message groups in parallel. Also, using batching increases throughput by reducing the number of API requests.

1. How does SQS handle data encryption?
    - Answer: SQS supports encryption of data at rest using AWS Key Management Service (KMS). You can specify an AWS KMS key to encrypt your messages when they're stored.

1. How do you ensure that SQS messages are encrypted in transit?
    - Answer: Messages in transit are automatically encrypted using Transport Layer Security (TLS) when they are sent between the consumer, producer, and SQS service.

1. How would you handle message duplication in a data processing workflow?
    - Answer: In a Standard Queue, idempotency in the consuming system should be used to handle duplicate messages. In a FIFO Queue, message deduplication eliminates duplicates based on the Message Deduplication ID.

1. How would you implement error handling for SQS messages in a data pipeline?
    - Answer: Use a Dead-Letter Queue (DLQ) to capture messages that can't be processed after multiple attempts. You can analyze these messages later to identify and fix the errors.

1. How would you configure batch processing in SQS to improve performance?
    - Answer: You can enable `ReceiveMessageBatch` and `SendMessageBatch` APIs to send and receive up to 10 messages in a single request. This reduces the number of API calls and increases throughput.

1. How does SQS ensure high availability in a data engineering workflow?
    - Answer: SQS automatically replicates messages across multiple Availability Zones within an AWS region to provide high durability and availability.

1. How do you ensure message processing order in a data pipeline?
    - Answer: Use FIFO Queues to ensure strict message ordering. FIFO queues ensure that messages are processed in the exact order they are sent.

1. How does SQS handle scaling?
    - Answer: SQS automatically scales based on the volume of messages. Standard queues support nearly unlimited throughput, while FIFO queues can handle up to 3,000 messages per second with batching.

1. How would you optimize the throughput of an SQS queue in a high-traffic data pipeline?
    - Answer: Use batching to send and receive multiple messages at once, configure long polling to reduce unnecessary requests, and enable Message Group IDs in FIFO queues for parallel processing.

1. What is the best way to handle large payloads in SQS?
    - Answer: For messages larger than 256 KB, use the SQS Extended Client Library, which stores the message payloads in Amazon S3 and references them in SQS.

1. How can you reduce latency in SQS message processing?
    - Answer: To reduce latency, ensure that your consumers are located in the same AWS region as your SQS queue, enable long polling, and use FIFO Queues if message order is important.

1. How does SQS handle backpressure or message buildup?
    - Answer: When messages pile up due to slow consumers, SQS provides features like visibility timeout adjustments and dead-letter queues to ensure that the system doesn’t lose messages while handling backpressure.

1. How do you ensure fault tolerance in an SQS-based system?
    - Answer: SQS automatically replicates messages across multiple Availability Zones, ensuring durability. You can use dead-letter queues (DLQ) to handle failed message processing.

## Scenario-Based Questions
1. You used SQS to trigger your pipeline. Why didn't you use 'FIFO' queues for everything? Isn't ordering always better?
    - The Answer: We chose Standard Queues because of Throughput and Cost.
    - Throughput: Standard queues support nearly unlimited transactions per second (TPS). FIFO queues are limited (default 300 TPS, or 3,000 with batching).
    - Use Case: For our data ingestion (e.g., uploading 10,000 logs/sec), exact ordering didn't matter as much as speed. **We handle ordering via timestamps in the data itself.**
    - Cost: FIFO queues are slightly more expensive.

1. What is 'Visibility Timeout', and why is it the most critical configuration in SQS?
    - The Answer: Visibility Timeout is the mechanism that prevents Double Processing.
    - How it works: When a consumer (Lambda/EC2) picks up a message, SQS doesn't delete it immediately. It 'hides' it for a set time (e.g., 30 seconds).
    - The Scenario: If my processing takes 5 seconds, I delete the message successfully.
    - The Failure: If my processing crashes or takes 40 seconds, the Visibility Timeout expires. The message 're-appears' in the queue, and another consumer picks it up.
    - Impact: If this timeout is too short, we get duplicates. If it's too long, retries are delayed.

1. Your SQS bill is high because you are making too many empty API calls. How do you fix this?
    - The Answer: We need to enable Long Polling.
    - Short Polling (Default): The consumer asks 'Any data?' SQS checks a subset of servers and returns immediately, often empty. We pay for every call.
    - Long Polling: We set WaitTimeSeconds to 20 seconds. The consumer asks 'Any data?'. SQS waits up to 20 seconds until a message arrives before returning.
    - Benefit: Drastically reduces the number of API calls (and cost) while keeping the system responsive.

1. We need to send the same data to the 'Data Lake Team' AND the 'Real-Time Dashboard Team'. How do we do this with SQS?
    - The Answer: SQS is 1-to-1 (Point-to-Point). For this, we use the Fan-Out Pattern using SNS + SQS.
    - Architecture:
        1. The Producer publishes the message to an SNS Topic.
        1. We subscribe two queues to that Topic: Queue_DataLake and Queue_Dashboard.
        1. SNS pushes a copy of the message to both queues automatically.
    - Benefit: This fully decouples the teams. If the Data Lake consumer crashes, the Dashboard queue fills up independently without affecting the other flow.

1. What is a Dead Letter Queue (DLQ) and why is it dangerous NOT to have one?
    - The Answer: A DLQ is a 'Graveyard' for bad messages (Poison Pills).
    - The Scenario: A message arrives with malformed JSON. The consumer tries to parse it, crashes, and the message returns to the queue (due to Visibility Timeout).
    - The Loop: The consumer picks it up again, crashes again. This happens infinitely (Infinite Loop), blocking valid messages and burning compute costs.
    - The Fix: We configure a Re-drive Policy (e.g., maxReceiveCount = 5). After failing 5 times, SQS moves the message to the DLQ so the main queue can continue processing. We then inspect the DLQ manually to fix the bug.

1. You are using Lambda to process SQS messages in batches of 10. If record #5 fails, what happens to the other 9?
The Answer: Historically, the entire batch would fail and be retried, causing duplicate processing for the 9 good records.
The Fix: We use Report Batch Item Failures.
How it works: When the Lambda fails, it catches the error and returns a specific response: `{'batchItemFailures': [{'itemIdentifier': 'id_of_record_5'}]}`.
Result: SQS deletes the 9 successful messages and only makes record #5 visible again for retry.

1. We have a FIFO queue for order processing. It is limited to 300 TPS, but we need 3,000 TPS. We cannot switch to Standard queues because ordering is required. What do we do?
    - The Answer: We can use High Throughput FIFO mode and utilize Message Group IDs.
    - The Concept: In FIFO, ordering is strictly guaranteed within a Message Group.
    - Strategy: We don't use a single global ID. We use CustomerID as the MessageGroupId.
    - Result:
        - Orders for Customer A are strictly ordered.
        - Orders for Customer B are strictly ordered.
        - But Customer A and Customer B are processed in Parallel.
    - Impact: This allows SQS to scale horizontally (partitioning by Group ID) while maintaining the necessary business ordering.

1. How do you auto-scale your consumer EC2 instances based on SQS load? Using CPU utilization isn't working.
    - The Answer: CPU is a lagging indicator. We must scale based on Queue Depth (Metric: `ApproximateNumberOfMessagesVisible`).
    - The Math: We calculate the 'Backlog Per Instance'.
    - Formula: `AcceptableLatency / AverageProcessingTime = Messages per Instance`.
    - The Setup: We create a CloudWatch Alarm. If `MessagesVisible / NumberOfInstances > Target`, we trigger the Auto Scaling Group to add more servers.mThis is 'Predictive Scaling' based on work pending, not work being done.

1. Explain the security implications of Cross-Account SQS access. How did you handle encryption?
The Answer: For cross-account access (e.g., Team A sends data to Team B's queue):
SQS Access Policy: The queue policy must explicitly allow the IAM Role ARN of the other account (Principal: AWS: 12345...).
Encryption (KMS): This is the blocker. If SSE-KMS is enabled, the queue policy isn't enough. We must also modify the KMS Key Policy to allow the external account to use `kms:GenerateDataKey` and `kms:Decryp`t. Without this, the external producer gets Access Denied even with valid queue permissions.

1. You wrote a script to push JSON logs to SQS. It worked for a week. Today, it failed with BatchRequestTooLong or MessageTooLong. You checked the log size, it was 300KB. Why did it fail?
The Answer: SQS has a strict limit of 256KB per message payload.
The Fix (Data Engineering Pattern): Use the Claim Check Pattern (or SQS Extended Client Library).
Upload the 300KB JSON to S3.
Send a small SQS message containing only the Pointer (Bucket Name + Key).
The consumer reads the SQS message, gets the pointer, and downloads the full payload from S3.

1. Your consumer application crashed on Friday night. You fixed it on Tuesday morning. You expected to process the backlog, but the queue is empty. Where did the data go? The default retention is 4 days.
    - The Answer: You likely hit the Retention Period Limit.
    - The Logic: SQS Default Retention is indeed 4 days.
    - The Trap: However, if the retention was configured to something lower (e.g., 1 day) by a Terraform script to save money during dev, the production messages expired and were deleted by AWS automatically.
    - The Fix: Always set Production Retention to the maximum (14 days) to survive long weekends or extended outages.

1. Team A (Producer) sends messages to Team B (Consumer) using a shared SQS queue. You enabled SSE-KMS encryption on the queue to meet compliance. Team A can still write messages. But Team B's Lambda now fails with `KMS.AccessDeniedException` when trying to read. Team B has `sqs:ReceiveMessage` permission.
    - The Answer: The Consumer (Team B) is missing Decrypt permissions.
    - The Mechanism: When SQS stores the message, it encrypts it. When a consumer tries to 'Receive', SQS must decrypt it first.
    - The Fix: You must update the KMS Key Policy (not just IAM) to allow Team B's IAM Role to perform `kms:Decrypt`. Access to the queue is not enough; they need access to the Key.

1. You are using a FIFO Queue because strict ordering is required. You have 1,000 different MessageGroupIds (customers). Suddenly, processing stops for Customer A. You check the logs: The consumer crashed on one specific message from Customer A. Why are new messages for Customer A not being processed?
    - The Answer: This is the FIFO Head-of-Line Blocking feature.
    - The Logic: In FIFO, if a consumer fails to process Message 1 (it doesn't delete it), SQS cannot give you Message 2, because that would break the order.
    - The Result: SQS blocks the entire MessageGroupId until Message 1 is either processed successfully or moved to a Dead Letter Queue (DLQ).
    - The Fix: Ensure you have a DLQ configured with a maxReceiveCount. Once the bad message moves to the DLQ, the 'block' is removed, and the rest of Customer A's messages flow again.

1. You rely on SQS FIFO for Deduplication. You send a message with `MessageDeduplicationId = '123'`. 10 minutes later, the producer retries and sends the same message with `MessageDeduplicationId = '123'`. SQS accepts it, and your consumer processes it twice. Why didn't SQS block the duplicate?
    - The Answer: The Deduplication Interval is only 5 minutes.
    - The Limit: SQS FIFO only remembers a DeduplicationId for 5 minutes.
    - The Scenario: If the retry happens at minute 6, SQS treats it as a brand new message.
    - The Fix: **Your consumer must still be idempotent** (check Database for ID=123 exists) because **SQS cannot guarantee deduplication over long time windows**.

1. Your Lambda reads 10 messages from SQS. It processes them successfully. It calls `sqs.delete_message_batch` to clear them. However, the API call fails with `BatchEntryIdsNotDistinct`. What does this mean?
    - The Answer: You tried to delete the same message twice in the same batch.
    - The Cause: If your queue contains duplicate messages (Standard Queue) or your logic added the same ID to the delete list twice, the API rejects the entire batch request.
    - The Fix: In your code, run a `.distinct()` or `set()` operation on the list of Receipt Handles before sending them to the Delete API.

## Error-Based Questions
1. Your Lambda function triggered by SQS is idempotent (safe to run twice). However, you notice that for complex tasks, the same message is being delivered to the Lambda twice, exactly 30 seconds apart. The Lambda logs show the first execution succeeded. Why did SQS send it again?
    - The Answer: The Visibility Timeout is shorter than the Processing Time.
    - The Error: The queue's default Visibility Timeout is 30 seconds. If your Lambda takes 35 seconds to process, SQS assumes the Lambda crashed at the 30-second mark.
    - The Mechanism: SQS makes the message 'Visible' again to other consumers.
    - The Race: The first Lambda finishes at 35s and deletes the message, but by then, a second Lambda might have already picked up the 're-visible' message.
    - The Fix: Increase the Visibility Timeout on the SQS queue to be 6x the Lambda timeout (or at least higher than the max processing time).

1. You tried to send a 300KB JSON payload to SQS. The application crashed with `BatchRequestTooLong` or `MessageTooLong`. You cannot split the JSON. How do you fix this?
    - The Answer: SQS has a hard limit of 256KB per message.
    - The Fix: Use the S3 Claim Check Pattern (often handled by the 'SQS Extended Client Library').
        1. Upload the 300KB payload to S3.
        1. Send a small SQS message containing only the S3 Key/Pointer.
        1. The consumer reads the message, sees the pointer, and downloads the full payload from S3.

1. Your SQS queue is mostly empty (1 message per hour). However, your bill shows millions of API requests (ReceiveMessage). Why is an empty queue costing money?
    - The Answer: You are using Short Polling (Default).
    - The Cause: If your consumer asks 'Any messages?' and the queue is empty, SQS returns 'No' immediately. Your consumer (loop) asks again instantly. This creates a tight loop of millions of empty requests.
    - The Fix: Enable Long Polling by setting WaitTimeSeconds = 20. Now, if the queue is empty, SQS waits up to 20 seconds on the server side before returning 'Empty'. This reduces API calls by a factor of ~1000x.

1. Your consumer reads 10 messages in a batch. It processes them successfully. It calls `delete_message_batch` with the list of 10 receipts. The API fails with `BatchEntryIdsNotDistinct`. Why? You definitely sent 10 IDs.
    - The Answer: You tried to delete the same message ID twice in the same batch request.
    - The Scenario: Typically happens in Standard Queues (which have 'At-Least-Once' delivery). You might receive the same message twice in the same batch (rare but possible), or your code logic added the same ID to the delete list multiple times.
    - The Fix: Always run a deduplication step (e.g., set(ids)) on the list of Receipt Handles before sending them to the `delete_message_batch` API.

1. What is the 'KMS' Cross-Account Lockout?
    - The Scenario:
        1. Account A owns the Queue. Account B wants to write to it.
        1. You added Account B to the SQS Queue Policy.
        1. Account B still gets `Access Denied` when calling `SendMessage`. The Queue is encrypted with SSE-KMS. What is missing?
    - The Answer: The KMS Key Policy.
    - The Trap: Permissions for SQS (`sqs:SendMessage`) are not enough if the queue is encrypted.
    - The Requirement: The producer (Account B) needs permission to Generate Data Keys (`kms:GenerateDataKey`) to encrypt the payload before sending it.
    - The Fix: Update the KMS Key Policy in Account A to trust the IAM Role from Account B.

1. A message causes your consumer application to crash (e.g., a Syntax Error in the JSON).
    - Scenario:
        1. App reads message -> Crashes.
        1. Timeout expires.
        1. App reads message -> Crashes. This has been happening for 3 days. Why didn't the message disappear?
    - The Answer: You missed configuring a Dead Letter Queue (DLQ) and a Re-drive Policy.
    - The Mechanism: Without a DLQ, SQS will retry the message indefinitely (until the 14-day retention limit).
    - The Fix: Configure a Re-drive Policy with `maxReceiveCount = 5`. After the message is read 5 times without being deleted, SQS automatically moves it to the DLQ, breaking the crash loop.

1. You are using a FIFO queue for order processing. You grouped orders by `MessageGroupId = 'AllOrders'` to keep global ordering. One malformed message is failing processing. Now, ALL processing has stopped. No new orders are being processed. Why?
    - The Answer: This is Head-of-Line Blocking in FIFO queues.
    - The Logic: FIFO guarantees order. If Message A fails (and is not deleted), SQS cannot give you Message B, because that would break the order.
    - The Impact: SQS blocks the entire MessageGroupId until Message A is resolved.
    - The Fix:
        - Granular Group IDs: Don't use a single ID like AllOrders. Use CustomerID or RegionID so a failure only blocks that customer, not everyone.
        - DLQ: Ensure a DLQ is configured so the bad message is moved out eventually, unblocking the group.

1. You migrated from Standard to FIFO SQS. Your application pushes 3,000 messages/sec. Suddenly, you are getting `ThrottlingException` (HTTP 429) errors. You didn't change the code.
    - The Answer: FIFO queues have a much lower throughput limit than Standard queues.
    - The Limits:
        - Standard: Nearly unlimited TPS.
        - FIFO: Limited to 300 TPS (send/receive/delete) by default, or 3,000 TPS if using Batching and High Throughput mode.
    - The Fix:
        - Enable High Throughput FIFO in the settings.
        - Batching: Change the producer to use `SendMessageBatch` (sending 10 messages per API call) to stay under the TPS limit.

1. You have 500 EC2 instances trying to pull from SQS. The queue is full, but the instances are processing very slowly. CPU is low. Application logs show ConnectTimeout errors occasionally when talking to SQS.
    - The Answer: You are likely hitting the NAT Gateway Bandwidth or VPC Endpoint limits.
    - The Cause: SQS involves high network traffic (HTTP polling). 500 instances polling constantly creates thousands of connections.
    - The Bottleneck: If all traffic goes through a single NAT Gateway, you might hit port exhaustion or bandwidth caps.
    - The Fix: Use a VPC Interface Endpoint for SQS to keep traffic internal and distributed, avoiding the NAT Gateway bottleneck.

1. You are building a logging pipeline. To make the logs searchable without parsing the body, you decided to add 20 different tags (UserID, SourceIP, Region, Browser, etc.) as Message Attributes. The SendMessage API fails with `InvalidParameterValue`. Why?
    - The Answer: SQS has a strict limit of 10 Message Attributes per message.
    - The Constraint: While the message body can handle 256KB, the metadata (headers) is limited to 10 distinct items.
    - The Fix:
        - Combine Attributes: Pack the metadata into a single JSON string attribute (e.g., AttributeName='Metadata', Value='{User:A, IP:1.1}').
        - Move to Body: If the metadata is essential, move it into the main JSON body payload.

1. During a deployment, you needed to clear the queue. You ran `PurgeQueue`. Immediately after (1 second later), your script started sending new messages. However, some of the new messages were also deleted. Why?
    - The Answer: Queue Purging is not atomic or instantaneous.
    - The Behavior: The `PurgeQueue` operation can take up to 60 seconds to propagate across all SQS storage nodes.
    - The Risk: Any messages sent to the queue while the purge is in progress might be swept up and deleted along with the old messages.
    - The Fix: Always wait at least 60 seconds after issuing a Purge command before allowing producers to write to the queue again.

1. You configured your Main Queue with a Retention Period of 14 Days. You configured your Dead Letter Queue (DLQ) with a Retention Period of 4 Days. A message stuck in the Main Queue for 13 days finally fails processing and moves to the DLQ. The Error: The message disappears from the DLQ almost immediately. Why?
    - The Answer: The Retention Timestamp does not reset when a message moves to the DLQ.
    - The Logic: The 'Age' of a message is calculated from when it was first created in the original queue.
    - The Math: Age = 13 days. DLQ Retention Limit = 4 days.
    - The Result: 13 > 4. SQS sees the message is already 'older' than the allowed retention of the DLQ and deletes it immediately.
    - The Fix: Always set the DLQ Retention Period to be longer than the Main Queue (e.g., Main=4 days, DLQ=14 days) to give you time to debug old failures.

1. A Lambda function receives a batch of 10 messages from SQS. Message #3 causes an error. You catch the exception in your code to prevent the whole batch from failing. 
    - The Error: Since you caught the exception, SQS thinks the batch succeeded. Message #3 is deleted and lost forever. How do you handle this?
    - The Answer: You must return the `batchItemFailures` response.
    - The Mechanism: If you catch the exception, Lambda returns 'Success' (HTTP 200) to SQS. SQS deletes everything.
    - The Fix:
        1. Configure the Lambda Event Source Mapping to enable 'Report Batch Item Failures'.
        1. In your code, catch the error for Message #3, add its messageId to a list, and return a JSON object: `{batchItemFailures: [{itemIdentifier: msg-id-3}]}`.
    - Result: SQS deletes the 9 good messages but keeps Message #3 in the queue to be retried.

1. You implemented a 'Request-Response' pattern.
    - Scenario:
        1. Client sends a request to a Request Queue.
        1. Client creates a Temporary Queue to listen for the answer.
        1. Server processes request and replies to the Temporary Queue. 
        1. The Error: The client crashes. When it restarts, it cannot find the answer. The Temporary Queue is gone. Why?
    - The Answer: Temporary Queues (managed by the AWS SDK) are often tied to the Process Lifecycle.
    - The Architecture: If you used the SQS Temporary Queue Client, it creates a queue that is deleted when the client shuts down or disconnects to save costs.
    - The Failure: If the client crashes, the queue is deleted, and any messages waiting in it (the responses) are lost.
    - The Fix: For critical data, use a static, persistent Response Queue and filter responses using a `CorrelationId` (Message Attribute), rather than creating ephemeral queues for every request.