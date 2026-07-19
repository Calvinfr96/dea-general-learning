# AWS SNS Interview Questions

## Basic Questions
1. What is Amazon SNS?
    - Answer: Amazon Simple Notification Service (SNS) is a fully managed pub/sub messaging service that enables you to send messages from publishers to subscribers, which can be AWS services, email addresses, SMS numbers, or HTTP/HTTPS endpoints.

1. What are the core components of SNS?
    - Answer: The core components of SNS are topics, publishers, and subscribers. Publishers send messages to SNS topics, and subscribers receive those messages.

1. What is an SNS topic?
    - Answer: An SNS topic is a logical access point where publishers send messages, and subscribers subscribe to receive those messages.

1. What are the different types of subscribers in SNS?
    - Answer: Subscribers can be HTTP/HTTPS endpoints, AWS Lambda functions, SQS queues, email, SMS, or application endpoints (like mobile push notifications).

1. How does SNS ensure message delivery?
    - Answer: SNS ensures **at-least-once delivery** of messages to subscribers. For certain protocols (like HTTP/HTTPS), it retries delivery if the initial attempt fails.

1. What is the maximum message size in SNS?
    - Answer: The maximum message size for an SNS message is 256 KB.

1. What is a message filtering policy in SNS?
    - Answer: Message filtering in SNS allows subscribers to receive only the messages they are interested in by defining filter policies based on message attributes.

1. How does Amazon SNS differ from SQS?
    - Answer: SNS follows a publish-subscribe model where a message is broadcast to multiple subscribers, while SQS is a queueing service for point-to-point messaging where consumers pull messages from the queue.

1. Can SNS trigger AWS Lambda functions?
    - Answer: Yes, SNS can trigger AWS Lambda functions by publishing messages to a topic that Lambda is subscribed to. Lambda then processes the message.

1. What are message attributes in SNS?
    - Answer: Message attributes are key-value pairs that provide additional metadata about the message. These attributes can be used for filtering or delivering specific information to subscribers.

1. What is SNS FIFO (First-In-First-Out)?
    - Answer: SNS FIFO ensures that messages are published and delivered in strict order and are processed exactly once. It is useful for use cases that require ordered message processing.

1. How can SNS be used with mobile push notifications?
    - Answer: SNS can send mobile push notifications to devices via platforms like Amazon Device Messaging (ADM), Apple Push Notification Service (APNS), Google Firebase Cloud Messaging (FCM), and Microsoft Push Notification Service (MPNS).

1. How does SNS ensure reliability in message delivery?
    - Answer: SNS automatically replicates messages across multiple Availability Zones (AZs) in an AWS region, ensuring high availability and durability.

1. How can you filter messages sent to subscribers in SNS?
    - Answer: You can use message filtering policies to specify which messages a subscriber receives. Filters are based on message attributes that subscribers can use to only receive relevant messages.

1. What is SNS fan-out?
    - Answer: SNS fan-out is a pattern where a single message is sent to an SNS topic and then distributed to multiple SQS queues or other subscribers. It’s useful for parallel processing in distributed systems.

1. How does SNS handle message retries for HTTP/HTTPS endpoints?
    - Answer: SNS retries message delivery to HTTP/HTTPS endpoints in case of failures. The retry logic uses backoff algorithms to handle intermittent failures and network issues.

1. What is the maximum retention period for SNS messages?
    - Answer: SNS doesn’t store messages after delivery. It pushes messages to subscribers, and retries are made if needed. The message retention period applies only to the subscriber endpoint, such as SQS.

1. What happens if an SNS message cannot be delivered?
    - Answer: If an SNS message cannot be delivered, SNS retries delivery based on the protocol (e.g., HTTP/HTTPS retries with exponential backoff). For SQS, Lambda, and other AWS services, dead-letter queues (DLQs) can capture failed deliveries.

1. How does SNS integrate with AWS CloudWatch?
    - Answer: SNS integrates with CloudWatch to publish metrics like the number of messages published, delivery attempts, successful deliveries, and failed deliveries. You can set alarms based on these metrics.

