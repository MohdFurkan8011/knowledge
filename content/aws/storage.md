## Storage
AWS offers a complete range of cloud storage service to support both application and archival compliance requirements. Select from object, file and block storage services as well as cloud data migration option to start designing the foundation of your cloud IT environment.

**Types of storage**
1. [Simple Storage Service](#simple-storage-service)
2. [Elastic File System](#elastic-file-system)
3. [Elastic Block Storage](#elastic-block-storage)
4. [Snowball](#snowball)


#### Simple Storage Service
Amazon S3 (Simple Storage Service)

Amazon S3 is AWS’s fully managed object storage service designed for:
- Massive scalability
- High durability
- Global accessibility
- Low cost storage

**What S3 Actually Is**
S3 is:
✅ Object storage
✅ Regional service
✅ Infinitely scalable (practically unlimited)
✅ 99.999999999% durability (11 9’s)
✅ Accessible over HTTP/HTTPS

It stores:
Objects inside Buckets

**Core Concepts**
✅ Bucket
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

#### Elastic File System

Amazon EFS is a fully managed, scalable file storage service for use with:
- Amazon EC2
- Amazon ECS
- Amazon EKS
- On-premises servers (via VPN / Direct Connect)

**What EFS Actually Is**

EFS is:
✅ Managed file storage
✅ Uses NFS protocol (v4)
✅ Multi-AZ by design
✅ Mountable by multiple instances at the same time
✅ Automatically scales storage up and down

Think:
EBS = one server’s hard drive
EFS = shared network file system

**Core Characteristics**
✅ Regional Service
- EFS is regional, not AZ-scoped.
- Data is automatically stored across multiple Availability Zones
- Highly available
- Fault tolerant

This is a BIG difference from EBS.

**Multi-Instance Access**

- Many EC2 instances
- Across multiple AZs
- Can mount the same file system simultaneously
Perfect for:
 - Shared content
 - CMS
 - Web server fleets
 - Containers

**Elastic & Auto-Scaling**

You:
- Do NOT provision storage size
- Pay only for what you use
- Storage grows and shrinks automatically

**Storage Classes**

EFS has lifecycle management:

🟢 Standard
- Frequently accessed files
🔵 Infrequent Access (EFS-IA)
- Lower cost
- Slightly higher access cost
- Automatically moved after X days

🧊 Archive (EFS Archive)
- Very low cost
- Higher latency
- For rarely accessed data

Lifecycle policies automatically move files between tiers.

**Encryption**
Uses:
👉 AWS Key Management Service

**High Availability**

EFS automatically:

- Replicates data across multiple AZs
- Survives AZ failure
- No manual snapshot setup needed for HA

This makes it simpler than EBS for HA.

**Pricing**

You pay for:

- Storage used (GB/month)
- Requests
- Data transfer (if cross-AZ)

#### Elastic Block Storage
Amazon EBS is a persistent block storage service for use with Amazon EC2. It provides storage volumes that you attach to EC2 instances, similar to how you would attach a hard drive to a physical server.

**What EBS Actually Is (Core Concept)**
- Block storage
- Works only with EC2
- Data persists even if instance stops
- Scoped to a single Availability Zone (AZ)
- Designed for low-latency, high-performance workloads

Think:
EC2 = compute
EBS = hard drive

**Persistent Storage**
- Data remains after instace stop/start
- Deleted only
 - You manually delete it
 - ***"Delete on termination"*** is enabled

**AZ Scoped**
- An EBS volume lives in one availability zone
- Can only attach to EC2 in the same AZ
- To move across AZ -> create a snapshot -> restore in new AZ

**Network Attached**
- EBS is network-attached storage, not physically attached.
That means:
- Slight latency compared to instance store
- Can detech and reattach to another EC2

**EBS volume type**
***SDD - Based Volume (For transactional workloads)***
- ***gp3 (General Purpose SSD)*** Recommended default
 - Balanced price/performance
 - Independent IOPS and throughput scalling
 - Used for
  - Boot volumes
  - Dev/Test
  - Web servers
  - small-medium databaes
- ***gp2 (older version)***
 - Performance scales with size
 - Being replaced by gp3
- ***io1 / io2 (provisioned IOPS SSD)***
 - High performance
 - For critical databases
 - You provision specific IOPS
 - Used for
  - Production DB
  - SAP
  - High transaction system

**HDD Based Volumes (For throughput)**
- ***st1 (Throughput optimized HDD)***
 - Big data
 - Data warehousing
 - Log processing
- ***sc1 (Cold HDD)***
 - Lowest cost
 - Infrequently accessed data

**EBS Snapshots**
Snapshots are backups of EBS volumes stored in:
- Incremental (only changes stored after first snapshot)
- Region-scoped (not AZ-scoped)
- Used to:
 - Backup volumes
 - Copy across regions
 - Create AMIs
 - Restore in another AZ

 **Encryption**
 EBS supports encryption:
 - At rest
 - In transit (between EC2 and EBS)
 - Snapshots
 - AMIs created from encrypted volumes
 Uses:
👉 AWS Key Management Service

**EBS vs Instance Store**

| Feature | Amazon EBS | Instance Store |
|----------|------------|----------------|
| Persistent | ✅ Yes | ❌ No |
| Survives Stop | ✅ Yes | ❌ No |
| Survives Termination | ❌ Usually No (depends on "Delete on Termination") | ❌ No |
| Availability Zone Scoped | ✅ Yes (volume lives in one AZ) | Attached to physical host (same AZ as instance) |
| Can Detach & Reattach | ✅ Yes | ❌ No |
| Backups | ✅ Snapshots supported | ❌ Not supported |
| Encryption | ✅ Supported | ❌ Not supported |
| Best For | Databases, boot volumes, long-term workloads | Cache, buffers, temporary data, scratch space |
| Performance | Network-attached | Very high (physically attached) |

**Multi Attach**
io1 / io2 volue support 👉 Multi-Attach
- Attach one volume to multiple EC2 instances
- Same AZ only
- Used for clustered applications

**Performance Concepts**
IOPS - Input/Output operations per second
Throughput - MB/s transferred
Burst - gp2 volumes can burst performance

**Resizing volue**
- Increase volume size
- Change volume type
- Increase IOPS

Cannot:
- Reduce size

#### Snowball
Snowball storage on AWS refers to a physical data transport solution called AWS Snowball, part of the AWS Snow Family offered by Amazon Web Services.
It’s designed to move large amounts of data (terabytes to petabytes) into and out of AWS securely and faster than transferring over the internet.

**What It Is**

AWS ships you a rugged physical device. You:
- Connect it to your local network.
- Copy your data onto it.
- Ship it back to AWS.
- AWS uploads the data into your cloud storage (like Amazon S3).

**Why Use Snowball?**

It’s useful when:

- 📦 You have huge data volumes (e.g., 100 TB+)
- 🐢 Internet transfer would take weeks or months
- 🔐 You need secure, encrypted transfer
- 🏢 You’re migrating a data center to AWS
- 🌍 You’re collecting data in remote locations

**Snowball vs Snowmobile**
For extreme scale, AWS offers AWS Snowmobile, which is literally a shipping container pulled by a truck for moving exabytes of data.