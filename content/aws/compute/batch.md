## AWS Batch

- [What is AWS Batch?](#what-is-aws-batch)
- [Key Concepts](#key-concepts)
- [Architecture](#architecture)
- [Compute Environment Types](#compute-environment-types)
- [Job Scheduling](#job-scheduling)
- [Integrations](#integrations)
- [Use cases](#use-cases)
- [Pros and Cons](#pros-and-cons)
- [Exam Tips](#exam-tips)

### What is AWS Batch?

AWS Batch is a fully managed batch processing service that lets you run large-scale, parallel, or high-performance computing (HPC) workloads on AWS.

- Automatically provisions compute resources (EC2 instances or Spot) for batch jobs.
- Handles job scheduling, queueing, and dependency management.
- Ideal for data processing, simulation, analytics, and rendering jobs.

**Exam tip: AWS Batch = run batch workloads at scale, serverless management of compute.**

### Key Concepts

| Term                 | Description                                                                 |
|----------------------|-----------------------------------------------------------------------------|
| Job                  | A single unit of work (script, program, containerized task)                 |
| Job Definition       | Blueprint for a job (Docker image, vCPU, memory, environment variables, IAM role) |
| Job Queue            | Where jobs are submitted; jobs wait here until resources are available      |
| Compute Environment  | Where jobs run; can be EC2, Spot, or Fargate resources                      |
| Job Scheduling       | AWS Batch automatically schedules jobs based on queue priority and dependencies |

### Architecture

- Submit Job → to a Job Queue
- Job Scheduler → decides which jobs run first based on priority and dependencies
- Compute Environment → provisions EC2 instances or Fargate resources automatically
- Job Execution → runs the job container with specified CPU/memory
- Monitoring & Logging → CloudWatch logs & metrics track progress

**Certification keyword: Job Queue → Job Scheduler → Compute Environment → Execution**

### Compute Environment Types

| Type      | Description                                      |
|-----------|--------------------------------------------------|
| Managed   | AWS manages EC2 instances and scaling for you   |
| Unmanaged | You manage EC2 instances manually               |
| Spot      | Use Spot instances for cost savings             |
| Fargate   | Serverless batch jobs without EC2 instances     |

### Job Scheduling

- FIFO (First In First Out) by default
- Priority → higher priority jobs run first
- Dependencies → job B can wait for job A to finish
- Array Jobs → run multiple copies of a job with different parameters

### Integrations

- **IAM →** Roles for jobs to access AWS services
- **S3 →** Input/output storage for batch jobs
- **ECR →** Store Docker images for containerized jobs
- **CloudWatch →** Logs and metrics
- **CloudTrail →** Audit API calls

### Use Cases

- Large-scale data processing
- Financial simulations
- Genome sequencing or HPC workloads
- Image/video rendering
- Any compute-intensive, parallelizable jobs

### Pros and Cons

| Pros                                      | Cons                                               |
|------------------------------------------|---------------------------------------------------|
| Fully managed, auto scales compute        | Not for real-time workloads                       |
| Supports EC2, Spot, Fargate              | Only batch workloads, not web apps               |
| Job dependencies & scheduling            | Complex setup for small jobs                      |
| Cost-efficient with Spot                  | Limited control over scheduling granularity      |
| Integrates with S3, CloudWatch, ECR      | Requires Docker for containers                   |

### Exam Tips

- AWS Batch is for batch jobs, not web apps.
- Job → Job Definition → Job Queue → Compute Environment → Execution.
- Can use Fargate or EC2 as compute environment.
- Supports array jobs, dependencies, and priorities.
- Cost-saving: use Spot instances.
- Integrates with S3, ECR, CloudWatch, IAM