1. What is the purpose of SNS dead-letter queues (DLQs)?
    - Answer: SNS DLQs capture undeliverable messages from failed HTTP/HTTPS or Lambda subscriptions. They help in debugging issues and ensuring that failed messages aren’t lost.

1. How can SNS be used in a data pipeline?
    - Answer: In a data pipeline, SNS can be used to trigger downstream processing by sending notifications when data processing tasks complete, alerting systems about changes, or triggering Lambda functions to handle events.

1. How can SNS and SQS be integrated in a data engineering workflow?
    - Answer: SNS can be integrated with SQS using a fan-out pattern. Messages published to SNS can be sent to multiple SQS queues, allowing parallel processing of the same message by different services or systems.

1. How would you use SNS to trigger ETL jobs?
    - Answer: SNS can trigger Lambda functions that execute ETL jobs. For example, after a file is uploaded to S3, SNS can notify a Lambda function to start the ETL process.

1. How would you handle high-throughput notifications in a data pipeline using SNS?
    - Answer: You can use SNS FIFO topics to handle high-throughput and ensure ordered message delivery. If ordering is not required, standard SNS topics can handle nearly unlimited throughput with high availability.

1. How does SNS integrate with Amazon S3 for event-driven data pipelines?
    - Answer: SNS can receive notifications from S3 event notifications when objects are created or modified. These SNS notifications can then trigger downstream processes like data ingestion or transformation tasks.

1. How would you use SNS to build a notification system for data pipeline failures?
    - Answer: SNS can be integrated with CloudWatch Alarms or AWS Step Functions to send notifications (via email, SMS, or HTTP) when specific conditions, such as job failures or pipeline errors, are detected.

1. What is the role of SNS in real-time data processing?
    - Answer: SNS enables real-time notifications that can trigger immediate actions in response to data events. It can be used to notify downstream systems or trigger Lambda functions to process real-time data.

1. How would you ensure the order of message delivery in a data pipeline using SNS?
    - Answer: Use SNS FIFO topics to ensure that messages are delivered in the exact order they are published. FIFO topics also ensure exactly-once message processing.

1. How does SNS integrate with AWS Step Functions in data workflows?
    - Answer: SNS can be used to trigger AWS Step Functions to orchestrate complex workflows. For example, SNS can notify Step Functions to begin a new step when an upstream task in the pipeline is complete.

1. How would you decouple microservices in a data pipeline using SNS?
    - Answer: SNS can be used to decouple microservices by enabling communication between them via a publish-subscribe model. When a microservice publishes data, other microservices subscribed to the topic receive notifications and act accordingly.

1. How do you secure an SNS topic?
    - Answer: SNS topics can be secured using IAM policies and topic policies to control who can publish and subscribe to the topic. Encryption using AWS KMS can be applied for data at rest.

1. What is a topic policy in SNS?
    - Answer: A topic policy is a resource-based policy that specifies who can publish messages to the topic and who can subscribe to the topic. These policies are written in JSON format and support fine-grained permissions.

1. How do you control cross-account access to an SNS topic?
    - Answer: To allow cross-account access, you can create an SNS topic policy that grants permissions to another AWS account to publish or subscribe to the topic.

1. What role does AWS KMS play in securing SNS?
    - Answer: AWS KMS provides encryption at rest for SNS messages. You can specify an AWS KMS key to encrypt messages before they are stored, ensuring that only authorized users can decrypt them.

1. How can you implement encryption in transit for SNS messages?
    - Answer: Messages transmitted between SNS and subscribers are encrypted using Transport Layer Security (TLS), ensuring data privacy and security in transit.

1. What is the purpose of SNS VPC endpoints (AWS PrivateLink)?
    - Answer: SNS VPC endpoints allow you to privately connect your VPC to SNS without using the public internet. This enhances security for applications running within a VPC that need to interact with SNS.

