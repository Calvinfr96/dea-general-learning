# AWS S3 Interview Questions

## Basic Questions
1. What is AWS S3?
    - Answer: AWS Simple Storage Service (S3) is a service for storing objects. It has the best scalability, data availability, security, and performance in the business.
    - It is mainly used for storing and retrieving any amount of data. It has various use cases, including data backup, archiving, content distribution, and various other use cases and data stored in S3 Bucket.

1. What is Bucket In AWS?
    - Answer: An S3 bucket is like a huge hard drive in the cloud that can store a lot of data, like files and any number of objects.
    - In AWS S3, things are stored in buckets, and each thing is called an object. Each object has its own unique key, given by the user.

1. What is the maximum size of an object that can be stored in S3?
    - Answer: The maximum size of an object that can be stored in S3 is 5 terabytes.

1. How is data stored within an S3 bucket?
    - Answer: An S3 bucket is like a folder on your computer for storing files. Whatever it is has its own name, and the bucket is like the main folder that stores all the information. So, it’s a bit like organizing your digital data into folders in the cloud.

1. What are the different storage classes in AWS S3?
    - Answer:
        1. Standard S3 Storage Class
        1. S3 Standard Storage Class for Infrequent Access
        1. S3 Reduced Redundancy Storage Class
        1. S3 Glacier Storage Class

1. Explain the concept of versioning in AWS S3.
    - Answer:
        - Versioning in AWS S3 is storing different versions of an object in the same AWS S3 bucket. With S3 Versioning, you can keep, get, and restore all versions of any object saved in your buckets.
        - Also it keeps a history of your digital files. Imagine you have a document, and you make changes to it over time. With versioning, S3 saves a copy of each change you make.
        - If you lose something by accident or make a mistake, you can go back in time and get the version of the file you need. It’s like making a copy of every change, so you will never lose important information in the cloud.

1. What is the significance of a unique object key in S3?
    - Answer: In AWS S3, each object has a unique object key, which is like a name. It helps S3 keep track of everything you store and find it when you need it.

1. How can you secure data in S3?
    - Answer: S3 provides various security mechanisms such as:
        - Bucket Policies
        - Access control Lists (ACLs)
        - Identity and Access Management (IAM) roles
        - You can use these to control who can access your buckets and objects.

1. Explain CORS in the context of S3.
    - Answer: Cross-Origin Resource Sharing (CORS) allows you to define which domains can access your AWS S3 resources. It’s very important for web applications hosted on one domain but needing to make requests to S3 on another domain.

1. What are ACLs in AWS S3?
    - Answer: An S3 Access Control List (ACL) is like a set of rules attached to every S3 bucket. These rules decide exactly what entities can and cannot do with the AWS S3 bucket.
    - When you make a bucket or an object, AWS S3 sets up a default set of rules giving full control to the owner.

1. How can you optimize the performance of data transfers for large files in S3?
    - Answer:
        1. Split up Big Files into Parts
        1. Enable S3 Transfer Acceleration
        1. Monitor and analyze performance metrics
        1. Choose the right storage class based on access frequency
        1. Improve data compression to cut down on file sizes and transfer times.

1. How To Host Websites In AWS S3?
    - Answer: To host a website in AWS S3, We have to follow these steps:
        1. Create an S3 Bucket
        1. Configure Bucket for Website Hosting
        1. Upload Website Files
        1. Set Permissions
        1. Configure DNS
        1. Access Website

1. What tools does AWS offer for monitoring S3?
    - Answer:
        1. AWS CloudWatch
        1. AWS CloudTrail
        1. AWS Config
        1. AWS S3 Storage Lens

1. Define the concept of event notifications in S3.
    - Answer: Event notifications in AWS S3 are like sending notifications to inform an external system or application when specific events occur within an S3 bucket.
    - This service allows you to automate responses or take actions in response to changes or events in your S3 storage, such as when a new object is created or an existing object is deleted.
    - For example: A message can be shown to you by S3 if someone adds a new file to your bucket. 

