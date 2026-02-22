# Amazon Web Services (AWS)

## Identity and Access Management (IAM)
- IAM is an AWS core service used to securely access AWS resources. It controls both authentication (identity) and authorization (permissions).
- IAM Core Concepts:
  - User: A resource that has associated credentials and permissions.
  - Group: A collection of users. Permissions can be assigned to a group and these permissions will be inherited by all users in the group, instead of assigning individual permissions to each user.
  - Policy: A JSON document specifying permissions.
  - Role: An entity created and assigned specific permissions.
- IAM Users:
  - When a user is created, it is assigned a user name and password that will be used to sign into the AWS Management Console under a specific account ID. The actions they can perform in the console are determined by the permissions assigned to the user.
  - When a user is created, permissions can be assigned to the user in one of three ways:
    - Permissions can be inherited from a group by assigning the user to a group.
    - Permissions can be copied from an existing user.
    - Permissions can be manually assigned to a user by attaching policies to the user entity.
- IAM Groups:
  - When a group is created, you have the option to add users to the group and attach permissions to the group that all users will inherit. Users and permissions can be modified after creation.
- IAM Policies
  - The two main types of policies that IAM offers are customer-managed policies and AWS-managed policies.
  - When you create a customer-managed policy, you will be given the option to create a policy visually, using drop-down menus, or manually, by creating a JSON object.
  - The default JSON object associated with a policy can look like:
    ```
    "Version": "2012-10-17",
    "Statement": [
      {
        "Sid": "ListObjectsInBucket",
        "Effect": "Allow",
        "Action": ["s3:ListBucket"],
        "Resource": [
          "arn:aws:s3:::bucket-name",
          ]
      }
    ]
    ```
    - Statement ID (Sid): The identifier for the statement. A policy can contain multiple statements. In this case, `"ListObjectsInBucket"`.
    - Effect: Whether permission is being granted or denied. In this case. `"Allow"`.
    - Actions specify the AWS service, as well as the action associated with that service. In this case, `"s3:ListBucket"`.
    - Resources specify the AWS resources on which the specified actions can be applied. In this case, `"arn:aws:s3:::bucket-name"`.
    - Actions and resources for a statement must relate to the same AWS services.
  - Once the policy is specified, you can give it a name and description and add tags.
- IAM Roles:
  - When you create a role, you will be asked to select a trusted entity, which will typically be an AWS account or service.
  - Once you select a trusted entity, you will be asked to add permissions by selecting AWS or customer-managed policies.
  - Once permissions are added, you will be asked to specify a name and description for the role and add tags.

## Simple Service Storage (S3)
- S3 is a reliable and scalable storage service that stores files of different types, such as text, video, image etc. S3 is typically used for data storage, backup and recovery of critical data, static website hosting (HTML and CSS files), and big data analytics.
- The two primary entities in S3 are buckets and objects.
  - Buckets are used for data storage and contain policies and configurations which determine how users can control and manipulate the data. Bucket names must be globally unique. The maximum size of an S3 bucket is 5TB.
  - Objects are any entity that is stored in a bucket.
- S3 Buckets:
  - When you create an S3 bucket, you will first be asked to choose the bucket type, which will either be general purpose or directory. General purpose buckets are used for general-purpose object storage and offer high durability and availability. Directory buckets are used in scenarios that require high-performance, low-latency, and consistent performance requirements, such as data-intensive applications. In most use cases, you will select general purpose.
  - After choosing the bucket type, you will specify the bucket name, which must be _globally_ unique.
  - When choosing settings for your bucket, you will be given the opportunity to copy settings from an existing bucket.
  - Ownership of objects within a bucket fall into two categories:
    - ACLs disabled (recommended): All objects within the bucket are owned by the associated AWS account and access to the bucket and objects within it are controlled by using IAM policies.
    - ACLs enabled: Objects in the bucket can be owned by other AWS accounts and access to the bucket and its objects are controlled using one or more Access Control Lists (ACLs).
  - After specifying ownership settings, you will be asked to specify public access settings. "Block all public access" is selected by default and recommended.
  - After specifying public access settings, you will be asked to enable or disable (default) bucket versioning. Bucket versioning is a feature that assigns a unique version ID to every object modification, allowing for protection against accidental overwrites or deletions by allowing you to retrieve variants of an object using the version ID.
  - After specifying bucket versioning, you will be given the option to add tags and select the type of encryption. The default encryption type is server-side encryption using S3-managed keys.
