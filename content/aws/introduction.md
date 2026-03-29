## Introduction

- [Deployment Model of Clouds](#deployment-model-of-clouds)
- [Cloud Computing Services](#cloud-computing-services)
- [Availability Zone](#availability-zone)
- [Edge Location](#edge-location)
- [Local Zone](#local-zone)
- [Region](#region)


### Deployment Model of Clouds

Cloud ***deployment models*** describe where the cloud infrastructure is hosted and who can access it. According to ***National Institute of Standards and Technology (NIST)***, there are four main deployment models.

- **1. Publish Cloud**
    ***Definition:***
    Infrastructure is owned and managed by a cloud provider and services are available to the ***general public over the internet***.

    ***Example providers:***
     - Amazon Web Services
     - Microsoft Azure
     - Google Cloud

    ***Characteristics***
     - Pay-as-you-go pricing
     - Highly scalable
     - No hardware maintenance by the user

    Example
    A company runs its application on Amazon EC2 in AWS.

- **2. Private Cloud**
    ***Definition:***
    Cloud infrastructure is used only by ***a single organization.***

    It can be:
     - Hosted on-premise (company data center)
     - Hosted by a third-party provider but dedicated to one company

    ***Characteristics***
     - High security and control
     - Customizable infrastructure
     - More expensive

    Example
    A bank hosting its own cloud infrastructure in its internal data center.

- **3. Hybrid Cloud**
    ***Definition:***
    A combination of public cloud and private cloud that work together.

    Example architecture:
    ```
    Private Cloud (Company Data Center)
        |
        | Secure Connection
        |
    Public Cloud (AWS)
    ```
    Example scenario:
     - Sensitive data stored in private cloud
     - Application servers running in Amazon Web Services

- **4. Community Cloud**
    Definition:
    Cloud infrastructure shared by ***multiple organizations with similar requirements.***
    Example:
     - Government agencies
     - Healthcare organizations


### Cloud Computing Services

Cloud computing services are commonly categorized into three service models: IaaS, PaaS, and SaaS. These describe how much of the infrastructure and software is managed by the cloud provider vs the user.

- **1. IaaS (Infrastructure as a Service)**
    ***Definition:***
    The cloud provider gives you basic infrastructure like servers, storage, and networking. You manage the OS, applications, and data.

    ***Example services:***
     - Amazon EC2
     - Amazon EBS
     - Google Compute Engine

    ***Example scenario:***
    You launch a VM in EC2 and install:
     - Linux/Windows
     - Java
     - MySQL
     - Your application

    You control almost everything.
    ***User manages***
     - OS
     - Runtime
     - Applications
     - Data

    ***Provider manages***
     - Hardware
     - Networking
     - Data center

- **2. PaaS (Platform as a Service)**
    ***Definition:***
    The cloud provider manages the ***infrastructure + operating system + runtime environment.*** You only deploy your application code.

    ***Example services:***
     - AWS Elastic Beanstalk
     - Google App Engine
     - Azure App Service

    ***Example scenario:***
    You upload a Spring Boot application, and the platform automatically handles:
     - Server setup
     - Scaling
     - OS updates
     - Runtime installation
    
    ***User manages***
     - Application code
     - Data

    ***Provider manages***
     - OS
     - Runtime
     - Servers
     - Networking

- **3. SaaS (Software as a Service)**
    ***Definition:***
    The cloud provider manages everything. Users simply access the software via a browser or app.
    
    Examples:
     - Gmail
     - Salesforce
     - Google Docs

    ***Example scenario:***
    You just log in and use the application.
    You do not manage servers, OS, or application deployment.


### Availability Zone

An Availability Zone is a full AWS data center (or group of data centers) used to run core services.

Example services running in AZ:
- Amazon EC2
- Amazon RDS
- Amazon EBS

In Amazon Web Services (AWS), infrastructure is organized in multiple layers so applications can be highly available, fault-tolerant, and low latency. The common terms are Region, Availability Zone, Local Zone, and Edge Location. Each exists for a specific reason.

Definition:
An Availability Zone is a ***physically separate data center*** (or group of data centers) inside an AWS Region.

**Reason / Purpose**
- High fault tolerance
- Protect applications from data center failure
- Allow multi-AZ deployments

**Key Characteristics**
- Multiple AZs exist in one Region (usually 3+)
- Connected with high-speed private networking
- If one AZ fails, others continue running

Example
In ***Asia Pacific (Mumbai)** Region there are AZs like:
- ap-south-1a
- ap-south-1b
- ap-south-1c

**Typical Use**
- Run database replicas in different AZs
- Load balancing across AZs

## Edge Location

Definition:
An ***Edge Location*** is a ***data center used for caching content close to users.***

Used mainly by:
- Amazon CloudFront
- AWS Global Accelerator
- Amazon Route 53

Reason / Purpose
- Reduce latency
- Deliver content faster to end users

**Example**
When a user in Delhi accesses a website:
- Content is served from the nearest Edge Location
- Instead of the main region (like Mumbai)

**Typical Use**
- CDN for images, videos, websites
- DNS routing


### Local Zone

Definition:
A **Local Zone** is an AWS infrastructure extension that places ***compute and storage closer to large cities.***

**Reason / Purpose**
- Ultra-low latency (single-digit milliseconds)
- Applications needing very fast response time

**Use Cases**
- Gaming
- Video rendering
- AR/VR
- Media production

Example
Applications hosted in **Asia Pacific (Mumbai) Region** may use a Delhi Local Zone to serve users faster.


### Region

A Region is a geographical area containing multiple Availability Zones.

**Example:**
- Asia Pacific (Mumbai) Region
- US East (N. Virginia) Region

**Reason**
- Data residency
- Compliance
- Disaster recovery