1. How do you audit access to SNS topics?
    - Answer: Use AWS CloudTrail to log all API calls to SNS topics, including who accessed the topics, what actions were performed, and when they were accessed. This helps in auditing and tracking unauthorized access.

1. How do you prevent unauthorized message publishing in SNS?
    - Answer: You can prevent unauthorized publishing by using IAM policies and topic policies that restrict who can publish messages to the topic. Additionally, use KMS encryption to secure the messages.

1. How can SNS integrate with AWS Secrets Manager for secure message handling?
    - Answer: SNS can integrate with AWS Secrets Manager by securely retrieving sensitive data such as API keys or credentials used in your Lambda function or endpoint that handles SNS messages.

1. How can you control who subscribes to your SNS topics?
    - Answer: You can control subscriptions using SNS topic policies to specify which AWS accounts, IAM users, or services are allowed to subscribe to the topic.

1. How does SNS handle scalability?
    - Answer: SNS automatically scales to handle virtually unlimited messages per second across different endpoints, ensuring high throughput and availability.

1. How would you optimize SNS for high-throughput applications?
    - Answer: Use SNS FIFO topics for ordered message processing and standard SNS topics for high-throughput, unordered delivery. Also, enable batching and ensure that your subscribers can handle the message rate.

1. How can you optimize SNS for mobile push notifications?
    - Answer: For mobile push notifications, SNS supports delivery batching and message fan-out to ensure efficient and scalable message delivery across multiple devices and platforms.

1. How can SNS be used to fan out messages to multiple systems?
    - Answer: SNS can be used to fan out messages by sending a single message to multiple subscribers like Lambda functions, SQS queues, or HTTP endpoints. This allows parallel processing across multiple systems.

1. What are the throughput limits of SNS FIFO topics?
    - Answer: SNS FIFO topics support up to 300 transactions per second (TPS) per message group by default, and you can increase throughput to 3,000 TPS by enabling message batching.

1. How can SNS and SQS work together to increase reliability in a data pipeline?
    - Answer: SNS can send messages to SQS queues, allowing for durable storage of messages and asynchronous processing. This ensures that messages are not lost if downstream systems are unavailable.
    - As long as the ETL logic is idempotent, sending the same message to multiple queues, instead of a single queue, helps lower the risk of a single queue becoming severely backed up, allowing messages to expire before they're consumed.

1. How do you handle large message payloads in SNS?
    - Answer: If you need to handle large payloads (>256 KB), you can store the payload in Amazon S3 and send the reference or URL to subscribers via SNS.

1. What is the benefit of using message batching with SNS?
    - Answer: Message batching allows you to send multiple messages to SNS subscribers in a single API call, reducing the number of requests, lowering costs, and improving overall throughput.

1. How do you reduce message delivery latency in SNS?
    - Answer: To reduce latency, ensure that your SNS topic and subscribers are in the same AWS region, use SNS FIFO topics if ordering is required, and configure efficient retry strategies for subscribers.

1. How does SNS handle message durability in case of failures?
    - Answer: SNS retries message delivery for HTTP/HTTPS endpoints and Lambda functions in case of failures. For other endpoints like SQS, messages are stored in the queue until successfully processed.

## Scenario-Based Questions
1. You used SNS in your pipeline. Why couldn't you just use SQS directly? What is the architectural difference?
    - The Answer: We needed a Pub/Sub (Publish/Subscribe) model, not a Point-to-Point model.
    - SQS (1-to-1): If I send a message to a Queue, only one consumer (e.g., one server) picks it up. If I want a second team to see that data, I can't do it.
    - SNS (1-to-Many): I publish a message to an SNS Topic once. SNS then 'fans out' copies of that message to all subscribers (SQS Queue A, SQS Queue B, Lambda C) simultaneously.
    - Use Case: It allowed us to decouple the 'Ingestion Team' from the 'Analytics Team'. The Ingestion team publishes to SNS, and we just subscribe our queue to it.