- S3 Objects:
  - Once a bucket is created, objects can be added to it by manually uploading files to the bucket.
  - Folders can be created within a bucket to categorize objects as needed.
  - Objects and folders can be copied and moved to different s3 destinations as needed. Objects can also be deleted as needed.
- S3 Replication:
  - S3 replication is a fully-managed feature that allows you to automatically replicate S3 objects from one bucket to another to help with reducing cost, protecting data, and achieving compliance with regulatory requirements.
  - Cross-Region Replication (CRR) replicates objects to buckets across multiple AWS regions.
  - Same-Region Replication (SRR) replicates objects to buckets within the same AWS region. 
  - **Replication will only work on S3 buckets (source and destination buckets) which have bucket versioning enabled.**
  - Replication is enabled by creating a replication rule in the source bucket. When creating a replication rule, you can choose to apply the rule to all objects in the bucket, or limit the scope to certain objects, such as objects within a certain folder.
    - After choosing the scope of the rule, you can choose the destination bucket as one in the same AWS account or one in a different AWS account.
    - After choosing the destination bucket, you must specify an IAM role by either choosing from an existing role or allowing AWS to create a role for you.
- S3 Versioning:
  - Versioning is an S3 feature that allows storage of multiple variations of an object within an S3 bucket. This allows you to preserve, retrieve, and restore every version of every object within a bucket. This can help to correct accidental deletion or modification of an object.
  - A bucket can either be unversioned, version-enabled, or version-suspended. Once versioning is enabled on a bucket, it cannot go back to being unversioned, versioning can only be suspended.
  - Versioning is typically enabled or disabled when a bucket is first created.
  - In a versioned bucket, when multiple versions of the same object are uploaded to the bucket, the most recent version will appear in the UI. When you click on this version and navigate to the 'Versions' tab, you will be able to see all previous versions of the object.

## Lambda
- Lambda is a serverless compute service that allows you to create functions which are fully managed by AWS. These functions can be executed without having to independently provision or manage servers.
- Lambda is typically used for event-driven data processing. Other uses cases include:
  - File Processing - Lambda functions can be triggered using S3, such that, whenever files are uploaded, data processing is triggered.
  - Web Applications - Lambda functions can be used to automatically scale services within a web application based on incoming traffic.
  - IoT (Internet of Things) Applications - Lambda functions can be triggered based on certain conditions while processing data from a device connected to an IoT application.
  - Stream Processing - Lambda functions can be integrated with Amazon Kinesis to process real-time streaming data for application tracking, log filtering, etc.
- AWS Lambda Features:
  - Autoscaling and High Availability - Lambda will automatically scale based on incoming traffic to an application, ensuring high availability.
  - Serverless Execution - There is no need to manually provision servers. Provisioning of servers is handled automatically by AWS.
  - Pay-Per-Use Pricing - AWS will only charge you for the time during which the compute engine is active (i.e. based on the time taken to execute the code).
  - Supports Different Programming Languages - Python, Node.js, Java, C#, PowerShell, and Go.
  - Integrates With Other AWS Services - API Gateway, Dynamo DB, S3, Step Functions, SNS, SQS. 
- Lambda is used by first creating lambda functions. This can be done by uploading code or manually creating a function. Once the function is created, it needs to be configured to trigger from other AWS services, HTTP endpoints, or mobile apps, based on certain conditions.
- Creating a Lambda Function:
  - When creating a function, you can either start from scratch, using a blueprint provided by AWS, or a container image.
  - After choosing how you want to create your function, you will give it a name, select a runtime programming language, architecture (x86_64 or arm64), and customize permissions by selecting an execution role. You can allow AWS to create default execution role (allowing lambda to upload logs to CloudWatch), select an existing IAM role, or create a new role from AWS policy templates.
