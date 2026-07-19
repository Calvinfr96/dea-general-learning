# AWS Secrets Manager Interview Questions

## Basic Questions
1. What is AWS Secrets Manager?
    - Answer: AWS Secrets Manager is a service that helps you securely store, manage, and rotate secrets such as database credentials, API keys, and other sensitive information.

1. How does AWS Secrets Manager differ from AWS Systems Manager Parameter Store?
    - Answer: Secrets Manager is designed for storing sensitive data and provides secret rotation capabilities. Parameter Store is a more general configuration store, and while it can store sensitive data, it does not have automatic rotation for secrets.

1. What types of secrets can AWS Secrets Manager store?
    - Answer: Secrets Manager can store various types of secrets such as database credentials, API keys, OAuth tokens, SSH keys, and any other sensitive information that needs secure storage.

1. What is secret rotation in AWS Secrets Manager?
    - Answer: Secret rotation is a feature in Secrets Manager that allows secrets (like database credentials) to be automatically rotated on a regular schedule, ensuring that secrets remain secure and up-to-date without manual intervention.

1. What is the default rotation period for secrets in AWS Secrets Manager?
    - Answer: The default rotation period for secrets is 30 days, but this can be customized based on the requirements.

1. How does AWS Secrets Manager ensure that secrets are securely stored?
    - Answer: Secrets Manager encrypts all secrets at rest using AWS Key Management Service (KMS) keys. It uses secure protocols, like HTTPS, for in-transit encryption, ensuring both rest and transit security.

1. How does a data engineer retrieve a secret stored in AWS Secrets Manager?
    - Answer: Secrets can be retrieved via AWS SDKs, AWS CLI, or the AWS Management Console. When retrieved via the SDKs or CLI, Secrets Manager automatically decrypts the secret using the associated KMS key.

1. What is a secret version in AWS Secrets Manager?
    - Answer: Each secret in Secrets Manager can have multiple versions. A version corresponds to a specific set of values stored under the secret. When rotating a secret, Secrets Manager creates a new version.

1. Can you manually rotate a secret in AWS Secrets Manager?
    - Answer: Yes, secrets can be rotated manually by invoking the RotateSecret API or through the AWS Management Console.

1. How do you configure AWS Secrets Manager to rotate a database secret automatically?
    - Answer: You configure rotation by enabling the automatic rotation feature in Secrets Manager, specifying a Lambda function to update the database credentials, and setting the desired rotation schedule.

1. How do you control access to AWS Secrets Manager?
    - Answer: Access to Secrets Manager is controlled using AWS IAM policies. You can grant or deny permissions to specific users, roles, or services to manage or retrieve secrets.

1. What is the purpose of resource-based policies in AWS Secrets Manager?
    - Answer: Resource-based policies allow you to control who can access a specific secret. These policies can be used to grant access across AWS accounts or to other AWS services.

1. How does AWS KMS integrate with AWS Secrets Manager?
    - Answer: AWS Secrets Manager uses AWS KMS to encrypt and decrypt secrets. Each secret is encrypted using a customer-managed KMS key, and access to the secret is contingent on having access to the associated KMS key.

1. How do you ensure that secrets are encrypted in transit?
    - Answer: Secrets Manager encrypts secrets in transit using Transport Layer Security (TLS) to ensure that data remains secure while being transmitted between the Secrets Manager service and applications.

1. How do you audit access to secrets in AWS Secrets Manager?
    - Answer: Access to secrets is logged using AWS CloudTrail, which records API calls made to Secrets Manager. You can review the logs to track who accessed, updated, or rotated a secret.

1. How do you prevent unauthorized access to AWS Secrets Manager secrets?
    - Answer: Unauthorized access can be prevented by enforcing fine-grained access control using IAM policies, resource-based policies, and KMS key policies. You can also enable multi-factor authentication (MFA) for more secure access.

1. How do you rotate the encryption keys used by AWS Secrets Manager?
    - Answer: KMS keys can be rotated either manually or automatically (if automatic rotation is enabled for the key). When the KMS key used by Secrets Manager is rotated, all future secret encryptions will use the new key.

1. Can you restrict cross-account access to secrets in AWS Secrets Manager?
    - Answer: Yes, cross-account access can be restricted or granted using resource-based policies attached to the secret. These policies define the actions other AWS accounts or principals can perform on the secret.