1. What is the 'Fan-out' pattern, and how did you implement it for data durability?
    - The Answer: The Fan-out pattern is where an SNS Topic pushes messages to multiple SQS Queues.
    - The Implementation:
        1. Topic: NewDataArrived_Topic.
        1. Subscribers: We attached two SQS queues to this topic:
            Production_Queue (for the main ETL pipeline).
            Audit_Queue (for storing raw logs in S3 for compliance).
    - The Benefit: If the Production pipeline crashes or gets backed up, the Audit queue is completely unaffected. Both systems receive the exact same data in parallel.

1. Can you trigger an EMR Job directly from SNS?
    - The Answer: Not directly. SNS cannot 'Submit a Step' to EMR natively.
    - The Glue: We used AWS Lambda as the bridge.
    - The Flow:
        - S3 Event -> SNS Topic.
        - SNS triggers a Lambda function.
        - The Lambda function calls the EMR API (`add_job_flow_steps`) to kick off the Spark processing.
    - Why Lambda? SNS is a notification service; it doesn't have compute logic to define how the EMR job should run.

1. We have one SNS Topic for 'All Orders'. The 'fraud-team' only wants to process orders where amount > $10,000. Do we need a separate Topic?
    - The Answer: No, creating separate topics for every variation is an anti-pattern. We should use SNS Message Filtering.
    - How it works:
        - The Publisher sends the message with Message Attributes (metadata): {amount: 12000, currency: USD}.
        - The Fraud Team's SQS Subscription has a Filter Policy: {amount: [{numeric: [>, 10000]}]}.
        - The Result: SNS looks at the attribute. If it matches, it pushes to the queue. If not, it drops it before it hits the queue.
    - Benefit: The Fraud Team's queue only receives relevant data, saving them money on SQS polling and compute.

1. Does SNS guarantee message ordering? If I publish Event A then Event B, will they arrive in that order?
    - The Answer: It depends on the Topic type.
    - Standard Topic: No. Order is not preserved. Event B might arrive before Event A. It is 'Best Effort' ordering.
    - FIFO Topic: Yes, but strictly requires an SQS FIFO Queue as the subscriber.
    - You must use a MessageGroupId (e.g., UserID).
    - SNS ensures that for a specific UserID, Event A is pushed to the FIFO queue before Event B.
    - Trade-off: FIFO topics have lower throughput (300/3,000 TPS) compared to Standard (Unlimited).

1. What happens if the subscriber (e.g., the Lambda endpoint) is down? Does SNS retry?
    - The Answer: Yes, SNS has a Delivery Retry Policy.
    - The Mechanism: If the destination returns an error (e.g., HTTP 500 or Throttling), SNS retries.
    - The Phases: It goes through 4 phases: Immediate retry -> Pre-backoff -> Backoff (Exponential) -> Post-backoff. This can last for hours or days depending on configuration.
    - The Failure: If all retries fail, the message is dropped unless a Dead Letter Queue (DLQ) is configured on the Subscription.

1. You are publishing to SNS from an S3 Bucket in Account A. The SNS Topic is in Account B. Why isn't it working even though the IAM Role has permission?
    - The Answer: Cross-account SNS is controlled by the Topic Policy (Resource Policy), similar to an S3 Bucket Policy.
    - The Trap: Giving the S3 service in Account A permission to `sns:Publish` is necessary but not sufficient.
    - The Fix: You must go to the SNS Topic in Account B and edit its Access Policy to explicitly allow the S3 Bucket ARN (or Account A ID) to perform `sns:Publish`.
    - Security Note: Never use Principal: * in the Topic Policy, otherwise anyone on the internet can spam your topic.

1. You have a massive 'Log Stream' topic receiving 1 million events/sec. You subscribed an HTTP endpoint (a webhook) to it. The webhook crashed. Why?
    - The Answer: You inadvertently created a DDoS Attack on your own webhook.
    - The issue: SNS is highly scalable. It will try to push 1 million requests/second to your HTTP server. Your server likely can't handle that concurrency.
    - The Solution: Never subscribe HTTP endpoints directly to high-volume SNS topics.
    - Buffer with SQS: Subscribe an SQS queue to the SNS topic.
    - Process Async: Let the HTTP server (or a worker) poll the SQS queue at its own pace (e.g., 50 messages/sec). This flattens the traffic spike.