- Once a function is created, an event needs to be specified to trigger execution of the underlying code. This is done by created a `lambda_handler` function within the code. This function needs to accept an `event` and `context`. This function acts as the entry point for the code that will be executed by lambda (unlike a script where code is typically executed starting from the first line of code in the file to the last line).
  - The `event` parameter will specify the event data that will be used to trigger the function. This parameter typically comes in the form of JSON.
  - The `context` parameter will specify runtime information about the lambda function, such as the function name and request id.
- The activity of a lambda function can be monitored through its associated CloudWatch log group.
- Adding triggers to a lambda function will allow it to trigger based on events that occur elsewhere, such as in other AWS services.
- Lambda also provides the option to set up destinations, such as an SNS topic or SQS queue, where invocation records for the lambda will be sent either for successful execution or execution failure (not both).

## Secrets Manager
- Secrets manager is a service used to store and manage access to confidential information, such as passwords, credentials, and third-party security keys. It allows you to replace hard-coded credentials in your code with an API call to secrets manager to retrieve credentials programmatically.
- Secrets manager encrypts the text of a secret using AWS Key Management Service.
- Important Features:
  - Rotate Secrets Safely - Secrets can be easily changed to ensure security and compliance with regulatory standards.
  - Secure and Audit Secrets Centrally - Secrets can be secured using encryption keys that are also managed by the service.
  - Pay As You Go - You will only be charged for the number of secrets managed by the service and the number of API calls made to the service.
  - Retrieve Secrets Programmatically - Programmatically retrieve encrypted secret values at runtime. This allows applications that rely on these secrets to seamlessly retrieve updates without the need to manually update their code.
- Create and Use Secrets:
  - When you need to connect to an external service or entity, such as Snowflake, in your python code, you either hard code the necessary credentials directly into the code, or retrieve them programmatically from secrets manager. Retrieving credentials from secrets manager is safer because it prevents anyone with access to the code from retrieving the credentials.
  - When you create a secret in secrets manager, you will be asked to choose the type of secret, which can vary from credentials for an AWS service to credentials for a third-party service or database or other types of secrets, such as API keys.
    - The first two types of secrets (AWS or third-party credentials) will require you to specify a username and password.
    - The third type secret (other) requires you to specify key-value pairs.
  - After specifying your credentials or key-value pairs, you can select the type of encryption key you want to use, which will default to an encryption key managed by secrets manager.
  - After specifying the type of encryption key, you will be asked to provide an name and description, as well as add tags if needed. You can also choose to apply a permissions resource policy to the secret and replicate the secret to other AWS regions.
  - Next, you will be asked configure automatic rotation (optional) and provide a rotation schedule, if needed, and specify a lambda rotation function to perform the rotation.

## Simple Notification Service (SNS)
- SNS is a web service that allows you to easily set up, operate, and send notifications from the cloud. It provides developers with a highly-scalable, cost-effective, flexible capability to publish messages from an application and send them to another application.
- The three key entities in SNS are publishers, subscribers, and topics. Publishers, also known as producers, send messages to SNS, which acts as a logical process point for subscribers. Subscribers, such as web servers, email addresses, AWS SQS queues, and AWS Lambda functions, receive the message or notification from the producer. A topic is a grouping of messages that will be sent only to users that are subscribed to the topic.
- Benefits of SNS:
  - Instantaneous Delivery - SNS is based on push-based delivery, where messages in a topic can be delivered to multiple subscribers.
  - Flexible - SNS supports multiple endpoint types, such as email addresses, SMS, AWS Lambda, AWS SQS, and HTTP.
  - Inexpensive - SNS uses a pay-as-you-go model, where you are only charged for compute resources used, with no upfront costs.
  - Ease of Use - SNS is very simple to use.
  - Simple Architecture - SNS can help simplify messaging architecture by only sending messages to entities that are subscribed to a topic.
- Creating a Topic:
  -  When you create a topic, you will be asked to provide a name and choose the type. The two types of topics in SNS are first-in-first-out (FIFO) and standard.
    - FIFO topics strictly preserve message ordering, send messages exactly once, support high throughput, and allow users to subscribe from AWS SQS.
    - Standard topics utilize "best-effort" message ordering, send messages at least once, support high throughput, and allow users to subscribe from AWS SQS, AWS Lambda, HTTP, SMS, email, and mobile application endpoints.
  - After specifying the type of topic you want to create, you will be given the option to specify details such as encryption, access policies, data protection policies, delivery policies, and logging.
  - Once a topic is created, subscribers can be added to the topic by creating subscriptions. When creating a subscription, you must specify the type of protocol (SQS, Lambda, HTTP, etc.), the name of the endpoint, as well as optional subscriber filter policies and re-drive policies.
  - When a subscription is created in a topic, it must be confirmed before it can receive messages. AWS automatically sends a link to the subscriber, via the provided endpoint, to perform this confirmation.
