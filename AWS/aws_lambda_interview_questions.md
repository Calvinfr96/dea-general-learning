# AWS Lambda Interview Questions

## Basic Questions
1. What is AWS Lambda?
    - Answer: AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers. It automatically scales and executes code in response to events such as changes in data or requests from an API.

1. What languages are supported by AWS Lambda?
    - Answer: AWS Lambda supports Node.js, Python, Ruby, Java, Go, .NET (C#), and custom runtime environments.

1. What is the maximum execution time for a Lambda function?
    - Answer: The maximum execution timeout for a Lambda function is 15 minutes.

1. What is the memory range you can allocate for a Lambda function?
    - Answer: AWS Lambda allows memory allocation from 128 MB to 10,240 MB (10 GB).

1. How does Lambda handle scaling?
    - Answer: AWS Lambda automatically scales by running more concurrent instances of your function to handle the incoming load.

1. What is the maximum size of a deployment package in AWS Lambda?
    - Answer: The maximum size for a deployment package (compressed) is 50 MB, and the unzipped function code size can be up to 250 MB when uploaded from the console.

1. What are Lambda execution roles, and why are they needed?
    - Answer: Execution roles are IAM roles that AWS Lambda assumes to execute a function. They define the permissions Lambda has to access other AWS services.

1. What is the difference between synchronous and asynchronous invocation in AWS Lambda?
    - Answer: In synchronous invocation, the caller waits for the function to process and return a response. In asynchronous invocation, the caller doesn’t wait for the response, and AWS Lambda handles retries in case of failure.

1. What are Lambda Layers?
    - Answer: Lambda Layers allow you to manage and share common code or libraries across multiple Lambda functions. It helps in managing dependencies separately from your function code.

1. How does AWS Lambda handle concurrency?
    - Answer: Lambda automatically scales with incoming requests, and each request is processed by a new instance of the function. The default limit for concurrent executions is 1,000 per region (soft limit).

1. What is the cold start problem in AWS Lambda?
    - Answer: A cold start happens when AWS Lambda has to initialize a new execution environment for a function, leading to slightly higher latency during the first request.

1. How can you reduce cold starts in AWS Lambda?
    - Answer: Cold starts can be minimized by allocating more memory (which includes CPU power), using Provisioned Concurrency, reducing the size of deployment packages, and optimizing initialization code.

1. What is Provisioned Concurrency in AWS Lambda?
    - Answer: Provisioned Concurrency keeps functions initialized and ready to respond instantly to requests, reducing the latency caused by cold starts.

1. What are the limits of Provisioned Concurrency?
    - Answer: Provisioned Concurrency has a soft limit of 3,000 concurrent executions per region. You can request an increase if necessary.

1. What are Lambda execution contexts?
    - Answer: The execution context is a temporary runtime environment that AWS Lambda uses to run your function. It includes resources like memory, temporary storage, and environment variables that are reused across multiple invocations to optimize performance.

1. What are AWS Lambda environment variables?
    - Answer: Environment variables are key-value pairs that can store configuration values, like database connection strings or sensitive information like API keys, and they can be encrypted using AWS KMS.

1. What is the AWS Lambda function handler?
    - Answer: The function handler is the method in your code that AWS Lambda calls to execute your function. It is the entry point of your function.

1. How does Lambda manage temporary storage?
    - Answer: AWS Lambda provides 512 MB of temporary storage (/tmp directory) per instance for file operations. This storage is not persistent between invocations.

1. How would you implement retries in AWS Lambda?
    - Answer: Lambda automatically retries asynchronous invocations if they fail, with an exponential backoff strategy. For synchronous invocations, retries can be handled by the calling service or custom retry logic.

1. What services can trigger AWS Lambda functions?
    - Answer: AWS Lambda can be triggered by services such as Amazon S3, DynamoDB Streams, Kinesis Data Streams, SNS, SQS, API Gateway, CloudWatch Events, EventBridge, Cognito, and more.

1. What are Lambda triggers, and how do they work?
    - Answer: Lambda triggers are events that invoke a Lambda function. These triggers can come from various AWS services, such as S3, DynamoDB, Kinesis, SNS, and others, based on configured events.

## Scenario-Based Questions
1. You used Lambda for file processing. Why didn't you just use EC2 or Glue for that?
    - The Answer: It was about Event-Driven capability and Cost.
    - Simple Explanation: EC2 is like leaving a car engine running 24/7 just in case you need to drive. Lambda is like starting the car only when you need to go.
    - Technical Detail: Our workload was 'spiky'. We receive files randomly throughout the day. Using EC2 means paying for idle time. AWS Glue has a startup time of minutes. Lambda starts in milliseconds and we pay only for the seconds the code runs. For lightweight transformations (under 15 mins), Lambda is the most efficient choice.

1. What are the hard limits of AWS Lambda that you had to consider?
    - The Answer: The two most critical limits for a Data Engineer are Time and Memory.
    - Timeout: Lambda has a hard stop at 15 minutes. If my data processing takes 16 minutes, Lambda is the wrong tool (I’d use Glue or Fargate).
    - Memory/CPU: The max memory is 10GB. Since CPU power is proportional to memory, if I need high compute, I have to increase memory, which increases cost.
    - Payload: The request body (event) is limited to 6MB. We can't pass a 1GB file into Lambda; we pass the S3 path (a pointer) to the file instead.

1. How does your Lambda function get access to the data in S3? Does it happen by magic?
    - The Answer: No, it requires IAM Roles.
    - Simple Explanation: Just because Lambda and S3 are both in my AWS account doesn't mean they trust each other. I have to give Lambda an ID badge (Role).
    - Technical Detail: I created an IAM Execution Role with a policy allowing `s3:GetObject` on the source bucket and `s3:PutObject` on the target bucket. I attached this role to the function. Without this, the code would crash with `AccessDenied`.

1. We need Lambda to query our private RDS (Postgres) database. When we connected it to the VPC, the internet access stopped working. Why?
    - The Answer: This is a classic VPC networking behavior.
    - The Cause: When you attach Lambda to a VPC to see a private DB, it loses its default public internet access. It is now 'stuck' inside the private network.
    - The Fix: We must route the traffic through an NAT Gateway in a public subnet.
    - The Flow: Lambda (Private Subnet) -> Route Table -> NAT Gateway (Public Subnet) -> Internet Gateway -> External API/Internet.
    - Note: **NAT Gateways cost money, so we only do this if absolutely necessary**.

1. How do you handle failures? If Lambda crashes while processing a file, is the data lost?
    - The Answer: It depends on the Invocation Type (Sync vs. Async).
    - S3 Triggers (Async): AWS automatically retries the function twice if it fails.
    - The Safety Net (DLQ): After the retries fail, we configured a Dead Letter Queue (DLQ) using SQS.
    - Simple Explanation: The DLQ is a 'graveyard' for failed events. If a file fails to process 3 times (maybe the data is corrupt), Lambda sends the event details to the SQS queue. I have a separate alarm on that queue so I can investigate the bad file later without losing the data.

1. You are processing data from an SQS queue. What is 'Batch Size' and why is it important?
    - The Answer: Batch Size determines how many messages Lambda picks up in one go.
    - Optimization: Instead of running the Lambda function 100 times for 100 messages (high cost, many cold starts), we set the batch size to 10 or 50. Lambda reads 50 messages, spins up one instance, loops through them, and finishes.
    - The Risk: If the 50th message fails, the default behavior causes the entire batch to return to the queue, and we might re-process the successful 49 again (duplicates).
    - The Fix: We implement `ReportBatchItemFailures`. We return the specific ID of the failed message so SQS deletes the 49 successful ones and only retries the 1 failed one.

1. We have a massive spike of traffic (10,000 files drop at once). How do we prevent Lambda from scaling infinitely and draining our database connection pool?
    - The Answer: We use Reserved Concurrency.
    - The Problem: By default, Lambda will try to scale to 1,000 concurrent executions. If each execution opens a connection to a small RDS database, the DB will crash (TooManyConnections error).
    - The Solution: I set a 'Reserved Concurrency' limit of 50 on the Lambda function.
    - The Result: Lambda will never spin up more than 50 instances at once. The remaining 9,950 events will queue up and wait their turn. It acts as a throttle to protect downstream systems.

1. Explain the 'Cold Start' problem. How did you mitigate it for your latency-sensitive data pipeline?
    - The Answer: A Cold Start is the time AWS takes to provision a container and download your code before it starts running (typically 100ms - 2 seconds).
    - Mitigation Strategies:
        - Reduce Package Size: We stripped out heavy libraries (like Pandas) if they weren't strictly needed, or used Lambda Layers to keep the core function light.
        - Move Initialization Code: I initialized expensive variables (like DB connections or S3 clients) outside the handler function. This way, warm containers reuse the connection.
        - Provisioned Concurrency: For critical paths, we paid extra for 'Provisioned Concurrency', which keeps X number of instances initialized and ready to respond in double-digit milliseconds.

1. Can you use Lambda for Stream Processing (Kinesis)? How does scaling work there?
    - The Answer: Yes, but the scaling model is different. It is Shard-Based.
    - The Rule: You can have at most one Lambda invocation per Kinesis Shard at any given second.
    - Scaling: If I have 10 Shards in Kinesis, I can have a maximum of 10 concurrent Lambdas processing that stream.
    - The Bottleneck: If data volume increases, adding more Lambdas doesn't help. The number of Kinesis Shards must be increased  (Re-sharding).
    - Parallelization Factor: A newer feature allows us to set a `ParallelizationFactor` to process multiple batches from the same shard in parallel, **but order is no longer strictly guaranteed**.

1. How do you debug your Lambda functions in production? Do you just scroll through thousands of log lines?
    - The Answer: No, scrolling is inefficient. We use CloudWatch Logs Insights.
    - The Tool: It allows us to write SQL-like queries against our logs.
    - Example: If I need to find which specific files failed, I can run a query like: `fields @timestamp, @message | filter @message like /ERROR/`.
    - Advanced: We also use Structured Logging (logging as JSON objects instead of plain text). This lets us query specific fields like filter file_size > 100MB directly in CloudWatch without regex.

1. What are Environment Variables, and how do you secure them?
    - The Answer: Environment Variables let us change configuration without changing code (e.g., DB_HOST, S3_BUCKET_NAME).
    - Security Risk: By default, these are visible in the AWS Console to anyone with read access.
    - The Fix: For sensitive data (like DB passwords), we use AWS KMS (Key Management Service) to encrypt the variable.
    - Better Practice: For highly-sensitive secrets, we don't put them in Environment Variables at all. We fetch them dynamically from AWS Secrets Manager inside the code.

1. We have a complex workflow: 'Download -> Validate -> Transform -> Load'. Should we write one giant Lambda or four small ones? How do they talk to each other?
    - The Answer: We should break them into four small Lambdas (Microservices principles), but never have Lambda A call Lambda B directly.
    - The Anti-Pattern: 'Lambda Chaining' (A calls B, waits for result). You pay for A waiting while B runs. It couples them tightly.
    - The Solution: Use AWS Step Functions.
    - Why: It is a state machine that orchestrates the flow. It handles retries, error catching, and passing data between steps visually. If 'Validate' fails, Step Functions stops the flow without triggering 'Transform'.

1. You are connecting Lambda to a relational database (RDS). You see 'Too Many Connections' errors even with low traffic. You already set Reserved Concurrency. What else is missing?
    - The Answer: We likely need Amazon RDS Proxy.
    - The Problem: Traditional databases (MySQL/PostgreSQL) are designed for long-lived connections (like from a web server). Lambda is ephemeral; it opens and closes connections rapidly. Even a few hundred Lambdas can exhaust the database's memory by opening hundreds of separate connections.
    - The Solution: RDS Proxy sits between Lambda and the DB. It maintains a pool of warm connections to the DB and shares them among the Lambda instances. It makes the architecture much more resilient to spikes.

1. In a Kinesis stream, if one record in a batch causes the Lambda to crash, the entire batch is retried effectively blocking the shard. How do you fix this 'Poison Pill' scenario?
    - The Answer: We use `BisectBatchOnFunctionError`.
    - How it works: If a batch of 100 records fails, Lambda splits it into two batches of 50 and retries. If 50 fails, it splits to 25.
    - The Result: It recursively isolates the single bad record ('Poison Pill').
    - Final Step: Once isolated, that single bad record is sent to a Destination (Dead Letter Queue) so we can examine it, and the shard proceeds with the valid records. This prevents data stalls.

1. Your Lambda function needs to process a 5GB file, but the `/tmp` storage limit (historically 512MB, now 10GB) is filling up, or you need to share this file across multiple concurrent function executions. What do you do?
    - The Answer: I would mount an EFS (Elastic File System) volume to the Lambda.
    - The Concept: EFS provides a scalable network file system.
    - Use Case:
        - Reference Data: If 1,000 Lambdas all need to read the same 10GB ML model file, I put it on EFS. They all mount it instantly without downloading it from S3 every time.
        - State Sharing: One Lambda can write a file to EFS, and another Lambda (or EC2) can read it immediately.

1. You moved your Lambda to a VPC to access a private database. Now you are paying a fortune for 'NAT Gateway Data Processing' charges because the Lambda also downloads from S3. How do you reduce costs?
    - The Answer: We should use a VPC Gateway Endpoint for S3.
    - The Cost Trap: When a private Lambda talks to S3 (public service), traffic goes: Lambda -> NAT Gateway ($$$) -> Internet -> S3. You pay for every GB processed.
    - The Fix: Create a Gateway Endpoint. It adds a route to the VPC Route Table.
    - The Result: Traffic goes Lambda -> VPC Endpoint (Free) -> S3. It bypasses the NAT Gateway entirely, stays on the private AWS network, is faster, and costs zero for data transfer.

1. How did you optimize the cost/performance ratio of your compute-heavy Lambda functions?
    - The Answer: We switched the architecture to Graviton2 (Arm64).
    - Simple Explanation: AWS developed their own processor (Graviton).
    - The Benefit: It is generally 20% cheaper and provides up to 40% better performance for many workloads compared to x86 (Intel).
    - Migration: For Python/Node.js interpreted languages, it's often as simple as changing a dropdown setting in the console. For compiled languages (Java/Go), we just recompile the binary.

## Error-Based Questions
1. You have a Lambda function that processes a CSV file uploaded to S3. It works fine for small files. Suddenly, a user uploads a 500MB file, and the function fails with Task timed out after 3.00 seconds. You increase the timeout to 5 minutes, but it still fails. Why?
    - The Answer: Increasing time isn't enough; we need to check Memory.
    - The Constraint: Lambda allocates CPU power proportional to the Memory you give it. If I allocate the minimum (128MB), I get a tiny fraction of a vCPU.
    - The Problem: Processing a 500MB file with 128MB RAM will likely cause the function to swap to disk (which is slow) or just run out of RAM, making the process so slow it times out anyway.
    - The Fix: Increase the Memory (e.g., to 1024MB or 2048MB). This gives more RAM and more CPU power, likely making the processing fast enough to finish within the window.

1. You deployed your Python Lambda code using a ZIP file. It fails immediately with `Runtime.ImportModuleError: Unable to import module 'lambda_function': No module named 'pandas'`. You definitely included pandas in the ZIP. What happened?
    - The Answer: This is usually a OS/Architecture Mismatch.
    - The Cause: You likely installed pandas on your local machine (Windows or Mac/M1) and zipped it. However, Lambda runs on Amazon Linux 2 (x86 or ARM). Python libraries often have C-extensions that are OS-specific.
    - The Fix: Use AWS Lambda Layers that are pre-built for the correct architecture. Or, build your deployment package using Docker (`sam build --use-container`) to ensure the libraries are compiled for Amazon Linux.

1. Your Lambda powers a real-time API. Users complain that the first request of the day takes 5 seconds, but subsequent requests take 200ms. What is this, and how do you fix it?
    - The Answer: This is a Cold Start.
    - Explanation: When Lambda hasn't run in a while, AWS shuts down the container. For the next request, AWS has to provision a new microVM, download your code, and start the runtime (Java/Python). This takes time.
    - The Fix:
        - Provisioned Concurrency: You pay AWS to keep a set number of containers 'warm' and ready 24/7.
        - Optimize Imports: Move heavy imports (like `import boto3`) outside the handler function so they remain initialized if the container is reused.

1. Your Lambda function connects to a database to write some data. During a traffic spike (1,000 requests/sec), your Lambda scales up perfectly, but your Database crashes. Why?
    - The Answer: Lambda scales horizontally (1,000 requests = 1,000 concurrent containers).
    - The Problem: Each container opens a new database connection. A traditional database (like MySQL/Postgres) cannot handle 1,000 concurrent connections; it runs out of memory and crashes.
    - The Fix:
        - RDS Proxy: Use AWS RDS Proxy to pool connections. The 1,000 Lambdas talk to the Proxy, and the Proxy shares ~50 connections to the DB.
        - Move Connection Logic: Initialize the DB connection outside the handler (global scope). If a container is reused, it reuses the existing connection.

1. You are using Lambda to process a Kinesis Data Stream. You notice the `IteratorAge` metric in CloudWatch is increasing (from 0ms to 2 hours). The function isn't failing errors. What is happening?
    - The Answer: Your Lambda is processing slower than the data arrival rate.
    - The Scenario: Data is coming in at 1,000 records/sec. Your Lambda takes 5 seconds to process a batch of 100 records. You are falling behind.
    - The Fix:
        - Increase Batch Size: Process more records per invocation to reduce overhead.
        - Parallelization Factor: Allow multiple Lambdas to process the same shard concurrently (this breaks strict ordering but increases throughput).
        - Optimize Code: Increase Memory/CPU to make the processing faster.

1. A Lambda function processes payments from an SQS queue. A bug caused the function to crash halfway through. AWS retried the message. Now the customer has been charged twice. How do you architect this to prevent double billing?
    - The Answer: We must make the Lambda Idempotent.
    - The Logic: We assume any Lambda can run multiple times for the same event (At-Least-Once Delivery).
    - The Fix:
        - Check before Act: Before charging, query DynamoDB with the TransactionID.
        - Conditional Write: Use a DynamoDB Conditional Write: 'Only write this transaction if TransactionID does not exist'. If the write fails (meaning it already exists), we know this is a retry, and we stop execution immediately.

1. You have a Lambda that downloads a large video file to process it. You are writing it to /tmp. It works for 500MB files, but fails for 2GB files with No space left on device. You increased the Lambda RAM to 10GB, but it still fails. Why?
    - The Answer: Lambda's RAM and Ephemeral Storage (/tmp) are configured separately.
    - The Error: Historically, /tmp was fixed at 512MB. Increasing RAM did not increase disk space.
    - The Fix: Go to the Lambda configuration and explicitly increase the Ephemeral Storage setting (up to 10GB).
    - Better Architecture: Streaming. Instead of downloading the whole file to disk, verify if you can read the S3 stream and process it in chunks in-memory to avoid hitting disk limits entirely.

1. You have a critical Lambda function OrderProcess that runs fine. Suddenly, it starts getting Rate Exceeded (429 Throttling) errors. You check the metrics, and it is only running 50 concurrent instances (far below the 1,000 account limit). Why is it being throttled?
    - The Answer: You likely have a 'Noisy Neighbor' in the same AWS account.
    - The Logic: The default concurrency limit (e.g., 1,000) is shared across ALL functions in the account.
    - The Cause: A different function (e.g., a dev log processor) might be scaling up to 950 instances, leaving only 50 slots for the rest of the account. Your critical function is fighting for scraps.
    - The Fix: Set Reserved Concurrency for the critical function. This guarantees it a specific number of slots (e.g., 200) that no other function can steal.

1. You are deploying a Lambda function that needs to connect to 10 different internal microservices. You added all 10 API Keys and URLs into the Environment Variables. Now, the deployment fails because Lambda was unable to configure your environment variables. Why?
    - The Answer: You hit the 4KB Limit for Environment Variables.
    - The Limit: The total size of all key-value pairs cannot exceed 4KB.
    - The Fix:
        - SSM Parameter Store: Store the config in AWS Systems Manager (SSM) or Secrets Manager.
        - Fetch on Init: In your Lambda code (outside the handler), call the SSM API to fetch the JSON configuration and cache it in a global variable.

1. Your Lambda reads from Kinesis. One specific record contains bad JSON (a 'Poison Pill'). Lambda tries to parse it -> Crashes. Lambda retries the same batch -> Crashes. This repeats forever. The shard is blocked, and valid data behind it is piling up. How do you fix this without losing the valid data in that batch?
    - The Answer: We use 'Bisect Batch on Function Error'.
    - The Feature: In the Event Source Mapping configuration, enable 'Bisect on Error'.
    - The Logic: When the batch fails:
        1. Lambda splits the batch into two halves.
        1. It retries each half separately.
        1. It keeps splitting until it isolates the single bad record.
    - The Result: The bad record is sent to a Dead Letter Queue (DLQ) (if configured), and all the valid records in the batch are processed successfully.

1. You have an architecture: S3 Event -> Lambda. The Lambda logic fails due to a bug. You check the S3 bucket, but you see no error message, and the S3 service reports 'Success'. You only realized data was missing days later. Why didn't you get an alert?
    - The Answer: S3 invokes Lambda Asynchronously.
    - The Mechanism: S3 hands the event to Lambda's internal queue and walks away. It doesn't wait for the code to run. If the code crashes later, S3 doesn't know.
    - The Fix: Configure an 'On-Failure Destination'.
        - Setup: Point the Lambda's 'Async Configuration' to an SNS Topic or SQS Queue for failed events.
    - Result: If the function retries 3 times and still fails, Lambda (the service) automatically sends the event payload to SNS so you get an alert.