1. Explain the 'Raw Message Delivery' setting. When do you use it?
    - The Answer: By default, SNS wraps the message body in a JSON envelope containing metadata (TopicArn, Timestamp, MessageId).
    - The Problem: If I push this to an SQS queue, my consumer has to parse the JSON to extract the actual message Body.
    - The Fix: Enable Raw Message Delivery.
    - SNS strips away the JSON wrapper and pushes only the raw string/payload to the SQS queue or Lambda.
    - Use Case: This is critical when the consumer expects a specific format (e.g., a legacy system) and will crash if it sees the extra AWS metadata fields.

1. You wrote a Terraform script to create an SNS Topic and subscribe an HTTP endpoint (a webhook) to it. The script runs successfully. However, when you publish messages to the topic, the webhook never receives them. CloudWatch shows DeliveryStatus: Failed. Why?
    - The Answer: The subscription is likely stuck in 'Pending Confirmation' state.
    - The Mechanism: For HTTP/HTTPS/Email endpoints, SNS sends a 'Confirmation Request' message first to verify ownership.
    - The Error: If your webhook code doesn't explicitly handle the `SubscriptionConfirmation` message type and call the SubscribeURL inside it, the subscription never activates.
    - The Fix: Update the webhook code to detect Type: `SubscriptionConfirmation` and make a GET request to the URL provided in the payload to confirm the link.

 

1. You subscribed a Lambda function to an SNS Topic. The Lambda fails with a syntax error when trying to parse event['Records'][0]['Sns']['Message']. The producer is sending valid JSON: {order_id: 123}. Why is the Lambda seeing a string instead of JSON?
    - The Answer: This is the Double Serialization trap.
    - The Behavior: SNS treats the message body as a String, even if you send JSON.
    - The Code Error: `event['Sns']['Message'] returns a String: {\order_id\: 123}`. If you try to access it like a dictionary (msg['order_id']), it fails.
    - The Fix: You must `json.loads()` the message string inside the Lambda code to convert it back into a Python dictionary/JSON object before accessing fields.

1. You have a secure setup: An SNS Topic (Encrypted with KMS) -> Subscribed to an SQS Queue (Encrypted with KMS). You publish a message. The SNS Publish API returns 200 OK. But the message never appears in the SQS queue. There are no errors in the Producer logs. Where did it go?
    - The Answer: This is a Silent Encryption Failure between services.
    - The Cause: The SNS Service Principal (`sns.amazonaws.com`) needs permission to use the KMS Key of the SQS Queue to encrypt the message before pushing it.
    - The Fix: You must add a statement to the SQS Queue's KMS Key Policy:
        ```
        Principal: Service: sns.amazonaws.com
        Action: kms:GenerateDataKey, kms:Decrypt
        Resource: *
        ```
    - Why it's silent: SNS successfully received the message (Publisher got 200 OK), but failed to deliver it to SQS. You would only see this in SNS Delivery Status Logs in CloudWatch.

1. You set up a Filter Policy to only route orders where price > 100. The policy is: `{price: [{numeric: [>, 100]}]}`. The producer publishes `{price: 200}`. The message is Dropped. Why? 200 is clearly greater than 100.
    - The Answer: SNS Filtering is Type Sensitive.
    - The Error: The policy specifies a Numeric comparison.
    - The Payload: The producer sent 200 as a String (quoted), not a Number (200).
    - The Result: SNS sees a type mismatch and evaluates it as 'False'. It drops the message.
    - The Fix:
        - Fix Producer: Send 200 (no quotes) as a number Message Attribute.
        - Or, Fix Policy: Use String matching (though less powerful for ranges).

 

