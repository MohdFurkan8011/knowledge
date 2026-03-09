## Elastic File System

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