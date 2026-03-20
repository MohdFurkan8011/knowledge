## EC2

- [What is AWS EC2?](#what-is-aws-ec2)
- [EC2 Architecture](#ec2-architecture)
- [EC2 Instance Types](#ec2-instance-types)
- [EC2 Features](#ec2-features)
- [Pricing Models](#pricing-models)
- [Security Group](#security-group)
- [User data](#user-data)
- [EC2 Networking](#ec2-networking)
- [Security](#security)
- [Use Cases](#use-cases)
- [Pros and Cons](#pros-and-cons)
- [Exam Tips](#exam-tips)

### What is AWS EC2?

Amazon EC2 is a virtual server in the cloud. It provides resizable compute capacity and gives you full control over OS, network, storage, and security.

- You manage the instance, OS, software, scaling, and networking.
- Supports Linux, Windows, and custom AMIs.
- Pay per second, per instance type.

**Exam tip:** EC2 = IaaS → you manage the OS & software; contrast with Fargate (serverless) or Beanstalk (PaaS).

### EC2 Architecture

- Instances → virtual servers running your workloads
- AMIs (Amazon Machine Images) → templates for launching instances
- Instance Types → define CPU, memory, storage, network capacity
- Security Groups & Key Pairs → firewall and SSH/RDP access
- Elastic IPs → static public IPs
- Elastic Block Store (EBS) → persistent storage
- VPC & Subnets → network isolation

### EC2 Instance Types

| Family                            | Use Case                                         |
|----------------------------------|-------------------------------------------------|
| General Purpose (t3, t4g, m6i)   | Balanced CPU/memory, web servers, apps         |
| Compute Optimized (c6i, c7g)     | High CPU, batch processing, HPC                |
| Memory Optimized (r6i, x2idn)    | Databases, analytics, in-memory caching       |
| Storage Optimized (i3, d2)       | Big data, NoSQL, distributed file systems     |
| GPU (p4, g5, inf1)               | ML training, graphics, inference               |
| Burstable (t3, t4g)              | Low-cost, small workloads                       |


**Exam Tip: Know which type is best for compute, memory, or storage-heavy workloads.**

### EC2 Features

- Elastic IPs → static public IPs
- Auto Scaling → add/remove instances automatically
- Load Balancing → ELB integration
- EBS Volumes → persistent storage
- Snapshots → backup volumes
- Placement Groups → optimize latency or fault tolerance
- Instance Store → ephemeral storage, tied to lifecycle
- Security Groups & NACLs → firewall rules

### Pricing Models

| Type           | Description                                               |
|----------------|-----------------------------------------------------------|
| On-Demand      | Pay per second/hour, no commitment                        |
| Reserved       | 1–3 year commitment, cheaper than on-demand              |
| Spot           | Up to 90% cheaper, interruptible workloads               |
| Savings Plans  | Flexible compute discount for EC2, Fargate, Lambda       |


### Security Group

In Amazon Web Services (AWS), a Security Group acts like a virtual firewall that controls incoming (inbound) and outgoing (outbound) network traffic for resources such as Amazon EC2 instances.

***What a Security Group Does***
A Security Group defines rules that determine:

- Who can access your resource
- Which ports/protocols are allowed
- Where the traffic can come from or go to

Think of it as a firewall attached directly to your AWS resource.

- **1. Inbound Rules**
    These rules control who can access your instance.


### User Data


### EC2 Networking

- VPC → Virtual network
- Subnets → public or private
- ENI → Elastic Network Interface
- Security Groups → instance-level firewall
- Elastic IP → static public IP
- NAT Gateway → allow private instances to access the internet

### Security

- Key Pair → SSH (Linux) / RDP (Windows) access
- IAM Roles for EC2 → give permissions to access AWS services
- Security Groups → firewall rules at instance level
- EBS Encryption → encrypt storage

### Use Cases

- Web & app servers
- Databases (self-managed)
- Batch processing & HPC workloads
- Containers (ECS/EKS on EC2)
- Machine learning & GPU workloads

### Pros and Cons

| Pros                                   | Cons                                         |
|---------------------------------------|---------------------------------------------|
| Full control of OS & software          | You manage patching & scaling               |
| Flexible instance types                | Higher operational overhead                 |
| Can use Reserved/Spot pricing          | More complex networking setup               |
| Integrates with ELB, Auto Scaling, VPC| No built-in container orchestration         |
| Persistent storage with EBS            | Costs can be high without scaling           |

### Exam Tips

- EC2 = IaaS → you manage instances
- Know instance types and their use cases
- Spot instances → cheap but interruptible
- IAM roles → give instance permissions to AWS services
- Auto Scaling & ELB → for high availability
- Elastic IP → static public IP, useful for DNS

**EC2 = Virtual server → choose AMI + Instance type → attach EBS → assign Security Group + Key Pair → connect via SSH/RDP → optionally auto-scale.**