1. You migrated from Standard SNS to FIFO SNS to guarantee ordering. Your application processes 2,000 transactions per second (TPS). Suddenly, the Publisher starts getting Throttling Errors (500s). You check the quota, and it says '3,000 TPS'. Why are you failing at 2,000?
    - The Answer: You are hitting the Distribution/Region Limit or lacking Batching.
    - The Nuance: The 3,000 TPS limit for FIFO is usually valid only if you are using `PublishBatch` API.
    - The Limit: If you are using single `Publish` API calls, the limit for FIFO topics in many regions is actually 300 TPS.
    - The Fix: Refactor the producer to use `publish_batch` (sending 10 messages per API call) to unlock the higher 3,000 TPS throughput.

1. You deleted an SNS Topic named MyTopic. You realized it was a mistake and recreated it with the exact same name MyTopic. However, the SQS queues that were subscribed to the old topic are not receiving messages from the new one. Why?
    - The Answer: Subscriptions are linked to the Topic ARN, not the Name.
    - The Reality: When you deleted the old topic, the subscriptions (links) were deleted.
    - The New Topic: Even though the name is the same, the Unique ID (suffix of the ARN) might be different (or simply the link ID is broken).
    - The Fix: You must manually re-subscribe all endpoints (SQS, Lambda) to the newly created Topic ARN.

## Error-Based Questions
1. You used Terraform to create an SNS topic and subscribe your team's email distribution list (team@company.com) to receive alerts. Terraform said 'Apply Complete'. However, when an alert fired 1 hour later, nobody received the email. You check the console, and the subscription status is `PendingConfirmation`. Why?
    - The Answer: Terraform/API cannot force an email subscription to be active; it requires human intervention.
    - The Mechanism: When you subscribe an email (or HTTP endpoint) to SNS, AWS sends a 'Confirm Subscription' email to that address to prevent spam.
    - The Error: Until someone clicks the 'Confirm subscription' link in that email, the status remains `PendingConfirmation`, and SNS will silently drop all messages sent to it.
    - The Fix: Log into the email inbox, find the AWS email (check Spam folder), and click the link. The status will change to Confirmed.

1. You subscribed a webhook (HTTP endpoint) to an SNS topic. The webhook is on a server that is currently down (returning HTTP 503). You publish a message to the SNS topic. The API call returns 200 OK. Does that mean the webhook received the message?
    - The Answer: No. The 200 OK from the SNS Publish API only means 'SNS accepted the message successfully'. It does not mean 'The subscriber received it'.
    - The Architecture: SNS is asynchronous. It takes the message, returns 200 to you, and then tries to deliver it to the subscribers in the background.
    - The Troubleshooting: If the webhook is down, SNS will retry delivery (according to its retry policy). If it eventually fails, the message is dropped unless a Dead Letter Queue (DLQ) is configured. You must check CloudWatch Delivery Status Logs to see the 503 errors.

1. Account A has an SNS Topic. Account B has an SQS Queue. You want Account A to publish to Account B's queue. You gave Account B's IAM Role permission to `sqs:SendMessage`. But SNS (in Account A) still gets AuthorizationError when trying to push to the queue. Why?
    - The Answer: You missed the SQS Queue Policy (Resource Policy).
    - The Logic: IAM permissions grant the user rights, but SQS Queue Policies control who can write to the queue.
    - The Trap: The SQS queue is in Account B. The writer is the SNS Service Principal from Account A.
    - The Fix: You must edit the SQS Queue Policy in Account B to explicitly allow the SNS Topic ARN from Account A to perform the `sqs:SendMessage` action.

1. You have a working Fan-out pattern: SNS -> SQS. To comply with security, you enabled Server-Side Encryption (SSE) on the SNS Topic using a Custom KMS Key. Suddenly, your S3 Event Notifications (which publish to this topic) stop working. S3 says 'Publish Failed'. Why?
    - The Answer: The S3 Service Principal cannot access your Custom KMS Key.
    - The Cause: When S3 publishes to an encrypted SNS topic, it must decrypt the key to encrypt the payload.
    - The Error: By default, your Custom KMS Key Policy allows your IAM users, but it does not allow AWS Services like S3.
    - The Fix: You must update the KMS Key Policy to allow `s3.amazonaws.com` (restricted by SourceArn condition) to use `kms:GenerateDataKey` and `kms:Decrypt`.

