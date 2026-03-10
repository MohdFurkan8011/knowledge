## Fargate

- [What is AWS Fargate?](#what-is-aws-fargate)
- [Fargate Architecture](#fargate-architecture)
- [How Fargate Works](#how-fargate-works)
- [Fargate Networking](#fargate-networking)
- [Fargate Security](#fargate-security)
- [Fargate Scaling](#fargate-scaling)
- [Use Cases](#use-cases)
- [Pros and Cons](#pros-and-cons)
- [Exam Tips for Fargate](#exam-tips-for-fargate)


### What is AWS Fargate?

AWS Fargate is a serverless compute engine for containers.

- It allows you to run containers without managing servers or clusters.
- Works with both ECS and EKS.
- You define CPU, memory, and networking, and AWS provisions the infrastructure automatically.

Certification tip: Fargate = “serverless containers” on AWS.

### Fargate Architecture

- No EC2 instances to manage.
- Each task/pod runs in its own isolated compute environment.
- Networking is VPC-native (awsvpc mode), each task/pod gets its own ENI and IP.
- Integrated with IAM roles, Secrets Manager, CloudWatch, and ALB/NLB.

**Key Exam Keywords: awsvpc, ENI per task/pod, serverless, isolated compute.**

### How Fargate Works

**1. Define a Task or Pod**
- **ECS:** Task Definition
- **EKS:** Pod spec
**2. Specify CPU & Memory**
- ECS examples: 0.5 vCPU / 1GB memory
**3. Launch**
- AWS provisions compute automatically
- Each task/pod gets a dedicated ENI and security group rules
**4. Auto Scaling**
- Scales based on ECS service or Kubernetes HPA
**5. Integrations**
- IAM for tasks/pods
- CloudWatch logs & metrics
- Secrets Manager & SSM parameters

### Fargate Networking

- awsvpc mode only
- Each task/pod gets:
  - Private IP
  - ENI attached to VPC
  - Security group isolation
- Allows direct VPC routing and ALB/NLB integration

### Fargate Security

- IAM Roles for Tasks / Pods
  - ECS → Task Role
  - EKS → IRSA (IAM Role for Service Account)
- Secrets Management
  - AWS Secrets Manager / SSM Parameter Store
- VPC & Security Groups
  - Network isolation per task/pod
- Encryption
  - Data at rest and in transit supported

**Exam Keyword: Serverless + isolated IAM roles + secure VPC networking.**

### Fargate Scaling

- Serverless scaling: AWS provisions resources dynamically
- Works with:
  - ECS Service Auto Scaling
  - EKS Horizontal Pod Autoscaler (HPA)
- Pay-per-resource model: only pay for vCPU + memory per second

### Use Cases

- Microservices without managing servers
- Event-driven containers
- CI/CD pipelines
- Short-lived batch jobs
- Applications needing secure isolated compute per container

### Pros and Cons

| Pros                                 | Cons                                           |
|-------------------------------------|-----------------------------------------------|
| No EC2 management                    | Limited CPU/memory combinations               |
| Serverless, auto scaling             | Higher cost for long-running tasks compared to EC2 |
| Works with ECS & EKS                 | Cannot SSH into compute                        |
| Network isolated per task/pod        | Only awsvpc mode supported                     |
| Integrates with IAM, Secrets, CloudWatch | Ephemeral storage limited                   |

### Exam Tips for Fargate

- Always awsvpc network mode.
- Serverless = no EC2 instances to manage.
- Pay for CPU + memory per second.
- Integrates with IAM, Secrets Manager, CloudWatch, ALB/NLB.
- Use for short-lived or microservice workloads.
- Compare with ECS EC2: Fargate = zero infra management, EC2 = cheaper long-term with full control.