1. How do you ensure that only specific applications can access secrets?
    - Answer: You can restrict access to secrets by attaching IAM roles to applications (like Lambda functions or EC2 instances) that have permissions to retrieve the secret. This ensures that only authorized applications can access the secret.

1. How does AWS Secrets Manager protect against accidental deletion of secrets?
    - Answer: Secrets Manager allows you to enable recovery windows for secrets, which means that when a secret is deleted, it enters a recovery state for up to 30 days, during which it can be restored.

1. How can you trace who accessed or modified a secret in AWS Secrets Manager?
    - Answer: You can trace access and modifications to secrets using AWS CloudTrail, which logs all API calls made to Secrets Manager, including details on who made the request, the action performed, and when it occurred.

1. How do you detect failed secret rotations in AWS Secrets Manager?
    - Answer: Failed secret rotations are logged in CloudWatch Logs and AWS CloudTrail. You can set up alarms or notifications in CloudWatch to alert you of rotation failures.

1. What is a recovery window in AWS Secrets Manager?
    - Answer: A recovery window is the grace period after deleting a secret. During this period, the secret can be restored before it's permanently deleted. The default recovery window is 30 days, but it can be configured.

1. How can AWS Secrets Manager help you comply with security and governance regulations?
    - Answer: Secrets Manager helps with compliance by securely storing and rotating sensitive information, providing detailed audit logs (via CloudTrail), and ensuring that secrets are encrypted using KMS.

## Scenario-Based Questions
1. You are writing a Python script in AWS Glue to connect to a MySQL database. Why didn't you just store the password in a variable or a config file in S3?
    - The Answer: Storing passwords in code or config files is a major security risk (Hardcoding).
    - The Risk: If I commit the code to Git, everyone sees the password. If I store it in S3, anyone with read access to that bucket can steal the credentials.
    - The Solution: I used AWS Secrets Manager.
    - How it works: I store the database username and password in Secrets Manager once. My Glue script uses the `boto3` library to call the API `get_secret_value()`. It retrieves the password programmatically at runtime.
    - Benefit: The password never appears in the code, logs, or version control.

1. What is the difference between AWS Secrets Manager and AWS Systems Manager (SSM) Parameter Store? They both seem to store strings.
    - The Answer: They are similar, but Secrets Manager is specialized for **Database Credentials**.
    - Parameter Store: Great for storing **non-sensitive** configuration (like `MaxThreadCount=50` or `Environment=Prod`). It is cheaper (free for standard parameters) but **lacks advanced rotation features**.
    - Secrets Manager: Designed for **passwords/keys**. It supports **Automatic Rotation** (changing the password automatically every 30 days) and built-in integration with RDS. It costs more ($0.40/secret/month) but offers higher security compliance.

1. How does your application authenticate with Secrets Manager to get the password? Do you need a password to get the password?
    - The Answer: No, that would be a chicken-and-egg problem. We use IAM Roles.
    - The Mechanism: The EC2 instance or Lambda function has an IAM Role attached to it.
    - The Policy: That IAM Role has a policy allowing the action `secretsmanager:GetSecretValue` on the specific ARN of the secret.
    - The Flow: When the code runs, AWS recognizes the IAM Role and allows the retrieval. No hardcoded credentials are needed to 'login' to Secrets Manager.

1. We noticed a spike in our AWS bill for Secrets Manager. The application is calling the API every time it processes a record. How do you fix this?
    - The Answer: The application is making too many `GetSecretValue` API calls.
    - The Cost: Secrets Manager charges per 10,000 API calls. If we process 1 million records and call the API for each one, it gets expensive and slow (latency).
    - The Solution: Implement Client-Side Caching.
    - How: Instead of calling AWS every time, we call it once when the application starts, store the password in a local variable (memory), and reuse it.
    - Library: AWS provides a python library `aws-secretsmanager-caching` that handles this automatically, including refreshing the secret from the cache if it changes.

1. Explain how 'Automatic Rotation' works for an RDS database. If Secrets Manager changes the database password, won't your application crash because it has the old password?
    - The Answer: Automatic Rotation uses a Lambda Function to coordinate the change safely.
    - The Process:
        1. Create: Secrets Manager creates a new version of the password.
        1. Update DB: It triggers a Lambda that logs into the RDS database and runs `ALTER USER ... IDENTIFIED BY 'new_password'`.
        1. Test: The Lambda tests the new password to ensure it works.
        1. Flip: Secrets Manager moves the label `AWSCURRENT` to the new password.
    - The App: Since our application uses Caching, there might be a brief moment where it has the old password. The caching library detects the login failure, automatically forces a refresh to get the new password, and retries. This ensures zero downtime.