- Publishing a Message:
  - Once a topic is created and subscribers are added and confirmed, messages can be sent to subscribers by publishing a message to the topic.
  - When you publish a message, you will be asked to provide an optional subject, an optional TTL, and a message body. You can also specify a message attribute, which consist of a name, value, and type.
  - When a message is successfully published, it is automatically sent to subscribers based on the policies associated with the topic.
  - In order for a publisher, such as S3, to publish messages to an SNS topic, that publisher must be given permission to do so by updating the access policy of the topic accordingly. In S3, you would then create an event notification in an S3 bucket that would be sent to the SNS topic, then to the associated subscribers.

## Simple Queue Service (SQS)
- SQS is a web service that gives you access to a message queue that can be used to store messages while waiting for a computer to process them. SQS allows you to send, store, and receive messages between software components at any volume, without losing messages.
- An SQS message can contain up to 256KB of text in any format, such as XML or JSON. Any message uploaded to a queue can later be retrieved programmatically from any software component of an application using the SQS API.
- The two different types of queues in SQS are standard (default) and FIFO.
  - A standard queue offers an unlimited number of transactions per second, guarantees a message is delivered at least once, and provides "best-effort" message ordering, meaning messages are generally sent in the same order in which they are received, but this behavior is not guaranteed.
  - A FIFO queue complements a standard queue and offers guaranteed message ordering, exactly-one delivery (messages remain available until a user processes and deletes it), and no duplicate messages.
- Important Caveats:
  - SQS is pull-based, not push-based (like SNS).
  - Message size is restricted to 256KB.
  - Messages can be kept in a queue from 1 minute up to 14 days.
  - The default retention period is 4 days.
  - Messages are guaranteed to be processed at least once.
- Creating a Queue:
  - When creating an SQS queue, you will first be asked to select the type (Standard or FIFO) and provide a name.
  - After selecting the type and providing a name, you will be asked to specify configuration details, such as visibility timeout, delivery delay, receive message wait time, message retention period, and maximum message size.
  - After specifying configuration details, you will be asked to select an encryption type. You can choose to enable or disable server-side encryption and you can choose between an SQS encryption key and an AWS Key Management Service encryption key.
  - After specifying encryption details, you will be asked to provide an access policy that determines the entities that can access the queue and what actions they can perform on the queue.
  - After providing an access policy, you will be given the option to specify a re-drive policy (determines which source queues can use this queue as a dead-letter queue) and whether you want to make the queue a dead-letter queue (one that receives undeliverable messages). You will also be given the option to specify tags for the queue.
- Once the queue is created, you can configure other AWS services to send messages to the queue,
- An example of using SQS would be creating a data pipeline that consists of an S3 database along with a lambda that performs ELT operations on the data. When objects are added to an S3 bucket, the bucket can be configured to send a message to an SQS queue. The lambda can then be configured to trigger when a message is added to that queue and perform the necessary operations on the data.
  - In order for the SQS queue to receive event notifications from the S3 bucket, it must be configured with the necessary permissions in its  access policy.

### Differences Between SNS and SQS
- Model: SNS uses a **push-based** publisher/subscriber model that is primarily used for real-time notifications to one or more subscribers. SQS uses a **poll-based** queue model that is primarily used for one-to-one message queueing, decoupling, and asynchronous processing.
  - Messages in SNS are sent instantly to subscribers while messages in SQS must be polled in order for consumers to retrieve and process messages.