1. You set up a Subscription Filter Policy to route messages. Policy: {store: [tokyo]}. The Publisher sends a message with the body: {store: tokyo, item: camera}. The filter drops the message. Why? The store is clearly tokyo.
    - The Answer: SNS Filter Policies apply to Message Attributes, NOT the Message Body.
    - The Nuance: SNS cannot inspect the JSON payload (Body) of your message (unless you enable the new Payload-Based Filtering feature and configure it explicitly).
    - The Standard Behavior: It only looks at the metadata headers (MessageAttributes) you attach to the API call.
    - The Fix: The publisher must change their code to send store as a MessageAttribute, not just as part of the JSON body string.

1. You subscribed an SQS queue to an SNS topic. Your application expects the message to be just the JSON: `{orderId: 123}`. However, when you read from the queue, the message is a huge JSON object containing Type, TopicArn, Message, Timestamp, Signature, etc. Your parser crashes. How do you fix this at the infrastructure level?
    - The Answer: You need to enable 'Raw Message Delivery' on the Subscription.
    - The Default: SNS wraps everything in a standard JSON envelope to provide metadata about the event.
    - The Fix: Edit the Subscription settings and check 'Enable raw message delivery'.
    - The Result: SNS strips away the metadata envelope and pushes only the string payload (`{orderId: 123}`) to the SQS queue, exactly as your app expects.

1. You migrated from Standard SNS to FIFO SNS to ensure strict ordering. Your application pushes 1,000 messages/sec. Suddenly, the publisher starts failing with `ThrottlingException`. You verify that Standard SNS handled this easily. Why is FIFO failing?
    - The Answer: FIFO SNS topics have lower throughput limits than Standard topics.
    - The Limit: By default, FIFO SNS is limited to 300 transactions per second (TPS) per topic (or 3,000 with batching). Standard is nearly unlimited.
    - The Cause: You exceeded the 300 TPS limit.
    - The Fix:
        - Batching: Update the publisher to use PublishBatch API (up to 10 messages per call).
        - Architecture: If strict global ordering isn't required, consider sharding across multiple FIFO topics.

1. You used SNS to send critical alerts via SMS to the on-call team. You wake up to a $2,000 bill for 'SNS Worldwide SMS'. It turns out a developer wrote a loop that accidentally triggered an alert every second for 24 hours. How could you have prevented the cost (not the bug)?
    - The Answer: You should have set a Monthly Spend Limit for SMS.
    - The Feature: In the SNS Console -> Text messaging (SMS) preferences, you can set a 'Account spend limit' (e.g., $50).
    - The Mechanism: Once the cost hits $50, SNS stops sending SMS messages.
    - Impact: You would miss alerts after the limit is hit, but you wouldn't be bankrupt.
    - Better Fix: Use CloudWatch Alarms on the metric `SMSMonthToDateSpentUSD` to alert you before it hits a high number.

1. SNS triggers a Lambda function. The Lambda function takes 5 minutes to process a heavy task. You notice the Lambda is running 3 times for every single message, even though the first one eventually succeeds. This is causing data duplication in your database.
    - The Answer: This is a timeout mismatch between SNS and Lambda.
    - The Default: SNS waits for the Lambda to respond. If Lambda takes too long, SNS assumes it failed and retries.
    - The Configuration: SNS has a default timeout for Lambda delivery (often shorter than the Lambda max of 15 mins).
    - The Fix:
        1. Async: Ensure the invocation is truly asynchronous and your Lambda handles idempotency.
        1. SQS Buffer: The best practice for heavy tasks is SNS -> SQS -> Lambda.
        SQS allows you to configure visibility timeouts properly to handle long-running jobs (up to 12 hours) without phantom retries.

