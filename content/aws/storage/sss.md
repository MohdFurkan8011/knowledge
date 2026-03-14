## Simple Storage Service

- [What S3 Actually Is](#what-s3-actually-is)
- [Core Concepts](#core-concepts)

Amazon S3 (Simple Storage Service)

Amazon S3 is AWS’s fully managed object storage service designed for:
- Massive scalability
- High durability
- Global accessibility
- Low cost storage

### What S3 Actually Is
S3 is:
✅ Object storage
✅ Regional service
✅ Infinitely scalable (practically unlimited)
✅ 99.999999999% durability (11 9’s)
✅ Accessible over HTTP/HTTPS

It stores:
Objects inside Buckets

### Core Concepts
- **1. Bucket**
    - Container for objects
    - Globally unique name
    - Defined in a Region
- Data automatically replicated across multiple AZs

✅ Object
An object consists of:
- Data (file)
- Metadata
- Key (unique identifier inside bucket)
- Version ID (if versioning enabled)
Max object size:
- 5 TB
- Single upload limit = 5 GB (above that use Multipart Upload)

**Storage Classes**

***S3 Standard***
- General purpose
- Low latency
- High durability
- Used for active data

***Infrequent Access***
S3 Standard-IA
 - Lower storage cost
 - Retrieval fee
 - For infrequently accessed but critical data

S3 One Zone-IA
- Stored in single AZ
- Cheaper
- Not resilient to AZ failure

**Versioning**
When enabled:
- Keeps multiple versions of objects
- Protects against accidental deletion
- Required for replication

**S3 Replication**
- Cross-Region Replication (CRR)
- Same-Region Replication (SRR)

**Security**
- Bucket Policies: Resource-based policies
- IAM Policies: User/role-based policies
- Block Public Access: Prevents accidental public exposure
- Encryption
 - SSE-S3
 - SSE-KMS (uses 👉 AWS Key Management Service)
 - SSE-C (customer provided keys)

**S3 Access Methods**
- AWS Console
- AWS CLI
- SDK
- REST API
- Pre-signed URLs (temporary access)

**Lifecycle Policies**

Automatically:
- Transition between storage classes
- Expire/delete objects

Example:    
- After 30 days → Standard-IA
- After 90 days → Glacier
- After 365 days → Delete
- Cost optimization question → lifecycle policy answer.

**S3 Event Notifications**

Can trigger:
- AWS Lambda
- Amazon SQS
- Amazon SNS

Used for:
- Image processing
- ETL pipelines
- Notifications