1. Your Glue job runs in a private subnet without internet access. It is failing to retrieve the secret. Why? And how do you fix it without a NAT Gateway?
    - The Answer: It fails because the Secrets Manager API is a public endpoint on the internet.
    - The Fix: Use a VPC Interface Endpoint (PrivateLink).
    - How it works: We create an Interface Endpoint for Secrets Manager inside our VPC. This places a virtual network card (ENI) in our subnet.
    - The Result: The Glue job connects securely to Secrets Manager via the private AWS network backbone, without needing the public internet or a NAT Gateway.

1. We have a Central Security Account where all secrets are stored. Our ETL jobs run in a separate 'Data Account'. How do you allow the ETL job to read the secret from the Security Account?
    - The Answer: We need to configure permissions on both sides (The Identity and the Resource).
    - In the Security Account (Resource): We must add a Resource-Based Policy to the Secret itself. It must explicitly say: 'Allow Principal: arn:aws:iam::DataAccountID:role/ETLJobRole to retrieve me'.
    - In the Data Account (Identity): The IAM Role of the ETL job must have a policy allowing `secretsmanager:GetSecretValue` on the full ARN of the secret in the Security Account.
    - KMS Encryption: Since secrets are encrypted, the ETL Role also needs `kms:Decrypt` permission on the KMS Key used to encrypt that secret.

1. You need to rotate the API Key for a third-party service (like Salesforce or Stripe). Secrets Manager doesn't support this out of the box. How do you automate it?
    - The Answer: We write a Custom Lambda Rotator.
    - The Logic: Secrets Manager allows us to provide our own Lambda function for rotation.
    - The Steps:
        1. Create: Generate a new API Key (if possible) or Token.
        1. Set: Call the 3rd Party API to update the key on their side.
        1. Test: Make a dummy call to the 3rd Party API with the new key.
        1. Finish: Update the secret in Secrets Manager.
    - Complexity: We must handle 'Two-User' rotation strategies (Active/Passive keys) carefully to ensure that while the key is being swapped, ongoing transactions don't fail.

1. What is your Disaster Recovery (DR) strategy for secrets? If the 'us-east-1' region goes down, how does your application in 'us-west-2' access the database credentials?
    - The Answer: We use Secrets Manager Cross-Region Replication.
    - Configuration: When creating the secret, we select 'Replicate to us-west-2'.
    - The Sync: AWS automatically keeps the secret in sync. If a rotation happens in East, the new password is encrypted and sent to West immediately.
    - The Failover: Our application code checks the region. If it fails to connect to East, it attempts to retrieve the secret from the West region endpoint. We usually use a 'Global' secret name or dynamic ARN construction to handle this switch.

1. I accidentally deleted a production secret in the console! Is the data gone forever? How do I get it back?
    - The Answer: No, it is not gone immediately. Secrets Manager has a Soft Delete mechanism.
    - The Default: When you hit 'Delete', AWS schedules the secret for deletion in a minimum of 7 days (configurable up to 30 days).
    - The Recovery: During this window, the secret is still there but marked as 'Pending Deletion'. We can restore it instantly using the RestoreSecret API call or the Console.
    - Immediate Deletion: If you really need to delete it now (e.g., you accidentally uploaded a real password to a public demo), you must use the CLI with --force-delete-without-recovery, but this is dangerous.

1. We need to store a private SSL Certificate file (.pem) for our Kafka connection. Secrets Manager only shows key-value pairs. Can it handle files?
    - The Answer: Yes, Secrets Manager supports Binary Secrets.
    - Two Types: It stores either 'Secret String' (JSON/Text) or 'Secret Binary'.
    - Implementation: We upload the .pem file as binary data.
    - Retrieval: In Python (boto3), we access the SecretBinary field instead of SecretString. The SDK automatically decodes it from Base64 into the raw bytes needed for the SSL handshake.

