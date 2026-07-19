# AWS IAM Interview Questions

## Basic Questions
1. What is AWS IAM?
    - Answer: AWS Identity and Access Management (IAM) is a service that helps you securely control access to AWS services and resources. IAM allows you to create and manage users, groups, roles, and policies.

1. What are IAM users?
    - Answer: An IAM user is an identity with specific permissions to interact with AWS services. A user represents a person or an application that interacts with AWS.

1. What are IAM groups?
    - Answer: IAM groups are collections of IAM users. Permissions granted to a group are applied to all users within that group, making permission management easier.

1. What are IAM roles?
    - Answer: IAM roles are similar to users but are intended to be assumed by entities like AWS services or applications. Roles provide temporary security credentials for access without long-term credentials like passwords.

1. What are IAM policies?
    - Answer: IAM policies are JSON documents that define permissions for users, groups, or roles. Policies specify what actions are allowed or denied on AWS resources.

1. What are managed policies in IAM?
    - Answer: Managed policies are pre-configured and reusable policies that AWS or the user can manage. They can be attached to multiple users, groups, or roles.

1. What is the principle of least privilege in IAM?
    - Answer: The principle of least privilege involves giving IAM entities (users, roles, etc.) only the permissions they need to perform their job and nothing more.

1. What is an inline policy in IAM?
    - Answer: An inline policy is a policy that is embedded directly in a single user, group, or role. Inline policies are not reusable and are tightly coupled with the IAM entity.

1. What are service-linked roles in AWS IAM?
    - Answer: Service-linked roles are predefined IAM roles directly associated with specific AWS services. They enable those services to perform actions on your behalf without you having to set up permissions manually.

1. What are resource-based policies in AWS IAM?
    - Answer: Resource-based policies are policies that are attached directly to AWS resources, like S3 buckets or Lambda functions, instead of users or roles. They define who can access the resource and under what conditions.

1. What is the difference between IAM roles and IAM users?
    - Answer: IAM users have long-term credentials, whereas IAM roles provide temporary security credentials. Users are tied to a specific identity, while roles can be assumed by any entity (like AWS services or other users).

1. How can you assume a role in IAM?
    - Answer: To assume a role, you use the `sts:AssumeRole` API, which returns temporary security credentials for the assumed role. This allows an IAM user or service to gain the permissions of that role temporarily.

1. What is the purpose of IAM access keys?
    - Answer: IAM access keys (consisting of an Access Key ID and Secret Access Key) are used by applications or users to sign programmatic requests to AWS services through the AWS CLI, SDKs, or APIs.

1. What is the IAM policy evaluation logic?
    - Answer: IAM policy evaluation follows these steps: first, explicit denies are evaluated; second, allow policies are checked; finally, if there’s no explicit deny and the request is allowed, access is granted. If no allow is found, access is denied.

1. What is a permission boundary in IAM?
    - Answer: A permission boundary is an advanced feature that defines the maximum permissions that an IAM user or role can have. It is often used to limit the scope of roles created by developers or teams.

1. What are IAM identity-based policies?
    - Answer: Identity-based policies are policies attached to IAM users, groups, or roles that define what actions they can perform on AWS resources.

1. What are IAM policy conditions?
    - Answer: IAM policy conditions are additional constraints that control when a policy statement is in effect. For example, you can add conditions to only allow access from a certain IP range or during a specific time period.
    - Practical Example: The Trust Policy of the `GitHubActionsCDKDeployRole` role (used in creating CI/CD pipelines) has conditions that limit which repositories GitHub Actions can modify.

1. What is a cross-account role, and how does it work in data pipelines?
    - Answer: A cross-account role allows IAM entities in one AWS account to assume a role in another account, enabling secure collaboration between AWS environments. This is useful for shared data pipelines across organizations.

1. What are IAM best practices for managing users and groups?
    - Answer: Some best practices include: following the principle of least privilege, regularly rotating access keys, using groups to manage permissions, enabling MFA, and auditing access logs.

## Scenario-Based Questions
1. In your project, did you create IAM Users for your Glue jobs or EC2 instances? If not, what did you use?
    - The Answer: No, creating IAM Users for machines is a bad practice because it requires managing long-term credentials (access keys) that can be leaked.
    - The Solution: We used IAM Roles.
    - Simple Explanation: An IAM User is like a permanent ID badge for a person. An IAM Role is like a 'hat' that a service (like an EC2 server or Glue job) puts on.
    - How it works: When I create a Glue job, I assign it a 'GlueServiceRole'. This role gives the job temporary permission to read S3 only while the job is running. No passwords are stored in the code.