- Message Retention: SNS does not persist messages; if subscribers are down, the message is lost. SQS persists messages in a queue for up to 14 days while waiting for the message to be polled by a consumer.
- Recipients: SNS supports one-to-many (fan-out) messaging. SQS typically supports one-to-one messaging.
- Use Cases: Use SNS for real-time alerts, mobile notifications, or triggering multiple microservices. Use SQS for buffering (handling traffic spikes), load balancing, decoupling processes, or background jobs.
  - SQS is used to decouple the Tenor Service from the Cache Warmer Service.
- Subscriber Type: SNS supports HTTP/S endpoints, Email, SMS, Lambda, and SQS queues. SQS supports worker applications, EC2 instances, or Lambda functions polling the queue.
- SQS and SNS can be used together in a "fan-out" pattern, where multiple SQS queues are subscribed to an SNS topic. SNS handles the broadcasting of a single event to multiple destinations. SQS provides durability, ensuring that if a downstream service is down, the message stays in the queue until it can be safely processed.
- Choosing Between The Two Services:
  - Choose SQS if you have a single worker that needs to process a list of tasks at its own pace without losing data during spikes.
  - Choose SNS if you need to instantly notify multiple different systems or people about the same event.

## Step Functions
- AWS Step Functions is an orchestration service that allows you to use multiple AWS services to accomplish a task.
- Step functions allow you to create steps in a process where the output of one step becomes the input of the proceeding step, all using a visual workflow editor.
- Step functions provides convenient functionalities, including automatic retry handling, triggering and tracking for each workflow step, and ensuring steps are executed in the correct order.
- Step functions are based on state machines and tasks:
  - A state machine is a workflow.
  - A task is a state in a workflow that represents a single unit of work that another AWS service performs.
  - Each step in a workflow is considered a state.
- An example of a step function is an online checkout process on an e-commerce website. The step function could consist of a series of lambda functions. The first lambda will check if the selected product has available stock. The second lambda bills the customer for the product. The third lambda ships the item to the customer.
- Benefits of Step Functions:
  - Step functions is a low-code, visual workflow service that developers use to build distributed applications, automate IT and business processes, and build data and machine learning pipelines using AWS services.
  - Workflows manage failures, retries, parallelization, service integration, and observability so developers can focus on more important business logic. Other features include:
    - Easy to connect with workflow editor.
    - Easy to integrate with other AWS services like SNS, SQS, Batch, and Fargate.
    - Automatic scaling based on the workload of the state machine.
    - Manage state checkpoints and restarts to ensure the application executes in order.
    - It can handle errors, rollback, and retries.
    - Logs each state. 
- Uses Cases:
  - Automate Extract, Transform, and Load (ETL) processes - Ensure that multiple, long-running ETL jobs run in order and complete successfully, without the need for manual orchestration.
  - Orchestrate Microservices - Combine multiple AWS Lambda functions into responsive, serverless applications and microservices.
  - Orchestrate Large-Scale, Parallel Workloads - Iterate over and process large data sets such as security logs, transaction data, or image and video files.
  - Automate Security and IT Functions - Create automated workflows, including manual approval steps, for security incident response.
- Step Function Example (Order State Machine):
  - The following step function will consist of various lambda functions which perform different tasks in the online ordering process. One lambda function calls a purchase handler, another lambda function calls a refund handler, and the other lambda function calls a result handler.
  - The state machine starts with a choice between "refund" and "purchase", which decides whether the purchase-handler or refund-handler lambda is called. Once either of these lambda functions is completed, they will call the result handler.
- Creating a State Machine:
  - When you create a state machine in step functions, you will be given the choice to choose among various templates or create your own custom state machine.
  - When creating a custom state machine, you will do so in a workflow editor that allows you to add elements to the state machine. Elements can either be actions, flows, or patterns. Actions are AWS services. Flows consist of various types elements, including choice, parallel, map, pass, wait, succeed, and fail.
    - Choice adds branching logic by comparing input data against defined rules (e.g., if/else) to determine which state to transition to next.
    - Parallel executes multiple branches of the workflow simultaneously. The state waits until all branches finish before moving to the next step.
    - Map dynamically iterates over an input array and runs a set of steps for each item. It supports Inline (for smaller datasets) and Distributed (for high-concurrency processing of millions of items) modes.
    - Pass passes its input to its output without performing work. It is often used to transform JSON data or inject fixed data for debugging.
    - Wait pauses the execution for a specific duration or until a specific timestamp is reached.
    - Succeed is a terminal state that stops the execution successfully.
    - Fail is a terminal state that stops the execution and marks it as a failure, allowing you to specify an error name and cause. 
  - After building the workflow in the editor, you will need to provide other details about the state machine, such as the name and permissions. By default, step functions will create an IAM role with all required permissions to execute the various services being used in the workflow. However, you can also choose your own IAM role.