1. We use Terraform (or CloudFormation) to build our infrastructure. How do you create a Database Password in Terraform without writing the actual password in the code?
    - The Answer: We use the Random Provider (or dynamic generation).
    - The Anti-Pattern: Never write `password = Hunter2` in the .tf file.
    - The Solution:
        1. Use Terraform to generate a random string (e.g., 16 chars, special characters).
        1. Create the AWS Secret resource using that random string.
        1. Create the RDS Instance referencing that same random string.
    - The Result: The password is created, stored, and assigned to the DB without a human ever seeing it or typing it into a file. The state file should be encrypted/securely stored.

1. You are running a Spark job on an EMR cluster. You need to access a secret. Do you attach the IAM policy to the Master Node or the Worker Nodes?
    - The Answer: You should attach it to the Instance Profile (Role) used by the **Worker Nodes** (Core/Task nodes).
    - Reason: The Spark driver/executors run on the worker nodes. They are the ones executing the code that calls `get_secret_value`.
    - Refinement: If the job is running in 'Client Mode' (driver on the master node), then the **Master Node** needs the permission.
    - Best Practice: Use EMR Roles for Runtime (IAM Roles for Service Accounts) if possible, so different Spark jobs on the same cluster can access different secrets, rather than giving the whole cluster access to everything.

1. An auditor is asking for proof of exactly WHO accessed the production database password in the last 90 days. How do you provide this report?
    - The Answer: We use AWS CloudTrail.
    - The Mechanism: Every time a user or service calls `GetSecretValue`, it is logged as an API event in CloudTrail.
    - The Analysis: I would query the CloudTrail logs (using Athena) filtering for:
        ```
        EventName = 'GetSecretValue'
        ResourceName = 'prod/db/password'
        ```
    - The Output: This gives a list of every IAM User, Role, and IP address that retrieved the secret, fulfilling the audit requirement.

1. Explain the encryption hierarchy. If you rotate the KMS Key used to encrypt the secret, do you break the application?
    - The Answer: No, the application will not break, thanks to Envelope Encryption.
    - How it works: Secrets Manager uses a Data Key to encrypt the actual password. That Data Key is then encrypted by your KMS Master Key (CMK).
    - Rotation:
        - If you rotate the Secret: Secrets Manager generates a new Data Key and re-encrypts the new data.
        - If you rotate the KMS Master Key: AWS handles the re-encryption of the Data Keys transparently. The API call `GetSecretValue` implicitly calls `kms:Decrypt`. As long as the IAM Role has permission to use the new version of the KMS key (via Alias or Key Policy), the application continues working without changes.

## Error-Based Questions
1. You wrote a Python Lambda to fetch a database password from Secrets Manager. You gave the Lambda execution role to the policy `secretsmanager:GetSecretValue` on the secret ARN. However, it still fails with Access Denied. The secret is encrypted with the default KMS key.
    - The Answer: You forgot the KMS Decrypt Permission.
    - The Logic: Secrets Manager encrypts the secret using a KMS Key (either the default aws/secretsmanager key or a custom Customer Managed Key).
    - The Trap: Permission to retrieve the secret (`GetSecretValue`) is not enough. You also need permission to decrypt the payload (`kms:Decrypt`).
    - The Fix: Add `kms:Decrypt` to the Lambda's IAM role for the specific Key ARN used to encrypt that secret.

1. Your application has 500 microservices starting up at the same time (e.g., after a deployment). Suddenly, many services crash with `ThrottlingException` when calling Secrets Manager. Why?
    - The Answer: You are hitting the API Request Limit.
    - The Limit: Secrets Manager has a hard limit on API calls (e.g., 5,000 requests per second).
    - The Cause: If 500 containers start and each one makes 10 calls to fetch secrets immediately, you spike above the limit.
    - The Fix:
        1. Cache the Secret: Use the AWS Secrets Manager Caching Library (available for Java, Python, etc.). It stores the secret in local memory and only refreshes it occasionally.
        1. Jitter: Add random delays (jitter) to the startup time of your containers so they don't all hit the API at the exact same millisecond.

1. You moved all your configuration (API Keys, Config strings) into Secrets Manager. You have 10,000 distinct config values. Your bill is now huge. Why?
    - The Answer: Secrets Manager is priced per Secret per Month (~$0.40).
    - The Math: 10,000 secrets * $0.40 = $4,000/month just for storage.
    - The Mistake: Using Secrets Manager for non-sensitive configuration (like 'Feature Flags' or 'UI Colors').
    - The Fix:
        1. Move non-sensitive config to AWS Systems Manager (SSM) Parameter Store (Standard parameters are free).
        1. Combine secrets: Instead of 5 secrets for DB host, user, pass, port, and dbname, store them as one JSON object in a single secret.

