## Beanstalk

- [What is AWS Elastic Beanstalk?](#what-is-aws-elastic-beanstalk)
- [How Elastic Beanstalk Works](#how-elastic-beanstalk-works)
- [Elastic Beanstalk Architecture](#elastic-beanstalk-architecture)
- [Supported Platforms](#supported-platforms)
- [Deployment Options](#deployment-options)
- [Scalling](#scaling)
- [Monitoring](#monitoring)
- [Security](#security)
- [Use Cases](#use-cases)
- [Pros and Cons](#pros-and-cons)


### What is AWS Elastic Beanstalk?

AWS Elastic Beanstalk (EB) is a Platform-as-a-Service (PaaS) that lets you deploy and manage applications without worrying about the underlying infrastructure.

- Supports multiple languages and platforms: Java, .NET, Node.js, Python, PHP, Go, Ruby, and Docker.
- Automatically handles:
- Provisioning EC2 instances
- Load balancing (ELB)
- Auto scaling
- Application health monitoring

Exam tip: EB is not a container service by default, but it supports Docker too.

### How Elastic Beanstalk Works

**1. Upload Application**
- Code + optional Dockerfile for containers
**2. Select Platform**
- EB handles OS, runtime, and web server configuration
**3. Deployment**
- EB provisions EC2 instances, Auto Scaling group, ELB, security groups, CloudWatch alarms
**4. Management & Monitoring**
- EB provides web console, CLI, and API to monitor health and scale

### Elastic Beanstalk Architecture

- **Environment →** a running application instance (can be web server or worker environment).
- **Application Versions →** versioned deployment packages.
- **Environment Tier:**
  - Web Server Tier → handles HTTP requests
  - Worker Tier → processes background jobs (using SQS queues)
- ***Managed Resources:**
  - EC2 instances
  - Auto Scaling Group
  - Elastic Load Balancer
  - RDS (optional)

### Supported Platforms

- **Languages:** Java, Python, Node.js, Ruby, Go, PHP, .NET
- **Containers:** Docker (single or multi-container using ECS under the hood)
- **Web Servers:** Apache, Nginx, IIS

### Deployment Options

- Single instance → for testing, dev environments
- Load balanced → for production, high availability
- Rolling deployments → updates with minimal downtime
- Immutable deployments → new environment for updates, rollback friendly

### Scaling

- **Auto Scaling:** 
  - Scale EC2 instances based on CPU, memory, or request metrics
  - Integration with ELB for load distribution
- Manual scaling also possible

### Monitoring

- CloudWatch integration
- EB health dashboard:
  - Green → healthy
  - Yellow → warning
  - Red → unhealthy

### Security

- IAM roles for EB environment → EC2 instances and EB service
- Security Groups for network access
- Encrypted communication (HTTPS) with ELB
- Supports VPC deployment

### Use Cases

- Quickly deploy web applications without managing infrastructure
- Rapid prototyping or proof of concept
- Standard web applications with autoscaling needs
- Worker queues and background jobs

### Pros and Cons

| Pros                                     | Cons                                               |
|-----------------------------------------|---------------------------------------------------|
| Fast application deployment              | Less control over underlying resources           |
| Auto scaling and ELB included            | Not ideal for highly customized infra            |
| Supports multiple platforms              | Debugging can be harder in managed environments  |
| Easy rollback & version management       | Docker support less flexible than ECS/EKS        |
| Integrated monitoring & alerts           | Limited for complex microservices orchestration  |

### Exam Tips

- EB = PaaS, not container orchestration, but supports Docker.
- Automatically manages EC2, ELB, Auto Scaling, and monitoring.
- Can deploy web server tier or worker tier.
- Use rolling or immutable deployments for updates.
- Good for simple web apps or quick deployments; not for complex Kubernetes workloads.