## Kinesis
- Kinesis allows users to process large amounts of data per second in real time. It is primarily used to analyze streaming data and process it for later use at large amounts of scales.
- Kinesis is fully managed by AWS, making it easy to capture, process, and store streaming data in the cloud.
- Kinesis allows developers to build applications that continuously ingest, process, and analyze data streams from various sources, such as application and service logs, clickstream data, sensor data, and in-app user events.
- How AWS Kinesis Works:
  - Data Ingestion - Kinesis collects or receives data from various data steams, including applications, sensors, etc.
  - Sharding and Scaling - Data is divided into smaller shards for redundancy and fault tolerance. There are no limits to the number of shards. Shards can be scaled horizontally based on business requirements.
  - Processing and Buffering - After sharding, data is prepared for further use.
  - Data Accessability - After completing the above steps, the data is made accessible in various ways.
- Services Offered:
  - Kinesis Data Streams - Provides a platform for real-time, continuous processing of data.
  - Kinesis Data Analytics - Allows streams of data provided by kinesis streams to be processed and analyzed with standard SQL.
  - Kinesis Data Firehose - Helps users reliably capture, transform, and load streaming data into AWS data stores and analytics services.
- Features Offered:
  - Cost Efficient - Kinesis, like other AWS services, follows a pay-as-you-go model where users are only charged actual resource utilization, with no flat upfront costs.
  - Integration With Other AWS Services - Allows users to integrate kinesis with other AWS services such as Dynamo DB and Redshift, which handle large amounts of data.
  - Availability - The service can be accessed from anywhere at any time.
  - Real-Time Processing - Allows real-time data processing.
- Use Cases:
  - Real-Time Application Monitoring - Provides access to real-time application data.
  - Fraud Detection and Prevention - Helps protect data from fraudulent activity by analyzing transaction data, detecting suspicious patterns, and blocking fraudulent transactions before they occur.
  - Personalized Recommendations and Marketing - Helps analyze customer data which can be used to better understand customer behavior and offer meaningful product recommendations in real time.
  - IoT Analytics and Predictive Maintenance - Examines sensor data from electronics, automobiles, and machinery.
- Creating and Using a Data Stream:
  - When creating a data stream, you will first be asked to provide a name and choose between on-demand and provisioned data stream capacity.
  - Once a data stream is created, producers can write data to the stream and consumers can read data from the stream.
  - Python scripts can act as a producer when they are written to send data to a data stream.
- Creating and Using Data Firehose:
  - A data firehose allows you to send data ingested by a data stream to another AWS service for storage or analytics.
  - When creating a data firehose, you will be asked to select a source, such as a kinesis data stream and a destination, such as an S3 bucket.
  - After choosing a source and a destination, you will be asked to specify the source settings, such as the specific data stream from which you want to ingest data.
  - After specifying the source settings, you will be given the option to transform source records with AWS Lambda, convert the record format, and decompress source records.
  - After choosing whether you want to transform source records, you will be asked to specify destination settings, such as the specific S3 bucket in which you want to store the ingested, transformed data.
  - Firehose writes data to the source based on the buffer size and interval. The buffer size specifies how much data must be ingested before it is sent to the source (recommended is 5MB) and the interval specifies how often data should be sent to the source. Firehose will send data to the source based on whichever (size or interval) requirement is met first.

## API Gateway
- API Gateway is a fully managed service that streamlines the publishing, maintenance, monitoring, and security of APIs at any scale.
- APIs act as a server between client applications and backend services. They are responsible for routing the request from the client side to the appropriate backend service, as well as performing other tasks, such as authentication, authorization, and traffic management.
- Key Features:
  - Traffic management.
  - Authentication, authorization, and access control.
  - Throttling,
  - Load balancing.
  - Caching.
