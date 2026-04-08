## IAM

**AWS Identity and Access Management (IAM)** is one of the most important services. IAM controls **who can access AWS and what they can do**. Below is a complete structured guide covering everything you should know.

- [What IAM Is](#what-iam-is)
- [IAM Core Components](#iam-core-components)
- [Types of IAM Policies](#types-of-iam-policies)
- [IAM Access Types](#iam-access-types)
- [IAM Security Best Practices](#iam-security-best-practices)


### What IAM Is

**IAM** is a **global AWS service** used to manage **authentication and authorization**.

- ***Authentication*** → Who are you?
- ***Authorization*** → What are you allowed to do?

Example:
A developer can deploy EC2 instances but cannot delete databases.

### IAM Core Components

- **Users**
    An IAM User represents a person or application that interacts with AWS. 
    Example:
      - Developer
      - Admin
      - Application

    Users can login via:
      - AWS Console (username + password)
      - Programmatic access (Access Key + Secret Key)
    Best practice:
      - Do NOT use the root account for daily work

- **Groups**
    A Group is a collection of users with the same permissions.
    Example:
    ```
    Developers Group
        - User1
        - User2
        - User3
    ```
    Permissions are attached to the group, not individual users.

    Benefits:
      - Easier permission management
      - Follows RBAC (Role Based Access Control)

- **Roles**
    An IAM Role is an identity that does not belong to a specific user.
    It is assumed temporarily by:
      - AWS services
      - Applications
      - Other AWS accounts
      - IAM users
    Examples:
      - EC2 accessing S3
      - Lambda accessing DynamoDB
    Advantages:
      - No need to store credentials
      - Temporary security credentials

- **Policies**
    Policies define permissions.
    Policies are written in JSON.

    Example policy:
    ```json
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": "s3:ListBucket",
                "Resource": "*"
            }
        ]
    }
    ```

### Types of IAM Policies

- **AWS Managed Policies**
    Created and maintained by AWS.

    Example:
      - AmazonS3ReadOnlyAccess
      - AdministratorAccess
    Pros:
      - Easy to use
      - Updated by AWS

- **Customer Managed Policies**
    Created by **you**.
    Benefits:
      - Reusable
      - Custom permissions

- **Inline Policies**
    Attached directly to:
      - User
      - Group
      - Role
    Disadvantages:
      - Hard to reuse
      - Not recommended

### IAM Access Types

- **Console Access**
    Used by **humans**.

    Login URL:
    > https://account-id.signin.aws.amazon.com/console

- **Programmatic Access**
    Used by ***applications and scripts.***
    Credentials:
    ```
    Access Key ID
    Secret Access Key
    ```
    Used with:
      - AWS CLI
      - SDK
      - APIs
    
### IAM Security Best Practices

- **Use Root Account Only for Setup**
    The root user has full permissions.
    Best practice:
      - Enable MFA
      - Avoid daily usage

- **Enable MFA (Multi-Factor Authentication)**
    Example:
    > Password + Authenticator app
    Supported:
      - Google Authenticator
      - Hardware token

- **Use Least Privilege Principle**
    Give minimum required permissions.
    Example:
    ❌ Bad
    > AdministratorAccess
    Good
    > Allow only s3:GetObject

- **Rotate Access Keys**
    Access keys should be rotated regularly.
    Best practice:
    > Every 90 days

- **Use Roles Instead of Access Keys**
    Bad:
    > Store access keys inside EC2
    Good:
    > Attach IAM Role to EC2

- **IAM Policy Evaluation Logic**
    AWS checks permissions in this order:
      - Explicit ***DENY***
      - Explicit ***ALLOW***
      - Default ***DENY***

    Rule:
    > Explicit Deny > Allow

    ```
    Example:
    User policy → Allow S3
    Group policy → Deny S3
    ```

- ***IAM Conditions***
  Conditions add restrictions.
  Example:
  Allow only from a specific IP.
  ```
  "Condition": {
    "IpAddress": {
      "aws:SourceIp": "192.168.1.0/24"
    }
  }
  ```

- **Identity Federation**
  Allows login using external providers.
  Example providers:
    - Google
    - Facebook
    - Microsoft
  Use cases:
    - Corporate login
    - Single Sign-On (SSO)

- **IAM Credential Report**
  Provides a report of:
    - User password usage
    - MFA enabled
    - Access key age
  Used for **security auditing**.

- **IAM Access Analyzer**
  Tool to detect public or cross-account access.