1. Account A owns the Secret (and the KMS Key). Account B wants to read it. You updated Account A's Secret Resource Policy to allow Account B. You updated Account B's IAM Role to allow `GetSecretValue`. It still fails. What is the third lock?
    - The Answer: The KMS Key Policy.
    - The Trap: The secret is encrypted with a KMS Key in Account A.
    - The Fix: You must update the KMS Key Policy in Account A to explicitly allow the IAM Role (or Root User) of Account B to perform `kms:Decrypt`.
    - Summary: Cross-account secrets always require 3 unlocks:
        - Secret Resource Policy.
        - Identity IAM Policy.
        - KMS Key Policy.

1. Your primary region us-east-1 goes down. You failover to us-west-2. Your application starts up in West, but it crashes because the Secret is missing. You assumed Secrets Manager is global. Is it?
    - The Answer: No, Secrets Manager is Regional.
    - The Logic: A secret created in East does not exist in West by default.
    - The Fix: You must enable Secret Replication. This automatically replicates the secret (and its updates/rotations) to the secondary region.
    - Crucial Detail: In the West region, **the secret will be encrypted with a different KMS key** (because KMS is also regional). Ensure the West app has permissions for the West KMS key.

1. You wrote a Custom Lambda Rotation function for a 3rd party API key. The Lambda runs, rotates the key, and then crashes. Secrets Manager retries immediately. The API provider blocks you for 'Too many key changes'. How do you debug this 'Half-Rotated' state?
    - The Answer: Rotation has 4 steps: createSecret, setSecret, testSecret, finishSecret.
    - The Failure: If your Lambda crashes at testSecret, the new password exists in the Pending stage but is not promoted to Current.
    - The Retry: When Secrets Manager retries, **your Lambda code must be Idempotent**. It should check: 'Is there already a pending secret? Yes? Then verify THAT one instead of creating a brand new one.'
    - The Fix: Ensure your custom rotation logic checks the current state (describeSecret) before aggressively calling the 3rd party API to generate a new key.

1. You updated a secret manually via the CLI using `put-secret-value`. You verified the new value in the console. However, your application is still receiving the OLD password. You restarted the app (cleared cache), but it still gets the old password. Why?
    - The Answer: You likely didn't move the `AWSCURRENT` Staging Label.
    - The Logic: Secrets Manager uses labels to track versions. `GetSecretValue` returns the version labeled `AWSCURRENT` by default.
    - The Trap: If you use the CLI `put-secret-value` without specifying `--version-stages AWSCURRENT`, AWS might create a new version but leave the `AWSCURRENT` label on the old version.
    - The Fix: You must move the `AWSCURRENT` label to the new version ID.

1. You created a secret using Terraform and set the initial password to ChangeMe123. You enabled Automatic Rotation. AWS rotated the password to XyZ999. Next week, you ran terraform apply to update a tag. Suddenly, the database password reverted to ChangeMe123, breaking the app. Why?
    - The Answer: This is a State Drift.
    - The Cause: Terraform's state file thinks the password should be ChangeMe123. When you ran apply, it saw the 'drift' (the value changed by AWS Rotation) and 'fixed' it by resetting it to the hardcoded value.
    - The Fix: In Terraform (or CloudFormation), you must use a Lifecycle Ignore Rule. `lifecycle { ignore_changes = [ secret_string ] }`. This tells IaC: 'Create this secret initially, but ignore any future changes to the value since an external process (Rotation) manages it.'

1. You have a global app. Primary Region is US-East. Replica Region is EU-West. US-East goes down. You point your EU-West application to the Replica Secret. The app works for reading, but when the app tries to rotate or update the secret in EU-West, it fails with an error. Why?
    - The Answer: Replica Secrets are Read-Only by default.
    - The Architecture: Secrets Manager allows you to read a replica in a secondary region, but the 'Source of Truth' remains in the Primary region. You cannot modify a replica.
    - The Fix: To failover fully, you must Promote the replica secret to a 'Standalone Secret'.
        - API: StopReplicationToReplica (converts replica to standalone).
        - Once promoted, it becomes writable, and you can enable rotation on it.