## ECS - Elastic Container Service

- [What is AWS ECS?](#what-is-aws-ecs)
- [ECS Architecture](#ecs-architecture)
- [ECS Launch Types](#ecs-launch-types)
- [Integrations & Ecosystem](#integrations--ecosystem)
- [ECS Networking](#ecs-networking)
- [ECS Task Auto Scaling](#ecs-task-auto-scaling)
- [ECS with CI/CD](#ecs-with-cicd)
- [ECS Security](#ecs-security)
- [ECS vs EKS vs Lambda](#ecs-vs-eks-vs-lambda)
- [ECS Exam Pointers](#ecs-exam-pointers)


### What is AWS ECS

AWS Elastic Container Service (ECS) is a fully managed container orchestration service that allows you to run, scale, and secure Docker containers on AWS.
It abstracts the underlying infrastructure so you don’t have to manage EC2 instances unless you choose to.

- ECS supports Docker containers only.
- It integrates with IAM, CloudWatch, ELB, and Auto Scaling.
- There are two launch types: Fargate and EC2.
- ECS can manage stateful and stateless workloads.

### ECS Architecture

ECS has a layered architecture:

**1. Cluster**
- A logical grouping of tasks and services.
- Can be made of:
  - EC2 instances (self-managed compute), or
  - Fargate (serverless, AWS-managed compute).

**2. Task Definition**
- JSON blueprint for running containers.
- Defines:
  - Container image
  - CPU and memory
  - Port mappings
  - Environment variables
  - Log configuration
  - IAM roles for tasks
- Must be versioned; each update creates a new revision.

**3. Task**
- A running instance of a task definition.
- Can run on EC2 or Fargate.
- Can be single-container or multi-container.

**4. Service**
- Ensures a specified number of tasks are running and healthy.
- Can attach to a load balancer (ALB/NLB).
- Supports auto scaling.
- Key for production workloads.

**5. Container Agent**
- Runs on each EC2 instance.
- Communicates with ECS control plane.
- Not required with Fargate (AWS manages it).

### ECS Launch Types

**1. EC2 Launch Type**
- You manage the EC2 instances.
- Good if you need:
  - Custom AMIs
  - GPU workloads
  - Cost optimization by reserving EC2
- ECS schedules tasks on your instances.

**2. Fargate Launch Type**
- Serverless containers.
- AWS manages the infrastructure.
- You only define task CPU/memory.
- Reduces operational overhead.
- You pay per vCPU + GB memory per second.

### Integrations & Ecosystem

ECS integrates tightly with AWS services:
| Service                          | Purpose                           |
|----------------------------------|-----------------------------------|
| IAM                              | Define permissions for tasks/services |
| CloudWatch                        | Logs & metrics                    |
| ECR (Elastic Container Registry) | Store Docker images               |
| ALB/NLB                           | Load balancing                    |
| Secrets Manager / SSM Parameter Store | Store secrets securely          |
| Auto Scaling                      | Scale services or EC2 cluster     |
| VPC & Security Groups             | Network isolation                 |

### ECS Networking

- ECS tasks run in a VPC.
- Can use bridge, host, or awsvpc network mode:
  - **bridge:** default Docker network (EC2 only)
  - **host:** task uses EC2 host network (low latency)
  - **awsvpc:** each task gets its own ENI & IP, required for Fargate 

### ECS Task Auto Scaling

- ECS allows service auto scaling based on:
  - CPU utilization
  - Memory utilization
  - Custom CloudWatch metrics
- Cluster auto scaling (EC2 only):
  - Adjusts number of EC2 instances in cluster automatically.

### ECS with CI/CD

- **Common flow:**
  - Push Docker image to ECR
  - Update ECS task definition
  - Deploy new revision via ECS service
- **Can integrate with:**
  - CodePipeline
  - CodeBuild
  - CodeDeploy

- **Exam Tip: ECS is blue/green deployable via CodeDeploy.**

### ECS Security

- **IAM Roles for Tasks →** fine-grained permissions for each task.
- **Security Groups & VPC →** network isolation.
- **Secrets Manager/SSM →** store sensitive environment variables.
- **Encryption at rest & transit →** optional for data.

### ECS vs EKS vs Lambda

| Feature        | ECS                 | EKS              | Lambda            |
|----------------|-------------------|-----------------|-----------------|
| Managed        | Yes               | Yes             | Yes             |
| Orchestration  | ECS service       | Kubernetes      | No              |
| Learning curve | Low               | High            | Low             |
| Cost model     | Pay for EC2/Fargate | Pay for EC2/EKS cluster | Pay per execution |

### ECS Exam Pointers
- ECS supports Docker only, not other container runtimes.
- Fargate tasks require awsvpc network mode.
- Know task definition vs service vs cluster.
- Understand ECS + ALB + Auto Scaling pattern.
- Know integrations with ECR, IAM, CloudWatch, and Secrets Manager.
- Understand pricing differences: EC2 vs Fargate.