- How API Gateway Works:
  - An API gateway endpoint receives requests from clients.
  - API gateway routes the request to the appropriate backend service.
  - After processing the request, the backend service sends a response to the client that is routed through API gateway.
- Supported API Types:
  - Public and Private REST APIs - Representational State Transfer (REST) is an architectural style that defines a set of constraints to be used for creating web services. REST APIs provide a simple and flexible way of providing access to web services without having any processing.
  - SOAP APIs - Simple Object Access Protocol (SOAP) is a network protocol for exchanging structured data between nodes.
  - Web Socket APIs - A framework used to develop HTTP-based RESTFUL services.
- Key Benefits:
  - Simple to Use - The AWS console provides a simple UI that makes it easy to create and manage APIs using API gateway.
  - Scalable - API gateway is backed by the highly scalable and reliable AWS infrastructure.
  - Secure - API gateway offers capabilities such as custom authorizers and integration with IAM to help with properly securing access to APIs.
  - Exposes Backend Services - Allows backend services to be exposed to external clients such as web applications, mobile applications, and other APIs.
- API Setup:
  - When you create an API, you will first be asked to choose between several API types, including HTTP, Web Socket, and REST APIs.
  - After selecting the API type, you will be asked to provide API details, including whether the API is a new API, import API, or clone of an existing API, as well as the API name, description, and endpoint type (Regional by default).
  - After providing API details, you will be asked to provide resources (paths) that will be apart of the invocation URL. When a resource name will be dynamic, such as the name of an S3 bucket, it should be placed in curly braces (i.e. `{bucket_name}`).
  - After creating resources, you need to specify methods (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`) for those resources. Once the method is chosen, you need to specify which service the API will integrate with. If you select an AWS service as the type of integration, you will need to specify the service, region, HTTP method, action type (action name or path override), and execution role (Allows API gateway to perform the necessary actions, like uploading a file to S3).
    - Path override should be used when the filepath depends on the specific resource (bucket and filename) being acted on.
- Once the API is set up, the URL path parameters need to be updated in the integration request settings.
- Once all of the API settings have been properly updated, the API must be deployed before it can be used.

## Cloud Watch
- CloudWatch is a monitoring and observability service that enables users to collect and track metrics, monitor log files, set alarms, and automatically react to changes in AWS services. It helps users gain insights into the operational health, performance, and resource utilization of their AWS infrastructure and applications.
- CloudWatch collects monitoring and operational data from applications in the form of logs, metrics, and events, providing users with an aggregated view of AWS resources, applications, and services.
- CloudWatch can also be used to detect anomalous behavior, set warnings and alarms, visualize logs and metrics side by side, take automated actions, and troubleshoot issues.
- Key Features:
  - CloudWatch Dashboard - A user-friendly console used for monitoring resources in a single view. There is no limit to the number of dashboards that can be created and these dashboards are not region-specific.
  - CloudWatch Agent - Collects logs and system-level metrics from AWS EC2 instances and on-premises servers (most be installed on the service from which it collects logs and metrics).
  - CloudWatch Events:
    - An event indicates a change in an AWS environment. Whenever there is a change in the state of AWS resources, an event is generated.
    - Events can be routed to one or more targets, such as a Lambda function, SNS topic, and SQS queue. Rules are used for matching events and routing to targets.
  - CloudWatch Logs - Enables you to store, monitor, and access files from AWS resources such as EC2 instances and Route 53. It also helps troubleshoot system errors and maintain logs in highly durable storage.
- Benefits:
  - Allows for easy collection, organization, and summarization of large amounts of data.
  - Improves the total cost of ownership by providing alarms and taking automatic actions when an error occurs.
  - Optimizes applications and resources by examining logs and metrics data.
  - Provides detailed insights from the application such as CPU and memory utilization.
  - Provides a great platform to compare and contrast data produced by various AWS services.
- Use Cases:
  - Used to monitor the performance of various AWS services, applications, and infrastructure components in real time.
  - Allows users to set up alarms that trigger notifications or automated actions in response to changes in the state of a resource.
  - Used to store, search, and analyze log data from various AWS services, applications, and infrastructure components.
  - Used to monitor the performance of EC2 instances, RDS databases, and other resources, which can be used to trigger automatic scaling events.

## Athena