1. What is the difference between an 'Identity-Based Policy' and a 'Resource-Based Policy'? When did you use which?
    - The Answer: It’s about where you attach the permission.
    - Identity-Based Policy: Attached to the User/Role. It says 'I allow this person to access these buckets'.
    - Use Case: I gave my developers a policy that allows them to read dev-bucket but denies prod-bucket.
    - Resource-Based Policy: Attached to the Resource itself (like an S3 Bucket Policy). It says 'I allow this bucket to be accessed by these people'.
    - Use Case: I added a Bucket Policy to our finance-data bucket that explicitly denies access to everyone except the 'Finance-Admin-Role', effectively locking it down at the source.
1. What is the Principle of Least Privilege, and how did you apply it?
    - The Answer: It means giving a user/role only the bare minimum permissions needed to do their job, and nothing more.
    - The Mistake: Attaching the `AdministratorAccess` or `S3FullAccess` policy to a Glue Job just to make it work.
    - The Correct Way: I created a custom policy that allowed `s3:GetObject` ONLY on `s3://my-source-bucket` and `s3:PutObject` ONLY on `s3://my-target-bucket`.
    - Why: If that Glue script gets hacked or has a bug, it cannot accidentally delete the entire data lake.
1. We have our raw data in Account A (Source), but our Glue jobs run in Account B (Analytics). How do you grant access across accounts?
    - The Answer: We cannot just attach a policy in Account B saying 'Allow access to Bucket A'. Account A must explicitly allow it too.
    - The Mechanism: We used Cross-Account Roles.
    - In Account A (Source): We create a Role (CrossAccountAccessRole) that has permission to read the S3 bucket. We edit the Trust Policy of this role to say 'Account B is allowed to assume me'.
    - In Account B (Analytics): We give our Glue Job permission to call sts:AssumeRole on that role in Account A.
    - The Flow: When the job runs, it temporarily 'becomes' the role in Account A to read the data.
1. What is the 'PassRole' permission? Why did your deployment pipeline fail with a 'AccessDenied' error even though you had Admin rights?
    - The Answer: This is a common security check in AWS.
    - The Scenario: I (the developer) have permission to create a Glue Job. I try to assign the AdminRole to that Glue Job.
    - The Risk: If AWS let me do that, I could write a Glue script that uses AdminRole to delete the whole account. Effectively, I would have escalated my own privileges to Admin.
    - The Fix: To assign a role to a service, my user must have the `iam:PassRole` permission for that specific role. It acts as a check: 'Are you allowed to give this powerful role to a machine?'
1. You have an IAM Policy that allows access to S3, but an S3 Bucket Policy that denies it. Who wins?
    - The Answer: **The Explicit Deny always wins**.
    - Evaluation Logic: AWS evaluates permissions in this order:
        1. Start with Implicit Deny (everything is blocked by default).
        1. Look for any Explicit Allow.
        1. Look for any Explicit Deny.
    - Result: If any policy (IAM, Bucket, Service Control Policy) has a Deny statement for that action, the request is rejected, regardless of how many Allow statements exist. This is useful for creating 'Guardrails' (e.g., 'Deny all deletion of logs', no matter what).
1. We have 1,000 developers. Creating individual IAM Users for them is unmanageable. How do you handle enterprise-scale access?
    - The Answer: We stop using IAM Users entirely and switch to Identity Federation (Single Sign-On).
    - The Architecture: We integrate AWS IAM Identity Center (formerly SSO) with the company's existing directory (like Active Directory, Okta, or Azure AD).
    - The Flow:
        1. Developer logs in to their corporate Okta portal.
        1. Okta handles the password/MFA check.
        1. Okta sends a SAML assertion (a secure token) to AWS.
        1. AWS maps that token to a specific IAM Role (e.g., DataEngineerRole) and logs them in.
    - Benefit: When an employee leaves the company, we disable them in Active Directory, and they instantly lose access to AWS. No need to hunt down stray IAM keys.
1. Explain Attribute (Tag)-Based Access Control (ABAC) vs. Role-Based Access Control (RBAC). Why would you move to ABAC for a Data Lake?
    - The Answer: RBAC is what we usually do: Create a role `ProjectA_Developer`, `ProjectB_Developer`, etc. This leads to 'Role Explosion' (hundreds of roles to manage for hundreds of different projects).
    - The Solution (ABAC): We create one single generic role (DeveloperRole), but we use Tags for logic.
    - The Policy: 'Allow this user to read S3 Bucket X only if `User.Department == Bucket.Tag.Department`'.
    - Real World: If I move from the 'Finance' team to the 'Sales' team, HR just updates my tag in the directory. I instantly lose access to Finance buckets and gain access to Sales buckets, without anyone editing IAM policies.