1. You are sending millions of notifications to an HTTP endpoint. Some messages are arriving, but others are missing. The Publish API returns Success for every single call. How do you find out which messages failed and why?
    - The Answer: You must enable SNS Delivery Status Logging.
    - The Problem: The Publish API only confirms that SNS accepted the message, not that it delivered it.
    - The Fix:
        1. Go to the Topic settings and configure an IAM Role that gives SNS permission to write to CloudWatch Logs.
        1. Enable logging for the specific protocol (HTTP/S).
        1. Check the CloudWatch Log Group (e.g., sns/us-east-1/12345/app/HTTP). It will show the exact HTTP status code (e.g., 400 Bad Request, 500 Internal Server Error, or Connection Timeout) returned by the endpoint for the failed messages.

1. You subscribed a secure endpoint https://my-startup.com/webhook to SNS. It fails to confirm the subscription. CloudWatch Logs show: `PEER_COULD_NOT_BE_AUTHENTICATED`. You can open that URL in Chrome just fine. What is wrong?
    - The Answer: The endpoint is likely using a Self-Signed Certificate or an unrecognized Certificate Authority (CA).
    - The Rule: SNS is strict. It requires the HTTPS endpoint to present a certificate signed by a trusted public CA (like DigiCert, Let's Encrypt, etc.).
    - The Trap: Chrome browsers often have extra root certificates installed that AWS servers do not have, or the server is sending an incomplete certificate chain (missing intermediate certs).
    - The Fix: Install a valid certificate chain on the server from a standard public CA.

1. SNS triggers a Lambda function that inserts data into a database. The database goes down for 5 minutes. Even after the DB comes back up, the Lambda continues to crash for hours, and the DB is hammered with traffic. What is happening?
    - The Answer: You are experiencing the SNS Retry Policy side effect.
    - The Behavior: When a Lambda function fails (returns an error), SNS retries. The default retry policy can extend for hours (Immediate -> Linear -> Exponential Backoff).
    - The Storm: During the 5-minute outage, thousands of messages piled up in the retry queue. Once the DB is up, SNS releases this backlog concurrently with new incoming traffic.
    - The Fix:
        1. Reduce Retries: Configure a custom Delivery Policy on the Subscription to limit retries to 3 attempts.
        1. Concurrency Limit: Set `ReservedConcurrency` on the Lambda to protect the database.
        1. DLQ: Move failed messages to a DLQ after 3 attempts.

1. You are using an SNS FIFO Topic -> SQS FIFO Queue. You publish Message A with `DeduplicationId=order-123`. 5 minutes later, you republish Message A with the same ID. The SQS queue receives it. 10 minutes later, you republish it again. The SQS queue does NOT receive it. This seems inconsistent. Why?
    - The Answer: This is a misunderstanding of the 5-minute Deduplication Window.
    - The Logic: SNS remembers the DeduplicationId for exactly 5 minutes.
        - Minute 0: Message sent. Accepted.
        - Minute 5: Retry sent. SNS sees the ID in cache. Drops it (Deduplicates).
        - Minute 10: Retry sent. The ID has expired from the cache. SNS accepts it as a new message.
    - The Fix: If you need deduplication over a longer window (e.g., 24 hours), you cannot rely on SNS/SQS native deduplication. You must implement a check (e.g., DynamoDB lookup) in your consumer application.

1. You use SNS for Mobile Push Notifications (FCM/APNs). It works fine for weeks. Suddenly, 10% of your users stop receiving notifications. CloudWatch shows EndpointDisabled errors. You re-enable them via API, but they fail again immediately. Why?
    - The Answer: The Device Token is invalid or expired.
    - The Lifecycle: When a user uninstalls/reinstalls the app or updates the OS, the push provider (Apple/Google) generates a new token for that device.
    - The Error: If you try to send to the old token, Apple/Google tells SNS This token is dead. SNS then marks the endpoint as Disabled.
    - The Fix: Your mobile app code must detect token refreshes on startup and send the new token to your backend, which calls `SetEndpointAttributes` to update the SNS Endpoint with the new token.