1. What is AWS S3 Replication?
    - Answer: Amazon S3 Replication is a feature that automatically replicates objects between Amazon S3 buckets. It's a fully-managed, low-cost service that can help with data protection, compliance, and cost reduction.
    - Here are some types of S3 Replication: 
        1. Same-Region Replication (SRR): Copies objects between buckets in the same AWS Region. This can be used to meet compliance requirements, change account ownership, or aggregate logs. 
        1. Cross-Region Replication (CRR): Copies objects across multiple Amazon Regions. This can be used to provide users with low latency. 
        1. S3 Batch Replication: Replicates existing objects to one or more destinations. This can be used to backfill a new bucket, re-replicate objects, or migrate data across accounts. 

1. Explain the benefits of S3 versioning?
    - Answer: We can store multiple variants of an object in a bucket by versioning it. An object can be restored to a previous or specific version by versioning. If an object is deleted or accidentally overwritten, versioning can be used to recover it.

1. How to configure S3 Versioning on a Bucket?
    - Answer: Versioning helps you keep multiple versions of an object in one place. Follow these steps to enable versioning on an S3 bucket:
        1. Login to your AWS account.
        1. Choose Simple Storage Service.
        1. Choose a bucket for which versioning should be enabled.
        1. Go to the properties tab.
        1. Select versioning from properties.
        1. Click on the OK button to enable versioning.

1. How do I delete an AWS S3 bucket?
    - Answer: For deleting an AWS S3 bucket, follow these steps:
        1. Log in to the AWS Management Console.
        1. Select the Simple Storage Service.
        1. Locate the bucket you wish to delete.
        1. Press the delete button. AWS will ask you to type the bucket name you wish to delete.
        1. Enter the bucket name and click Confirm.

1. Which storage class does AWS S3 use by default?
    - Answer: Standard