1. What are Permissions Boundaries? How do you let a Data Science team create their own IAM roles without giving them the power to create Admin roles?
    - The Answer: We use a Permissions Boundary.
    - The Problem: We want Data Scientists to be self-sufficient (create roles for their SageMaker jobs), but we don't want them creating a role that has Full Admin Access.
    - The Solution: We attach a Permissions Boundary (a limit policy) to their user. It says: 'You can create any role you want, BUT that new role must have this specific Boundary attached to it'.
    - The Effect: Even if they try to write a policy giving `AdministratorAccess`, the Boundary acts as a glass ceiling. The effective permission is the intersection of what they wrote and what the Boundary allows.
1. You need to grant a temporary consultant read-only access to a specific S3 bucket from 9 AM to 5 PM only. How do you enforce this time restriction?
    - The Answer: We use IAM Policy Conditions.
    - Simple Explanation: In the JSON policy, we add a Condition block.
    - Technical Detail: We use the `aws:CurrentTime` condition key:
        ```
        Condition: {
            DateGreaterThan: {aws:CurrentTime: 2024-01-01T09:00:00Z},
            DateLessThan: {aws:CurrentTime: 2024-01-01T17:00:00Z}
        }
        ```
    - Why: This ensures that even if they have the keys, they are useless outside of business hours.
1. What is the 'Confused Deputy' problem, and how did you prevent it when using cross-account roles?
    - The Answer: The Confused Deputy problem is a security risk where a malicious actor uses a legitimate service (like a confusing deputy) to access resources they shouldn't have.
    - The Scenario: Imagine I have a service that writes to my S3 bucket. A hacker might trick that service into writing to their bucket using my role.
    - The Fix: We use the `aws:SourceArn` or `aws:SourceAccount` condition in the Trust Policy.
    - Implementation: 'I trust the Glue Service (`glue.amazonaws.com`) to assume this role, BUT ONLY IF the request comes from My Account ID.' This prevents another AWS account from using the Glue service to assume my role.
