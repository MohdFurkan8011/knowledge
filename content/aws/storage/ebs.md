## Elastic Block Storage

- [What EBS Actually Is](#what-ebs-actually-is)
- [Persistent Storage](#persistent-storage)
- [AZ Scoped](#az-scoped)
- [Network Attached](#network-attached)
- [EBS volume type](#ebs-volume-type)
- [EBS Snapshots](#ebs-snapshots)
- [Encryption](#encryption)
- [EBS vs Instance Store](#ebs-vs-instance-store)
- [Multi Attach](#multi-attach)
- [Performance Concepts](#performance-concepts)
- [Resizing volue](#resizing-volue)

### What EBS Actually Is

Amazon EBS is a persistent block storage service for use with Amazon EC2. It provides storage volumes that you attach to EC2 instances, similar to how you would attach a hard drive to a physical server.

- Block storage
- Works only with EC2
- Data persists even if instance stops
- Scoped to a single Availability Zone (AZ)
- Designed for low-latency, high-performance workloads

Think:
EC2 = compute
EBS = hard drive

### Persistent Storage

- Data remains after instace stop/start
- Deleted only
 - You manually delete it
 - ***"Delete on termination"*** is enabled

### AZ Scoped

- An EBS volume lives in one availability zone
- Can only attach to EC2 in the same AZ
- To move across AZ -> create a snapshot -> restore in new AZ

### Network Attached

- EBS is network-attached storage, not physically attached.
That means:
- Slight latency compared to instance store
- Can detech and reattach to another EC2

### EBS volume type

- **1. SDD - Based Volume (For transactional workloads)**
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

- **2. HDD Based Volumes (For throughput)**
  - ***st1 (Throughput optimized HDD)***
   - Big data
   - Data warehousing
   - Log processing
  - ***sc1 (Cold HDD)***
   - Lowest cost
   - Infrequently accessed data

## EBS Snapshots

Snapshots are backups of EBS volumes stored in:
- Incremental (only changes stored after first snapshot)
- Region-scoped (not AZ-scoped)
- Used to:
 - Backup volumes
 - Copy across regions
 - Create AMIs
 - Restore in another AZ

 ### Encryption

 EBS supports encryption:
 - At rest
 - In transit (between EC2 and EBS)
 - Snapshots
 - AMIs created from encrypted volumes
 Uses:
👉 AWS Key Management Service

### EBS vs Instance Store

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

## Multi Attach

io1 / io2 volue support 👉 Multi-Attach
- Attach one volume to multiple EC2 instances
- Same AZ only
- Used for clustered applications

## Performance Concepts

IOPS - Input/Output operations per second
Throughput - MB/s transferred
Burst - gp2 volumes can burst performance

## Resizing volue
- Increase volume size
- Change volume type
- Increase IOPS

Cannot:
- Reduce size