## Scenario-Based Questions
1. Why did you choose S3 as your storage layer instead of a database or Elastic Block Store (EBS)?
    - The Answer: We chose S3 because it is the standard for a Data Lake.
    - Simple Explanation: EBS is like a hard drive attached to a specific computer; if the computer dies, it can be tricky. You also pay for the entire provisioned capacity and allocated performance (IOPS/throughput), regardless of how much data you actually write.
    - A Database is expensive and needs structure. S3 is like an infinite, shared file cabinet that is accessible from anywhere by any service (Glue, Athena, EMR).
    - Key Features: It offers very high durability (99.99% chance your data won't get lost), it scales automatically without us provisioning space, and it supports many file formats (JSON, CSV, Parquet, Images).

1. What is the difference between S3 Standard and S3 Glacier? When did you use which?
    - The Answer: It comes down to cost vs. retrieval speed.
        - S3 Standard: This is our 'hot' storage. We use it for data we are processing today or accessing frequently. It’s more expensive but retrieval is instant (milliseconds).
        - S3 Glacier: This is our 'cold' archive. We use it for data we are required to keep for compliance (e.g., 7 years of history) but rarely touch. It is much cheaper (pennies per TB), but if we need the data back, it can take minutes or hours to 'thaw' (retrieve) it.

1. How did you secure the sensitive data in your S3 bucket?
    - The Answer: We used a 'Defense in Depth' approach with three layers:
        - Block Public Access: We enabled the 'Block All Public Access' setting at the bucket level to prevent accidental leaks to the internet.
        - Encryption: We enabled Server-Side Encryption (SSE-S3 or KMS). This means the data is scrambled on AWS's physical disks. Even if someone stole the hard drive from the AWS data center, they couldn't read it.
        - IAM & Bucket Policies: We used strict IAM roles. Only the specific Glue Job role and the Admin team have 'Read/Write' access; everyone else is denied.

1. Explain your Partitioning Strategy in S3. Why didn't you just dump all the files in one folder?
    - The Answer: We used Hive-Style Partitioning (e.g., s3://bucket/sales/year=2024/month=01/day=15/).
    - The Problem: If you have 1 million files in one folder, finding data for 'Jan 15th' requires scanning all 1 million files. This is slow and expensive.
    - The Solution: By creating folders based on date (or region), tools like Athena and Glue can use Partition Pruning. They skip the folders that aren't relevant to the query.
    - Result: This reduced our query costs by over 90% and improved speed significantly.

1. How did you handle the lifecycle of your data? Did you manually delete old files?
    - The Answer: No, manual deletion is risky and doesn't scale. We configured S3 Lifecycle Policies.
    - Simple Explanation: It’s an automated rule we set on the bucket:
        - Day 0-30: Keep in Standard (for immediate analysis).
        - Day 30-90: Move to Standard-IA (Infrequent Access) – cheaper storage, slightly higher access cost.
        - Day 90+: Move to Glacier Deep Archive (for long-term compliance).
        - Day 365: Expire (delete) the data if regulations allow.
    - Why: This saved us roughly 40-60% on storage bills automatically.

1. Have you used S3 Event Notifications? Give a real-world scenario.
    - The Answer: Yes, we used them for Event-Driven Architectures.
    - Scenario: We receive files from a third-party vendor at random times. We can't schedule a job because we don't know when the file will arrive.
    - The Setup: We configured an S3 Event Notification (specifically `s3:ObjectCreated:Put`).
    - The Flow: As soon as a file lands in the landing bucket, S3 sends a message to AWS Lambda (or SQS), then Lambda triggers the Glue Job.
    - Benefit: This reduced latency. Data is processed seconds after arrival, rather than waiting for a nightly batch job.

1. We have a high-throughput application doing thousands of writes per second. Did you face S3 Throttling (503 Slow Down)? How did you handle it?
    - The Answer: Yes, S3 has a request rate limit per prefix (3,500 PUTs/copy/post/delete and 5,500 GETs per second).
    - The Bottleneck: If all our data goes into s3://bucket/data/, that single folder (prefix) hits the limit.
    - The Solution: We increased parallelization by randomizing prefixes (in older designs) or relying on S3's improved scaling, but primarily we ensured our partition keys had high cardinality.
    - Modern Approach: For massive uploads, we use S3 Multipart Upload. It breaks a large file into chunks and uploads them in parallel. If one chunk fails, we only retry that chunk, not the whole file. This improves throughput and reliability.

1. What is S3 Strong Consistency, and why was it a big deal for Data Engineering when it was announced?
    - The Answer: Before late 2020, S3 was 'Eventually Consistent'.
    - The Old Problem: If a Spark job wrote a file (file_A.csv) and immediately tried to list the files to verify it, S3 might say 'File not found' for a few seconds. This caused flaky ETL pipelines where jobs failed randomly.
    - The Update: S3 now delivers Strong Consistency automatically.
    - Impact: This simplified our architecture. We removed all the complex 'wait logic' or secondary databases (like DynamoDB) that we used to use just to keep track of what files were actually written. It made Spark/Hadoop jobs directly on S3 much more stable.

1. Tell me about S3 Select. When would you use it over downloading the whole file?
    - The Answer: S3 Select allows us to use simple SQL expressions to filter the contents of a file within S3 itself before retrieving it.
    - Scenario: We have a 10GB CSV file of 'Global Sales', but the application only needs rows where Country='USA'.
    - Standard Way: Download 10GB to the EC2 instance -> Filter for USA -> Result is 200MB. Wasted bandwidth and CPU.
    - S3 Select Way: Send a SQL query (SELECT * FROM S3Object WHERE Country='USA') -> S3 scans the file -> Returns only the 200MB.
    - Benefit: Drastically reduces network traffic and speeds up applications that only need a slice of large datasets.

1. We accidentally overwrote a critical configuration file in our S3 bucket yesterday. Is there any way to get the previous version back?
    - The Answer: Yes, if S3 Versioning was enabled on the bucket.
    - Simple Explanation: Versioning can act like a 'Ctrl+Z' for your bucket. When you upload a file with the same name (e.g., config.json), S3 doesn't actually delete the old one. It keeps the old one hidden and puts the new one on top.
    - How to Recover: We can list the 'versions' of the file and download the one from yesterday.
    - Caveat: If Versioning wasn't enabled before the overwrite, the data is permanently lost. This is why we enable versioning on all **production** buckets by default.

1. Can you host a website directly on S3? What are the limitations?
    - The Answer: Yes, S3 has a feature called Static Website Hosting.
    - What it does: It turns an S3 bucket into a simple web server that serves HTML, CSS, and JavaScript files.
    - The Limitation: It is static only. It cannot run server-side code like PHP, Python, or Java. It can't connect to a database directly.
    - Real World Use: We use it to host the front-end (React/Angular) of our dashboard, while the backend API runs on Lambda or EC2.

1. We have customers in Europe complaining that uploading large video files to our US-East bucket is too slow. How can we fix this without moving the bucket?
    - The Answer: We can enable S3 Transfer Acceleration.
    - Simple Explanation: Instead of the data traveling across the slow, public internet all the way to the US, the user uploads to the nearest AWS 'Edge Location' (like a local post office). From there, AWS moves the data over its own optimized, high-speed fiber network directly to the bucket.
    - The Trade-off: It costs extra, but it can be 50-500% faster for long-distance uploads.

1. We need a Disaster Recovery (DR) plan. If the entire 'us-east-1' region goes down, we need our data available in 'eu-west-1'. How do we automate this?
    - The Answer: We would configure CRR (Cross-Region Replication).
    - How it works: We set up a rule on the source bucket. Any new object uploaded to the US bucket is automatically and asynchronously copied to the Europe bucket.
    - Critical Detail:
        - Both buckets must have Versioning enabled.
        - It only replicates new data by default. For existing data, we would need to run an S3 Batch Replication job to sync the history.
    - We can also change the storage class on the destination (e.g., replicate to Glacier in Europe to save money).

1. What is S3 Intelligent-Tiering, and why would you use it over standard Lifecycle Policies?
    - The Answer: Intelligent-Tiering is for data with unpredictable access patterns.
    - The Problem: Standard Lifecycle rules work by age (e.g., 'Move to cold storage after 30 days'). But what if our users suddenly need to access that 'old' data again? In standard classes, we pay a retrieval fee.
    - The Solution: Intelligent-Tiering monitors access. If we haven't touched a file for 30 days, it moves it to a cheaper tier. If we suddenly access it, it moves it back to the hot tier automatically and without retrieval fees.
    - Ideal Use Case: Data Science lakes where we don't know which datasets the analysts will need next month.

1. We are building a financial application. The auditors require 'WORM' (Write Once, Read Many) compliance. No one, not even the root user, should be able to delete these logs for 5 years. How do we achieve this?
    - The Answer: We must use S3 Object Lock in 'Compliance Mode'.
    - Governance Mode: Allows users with special permissions to delete files (good for testing).
    - Compliance Mode: This is the 'nuclear option.' Once a file is locked for 5 years in this mode, nobody, not even the AWS account owner or root user, can delete or overwrite it until the timer expires.
    - Real World Impact: This is critical for SEC/FINRA regulations. We usually put these objects in a separate bucket with MFA Delete enabled as an extra precaution.

1. Our Data Lake has grown to 100 different teams accessing one bucket. The Bucket Policy has hit the 20KB size limit, and managing permissions is a nightmare. How do we fix this?
    - The Answer: We should migrate to S3 Access Points.
    - The Problem: A single Bucket Policy is a 'monolith.' Cramming rules for Finance, HR, and Sales into one JSON file is unmanageable.
    - The Solution: Access Points allow us to create multiple 'entry doors' to the same bucket.
        - Door 1 (Finance Access Point): Only allows read/write to the /finance folder.
        - Door 2 (Sales Access Point): Only allows read access to /sales.
    - Benefit: Each team gets their own specific policy. We can scale access without hitting bucket policy size limits.

1. How does S3 ensure data integrity? How do we know the file didn't get corrupted during the network transfer?
    - The Answer: S3 uses Checksums (MD5/CRC).
    - The Mechanism: When we upload a file, we can calculate its checksum (a digital fingerprint) on our local machine and send it along with the PUT request.
    - Verification: S3 calculates the checksum on its end as it receives the data. If the two fingerprints don't match, S3 rejects the upload instantly, ensuring that we never store corrupted data.
    - New Feature: S3 now supports additional algorithms like CRC32 and SHA-1, which are faster to calculate than MD5 for large files.

## Error-Based Questions
1. You are trying to download a file from S3 using the AWS CLI. You get 403 Access Denied. You checked your IAM User, and it has `AdministratorAccess`. How is this possible?
    - The Answer: In S3, an 'Allow' in IAM is not enough. Access is evaluated based on the union of Three Layers. I would check them in this order:
        1. Bucket Policy: Does the bucket itself explicitly Deny my user or my IP address? (Explicit Deny always wins).
        1. Public Access Block: Is 'Block Public Access' enabled on the bucket? If I am accessing it via the public internet without signing (e.g., browser), this will block me.
        1. KMS Key Policy: This is the most common hidden trap. If the object is encrypted with a custom KMS key, my IAM user needs kms:Decrypt permission on that specific key, not just S3 permissions.

1. Your application is uploading thousands of PDF documents to S3. Suddenly, you start getting 503 Slow Down errors. You are nowhere near the total bucket storage limit. What is happening?
    - The Answer: You are hitting the Request Rate Limit per Prefix.
    - The Limit: S3 supports 3,500 PUTs/copy/post/delete and 5,500 GETs per second per partitioned prefix.
    - The Cause: If you file names like `2024-01-01-file1` or `2024-01-01-file2`, all traffic hits the same '2024-01-01' partition.
    - The Fix: Add Entropy: Add a random hash to the start of the key: `a1b2-2024-01-01....`. This spreads the load across different physical partitions in S3. 
    - Retry Strategy: Implement 'Exponential Backoff' in your SDK to handle the 503s gracefully.

1. To save money, you set up a Lifecycle Rule to move log files to S3 Glacier Deep Archive after 1 day. A month later, your bill is HIGHER, not lower. Why?
    - The Answer: This is the Transition Cost and Minimum Size trap.
    - Trap 1 (Size): Glacier has a minimum object size (e.g., 128KB). If your logs are tiny (5KB), S3 charges you for 128KB of storage for every file. You are paying for 'air'.
    - Trap 2 (Requests): AWS charges a fee for every request to move a file to Glacier. If you move millions of tiny files, the request fees ($0.05 per 1,000) outweigh the storage savings.
    - The Fix: Aggregate small files into larger bundles (e.g., 100MB tarballs) before transitioning them to Glacier.

1. Account A uploads a file to Account B's bucket. The upload succeeds. However, when Account B tries to read the file in their own bucket, they get Access Denied. Why?
    - The Answer: This is an Object Ownership or KMS issue.
    - Case 1 (Legacy ACLs): If Account A uploaded the file without granting bucket-owner-full-control, Account A still owns the object. Account B hosts it but cannot read it.
        - Fix: Enable S3 Object Ownership: Bucket Owner Enforced on the bucket to disable ACLs and auto-claim ownership.
    - Case 2 (KMS): If Account A encrypted the file with Account A's KMS Key, Account B cannot decrypt it.
        - Fix: Account A must use Account B's Public Key (or a shared Multi-Region Key) to encrypt the file during upload.

1. You enabled Cross-Region Replication (CRR) to copy data from us-east-1 to eu-west-1. New files are replicating fine, but the 50TB of existing data isn't moving.
    - The Answer: CRR is Event-Driven, not retroactive.
    - The Explanation: Enabling CRR only sets up a listener for new upload events. It does not automatically scan and copy old files.
    - The Fix: You must create an S3 Batch Replication Job. This is a specific operation where you tell S3, 'Go scan the bucket inventory and replicate all the files that existed before I turned on the rule.'

1. We need to prove to auditors that the file in S3 is bit-for-bit identical to the source file on our server. The ETag in S3 is not matching our local MD5 checksum. Why?
    - The Answer: The S3 ETag is not always an MD5 hash.
    - The Nuance: If the file was uploaded using Multipart Upload, the ETag is a composite hash (e.g., hash-part1 + hash-part2...) followed by -N (number of parts). It will never match a simple local MD5.
    - Potential Fixes:
        - Use Additional Checksums: When uploading, enable CRC32 or SHA256 checksums in the S3 API. S3 stores this as a separate metadata field which will match your local calculation.
        - Calculate the composite ETag locally by simulating the multipart chunking logic.

1. You have a bucket `uploads/` where users drop images. You set up TWO event notifications: Prefix `images/` triggers Lambda A (Resize). Prefix `images/` and Suffix `.jpg` triggers Lambda B (Metadata).  You upload a `test.jpg` to `images/`. AWS throws an error immediately and saves nothing. Why?
    - The Answer: You violated the Overlapping Prefixes Rule.
    - The Error: S3 does not allow two configurations to overlap for the same event type because it cannot guarantee which one fires (or if both fire).
    - The Logic: Since 'images/' includes '.jpg' files, these two rules conflict.
    - The Fix: You must route to a single destination (like an SNS Topic or EventBridge) first. Then, let SNS/EventBridge filter the messages and fan them out to Lambda A and Lambda B independently.

1. You are cleaning up a 'Test' bucket. You try to delete a file `contract.pdf`, but S3 gives Access Denied. You log in as the Root User and try again. It still says Access Denied. How is this possible?
    - The Answer: The object is likely under Object Lock in Compliance Mode.
    - Governance Mode: Prevents deletion, but a user with special permissions (like Root) can bypass it.
    - Compliance Mode: This is the 'Nuclear Option'. Nobody, not even the Root User or AWS Support, can delete that object until the retention period expires (e.g., 7 years).
    - The Only Fix: You cannot delete the file. If you absolutely must remove it (e.g., it was uploaded to the wrong bucket by mistake), your only option is to **delete the entire AWS Account** (if it's a test account), though typically you just have to wait.

1. Your Spark job reads 100,000 files from S3. S3 handles the throughput fine (no 503s), but the job crashes with KMS.ThrottlingException. Why is KMS involved in a simple read?
    - The Answer: Your bucket uses SSE-KMS (Server-Side Encryption with KMS) instead of SSE-S3 (Managed Keys).
    - The Bottleneck: When you use SSE-S3, AWS handles the decryption scale for free. When you use SSE-KMS, every single file read generates a separate API call to the KMS service to decrypt the key (`kms:Decrypt`).
    - The Limit: KMS has a strict request-per-second limit (e.g., 5,500 - 30,000 RPS depending on region). 100,000 Spark tasks reading simultaneously will instantly crush this limit.
    - The Fix: Enable S3 Bucket Keys. This allows S3 to request a 'short-lived key' from KMS once and reuse it for thousands of file operations, reducing KMS traffic by 99%.

1. You used S3 Batch Operations to copy 1 million objects to a backup bucket. The job status says 'Failed'. How do you find out which specific files failed so you don't have to re-copy the successful ones?
    - The Answer: You need to analyze the Completion Report.
    - The Setup: When creating a Batch Job, you must enable the 'Completion Report' option and point it to a bucket.
    - The Debug: This report is a CSV file listing every object key and its status (Succeeded or Failed).
    - The Fix:
        1. Download the CSV.
        1. Filter for rows where Status = Failed.
        1. Create a new Batch Job using that filtered CSV as the input manifest to retry only the failures.