1. You are the Data Architect. How do you prevent your team from accidentally spinning up expensive GPU instances (P3/P4) for simple ETL jobs?
    - The Answer: We use Service Control Policies (SCPs) at the AWS Organization level.
    - Simple Explanation: IAM Policies say what a User can do. SCPs say what the entire Account can do.
    - The Strategy: I apply an SCP to the 'Data Engineering' Organizational Unit (OU) that explicitly Denies `ec2:RunInstances` if the InstanceType is not in a sanctioned list (e.g., t3.medium, m5.large).
    - The Result: Even if a user has `AdministratorAccess` in that account, the SCP overrides it (because it **denies** access, it doesn't grant access). They physically cannot launch a GPU instance. It acts as a hard guardrail for cost control.
1. Your ETL job is failing with 'Access Denied' when trying to read from S3, but you checked the IAM Role and it has `s3:FullAccess`. What else could be blocking it?
    - The Answer: There are two other major layers to check besides the Identity Policy:
    - VPC Endpoint Policy: If the job runs in a private subnet, it uses a VPC Endpoint to reach S3. That Endpoint itself has a policy. If it says 'Allow only bucket A', and I try to access bucket B, it fails.
    - S3 Bucket Policy: The target bucket might have an explicit Deny for my role or IP range.
    - Permissions Boundary: My role might have a boundary attached that limits its maximum permissions.
1. What is AccessAnalyzer and when would you use it?
    - The Answer: IAM Access Analyzer is a tool we use to audit external access.
    - The Problem: It's hard to manually check 100 buckets to see if any are public or shared with external accounts.
    - The Solution: Access Analyzer continuously scans our resource-based policies (S3, KMS, IAM Roles).
    - The Alert: It alerts us: 'Hey, this S3 bucket allows access from Account 12345 (which is not in your Organization)'.
    - Use Case: We use it during security audits to ensure no data is inadvertently shared with vendors or the public.
1. How does AWS Lake Formation change the way you manage IAM permissions? Do you still need IAM Policies?
    - The Answer: Lake Formation introduces a hybrid permission model.
    - The Old Way (IAM Only): To give access to a specific column in a Glue Table, we had to create complex views or separate buckets. IAM is 'all or nothing' on the file level.
    - The New Way (Lake Formation):
    - IAM Layer: We give the user a 'coarse' IAM permission (e.g., `lakeformation:GetDataAccess`). They don't need direct S3 access anymore.
    - Lake Formation Layer: We define fine-grained rules: 'User A can see Table Sales, but exclude the 'SSN' column'.
    - Benefit: It moves access control from the 'File/Bucket' level (Infrastructure) to the 'Table/Column' level (Data), which is much more natural for data governance.
1. Explain the security implications of `sts:GetSessionToken` vs `sts:AssumeRole`.
    - The Answer: They serve different purposes for temporary credentials:
        1. `sts:AssumeRole`: Used when you want to change your identity (e.g., User A becomes Role B). You gain the role's permissions but lose your original user permissions.
        1. `sts:GetSessionToken`: Used when you want to keep your identity but add MFA protection.
    - Real World Scenario: If I have a policy that says 'Allow S3 Delete ONLY if MFA is present', I must call GetSessionToken with my MFA code. It returns temporary keys that look like me but have the 'MFA Authenticated' flag set, allowing me to perform the delete operation.

## Error-Based Questions
1. You wrote a Python script to read a file from `s3://my-data-bucket`. You are running it from an EC2 instance. The script fails immediately with 403 Access Denied. You checked the IAM Role attached to the EC2, and it has AmazonS3FullAccess. Why is it still failing?
    - The Answer: In AWS, an 'Allow' in your IAM Role is not the final word. Access is evaluated based on multiple layers. If the Identity (Role) has permission, the block is likely on the Resource (Bucket) side.
    - Bucket Policy: The S3 bucket might have a 'Bucket Policy' that explicitly denies access to your specific Role or IP address. **An Explicit Deny always wins over an Allow**.
    - KMS Encryption: This is a classic trap. If the file is encrypted with a generic AWS KMS key, your IAM Role also needs `kms:Decrypt` permission. `S3FullAccess` often does not include KMS keys by default.
    - VPC Endpoint: If you are accessing S3 from a private subnet, the Bucket Policy might enforce that traffic must come through a specific VPC Endpoint (`aws:sourceVpce`).
1. A developer on your team hardcoded their AWS Access Key and Secret Key into a Python script to run a nightly ETL job. Why is this a bad practice, and what should they use instead?
    - The Answer: Hardcoding long-term credentials (IAM Users) creates a massive security risk. If that code is pushed to Git, hackers can steal the keys.
    - The Fix: We should use IAM Roles.
    - How: If the script runs on EC2, attach an Instance Profile. If it runs locally, use AWS SSO (Identity Center) to generate temporary, short-lived credentials.
    - Why: Roles use temporary credentials that rotate automatically. If they are stolen, they expire in 1 hour.
1. You have a Glue Job in Account A. You need to write data to an S3 bucket in Account B. You added a Bucket Policy in Account B allowing Account A's Role. You added an IAM Policy in Account A allowing access to Bucket B. It still fails. What is missing?
    - The Answer: For cross-account S3 access, checking permissions is a two-step handshake, but often Object Ownership breaks it.
    - The Hidden Issue: If Account A writes a file to Account B's bucket, Account A still owns that file by default. Account B cannot read or delete it!
    - The Fix: 
        - ACLs: Ensure the writer sends the bucket-owner-full-control ACL during the upload.
        - Object Ownership: The modern fix is to enable 'S3 Object Ownership: Bucket Owner Enforced' on the destination bucket. This forces all new files to be owned by the bucket owner (Account B), regardless of who uploaded them.
1. Your policy allows `s3:ListBucket` on `arn:aws:s3:::my-data-bucket/*`. The developer says they get Access Denied when trying to list the files.
    - The Answer: This is a subtle syntax error.
    - The Error: `s3:ListBucket` is an action that happens on the Bucket itself, not the objects inside it.
    - The Fix:
        - `s3:ListBucket` must apply to `arn:aws:s3:::my-data-bucket` (No /*).
        - `s3:GetObject` must apply to `arn:aws:s3:::my-data-bucket/*` (With /*).
    - Takeaway: You usually need two separate statements in the IAM policy to fully access a bucket.
1. You have 500 Data Science projects. Creating 500 different IAM Roles (ProjectA_Role, ProjectB_Role...) is unmanageable. How do you design a scalable permission system so new projects don't require IAM updates?
    - The Answer: I would switch from RBAC (Role-Based) to ABAC (Attribute-Based Access Control).
    - The Strategy:
        1. Tag the IAM Role with Project = Project A.
        2. Tag the Resources (S3 Buckets, Glue Jobs) with Project = Project A.
        3. Write One Single IAM Policy: 
            ```
            Allow s3:*
            Condition: StringEquals: { aws:RequestTag/Project: ${aws:PrincipalTag/Project} }
            ```
    - The Result: When a user assumes the role, IAM checks if their tag matches the resource's tag. If we add Project C, we just tag the new bucket. We never touch the IAM policy again.
1. You want to let your Senior Data Engineers create IAM Roles for their Lambda functions, but you want to guarantee they never create a role with `AdministratorAccess`. How do you enforce this without blocking their ability to create roles?
    - The Answer: I would use IAM Permissions Boundaries.
    - The Mechanism: Create a policy called `DataEngBoundary` that allows S3 and Glue but denies IAM and Billing. Give the Engineers permission to `iam:CreateRole`, but add a Condition: They can only create a role if they attach the `DataEngBoundary` policy to it.
    - The Outcome: Even if the engineer writes a policy saying Allow *:* (Admin) and attaches it to the new role, the Boundary acts as a hard ceiling. The effective permission is the intersection of the two. The role will never exceed the boundary.