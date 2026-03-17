## Elastic Kubernate Service

- [What is AWS EKS?](#what-is-aws-eks)
- [EKS Architecture](#eks-architecture)
- [EKS Launch Options](#eks-launch-options)
- [Networking](#networking)
- [Integrations](#integrations)
- [EKS vs ECS](#eks-vs-ecs)
- [Scaling in EKS](#scaling-in-eks)
- [Security in EKS](#security-in-eks)
- [Exam Pointers](#exam-pointers)
- [AWS Container Services Cheat Sheet](#aws-container-services-cheat-sheet)

### What is AWS EKS?

AWS Elastic Kubernetes Service (EKS) is a fully managed Kubernetes service. It lets you run Kubernetes clusters on AWS without managing the control plane.
- AWS manages the master/control plane (API server, etcd, scheduler).
- You manage the worker nodes (EC2 instances or Fargate).
- Supports Kubernetes-native workloads.
- Integrates with IAM, VPC, CloudWatch, ALB/NLB, and autoscaling.
- Certification Tip: EKS is AWS’s managed Kubernetes offering. Know how it differs from ECS.

### EKS Architecture

**1. Control Plane**
- Managed by AWS.
- Consists of:
  - API server
  - etcd (cluster state)
  - Scheduler & controller manager
- Redundant & highly available across multiple AZs.
- AWS charges per cluster per hour.

**2. Worker Nodes**
- EC2 instances or Fargate pods.
- Join the cluster via kubelet and IAM role.
- Managed via Node Groups:
  - **Managed Node Groups →** AWS manages scaling, patching, and lifecycle.
  - **Self-managed Node Groups →** You handle updates and scaling.

**3. Pods & Services**
- Pod = smallest deployable unit (1+ containers)
- Deployment manages replicas of pods
- Service exposes pods internally (ClusterIP) or externally (LoadBalancer)

### EKS Launch Options

**1. EC2 Worker Nodes**
- You manage the EC2 instances.
- Full control over:
  - AMI
  - Instance type
  - Node auto scaling
- Integrates with Cluster Autoscaler to scale nodes based on pods.

**2. Fargate**
- Serverless worker nodes.
- AWS manages the infrastructure.
- Pods run without needing EC2.
- Each pod gets its own ENI & IP (awsvpc mode).

**Exam Tip: Fargate in EKS = serverless pods, pay per CPU/memory.**

### Networking

- EKS pods run in a VPC.
- Uses CNI plugin (aws-vpc-cni-k8s) to assign each pod an ENI + private IP.
- Services can be exposed via:
  - **ClusterIP →** internal only
  - **NodePort →** port on worker nodes
  - **LoadBalancer →** ALB/NLB integration for external access

### Integrations

| Service                        | Purpose                                       |
|--------------------------------|-----------------------------------------------|
| IAM                            | Pod IAM roles using IRSA (IAM Roles for Service Accounts) |
| CloudWatch                     | Logs & metrics for pods                       |
| ECR                            | Container image repository                    |
| ALB/NLB                        | Load balancing for services                   |
| Secrets Manager / SSM          | Manage sensitive data                         |
| Auto Scaling                    | Horizontal pod autoscaling & node autoscaling|
| VPC & Security Groups           | Network isolation and pod security           |

**Exam Tip: Know IRSA → lets a pod assume a specific IAM role, replacing EC2-wide IAM roles.**

### EKS vs ECS

| Feature        | EKS                     | ECS                    |
|----------------|------------------------|------------------------|
| Orchestration  | Kubernetes             | ECS service scheduler  |
| Learning curve | High                   | Low                    |
| Control        | Full Kubernetes API    | AWS-managed abstraction|
| Worker nodes   | EC2 / Fargate          | EC2 / Fargate          |
| CI/CD          | Kubectl, Helm, ArgoCD  | CodePipeline, ECS Service |

**Tip: Exam often asks: “Use EKS when you need Kubernetes-native workloads or multi-cloud portability.”**

### Scaling in EKS

- **Horizontal Pod Autoscaler (HPA) →** scales pods based on CPU/memory/custom metrics
- **Vertical Pod Autoscaler (VPA) →** adjusts pod resources
- **Cluster Autoscaler →** scales worker nodes based on pending pods
- **Fargate →** automatically scales pods serverlessly

### Security in EKS

- **IAM for nodes →** nodes get an IAM role for AWS API calls
- **IRSA →** pods get per-service IAM roles
- **Security Groups & VPC →** network isolation
- **Secrets Manager & SSM Parameter Store →** manage secrets
- **RBAC (Kubernetes) →** controls access at API level
- **Pod Security Policies / OPA Gatekeeper →** optional advanced security

### Exam Pointers

- Know EKS components: control plane vs worker nodes.
- Understand IRSA for pod-level IAM access.
- Fargate pods = serverless compute.
- Pods are scheduled by Kubernetes scheduler.
- Worker nodes can be managed or self-managed.
- Autoscaling includes HPA, VPA, and cluster autoscaler.
- Networking is VPC-native with ENIs.

💡 Shortcut Memory Tip for Exams:
- ECS = AWS-managed container orchestration (Docker-only)
- EKS = Managed Kubernetes (multi-cloud, pods, more complex)
- Fargate = Serverless compute for both ECS & EKS


### AWS Container Services Cheat Sheet

| Feature / Aspect       | ECS                                           | EKS                                                      | Fargate                                 |
|------------------------|-----------------------------------------------|----------------------------------------------------------|-----------------------------------------|
| Type                   | AWS-managed container orchestration          | Managed Kubernetes                                       | Serverless container compute            |
| Orchestration          | ECS service scheduler                         | Kubernetes scheduler                                     | N/A (serverless, works with ECS/EKS)   |
| Containers Supported   | Docker only                                  | Docker / OCI containers                                  | Docker / OCI containers                 |
| Control Plane          | Fully AWS-managed                             | AWS-managed Kubernetes control plane (API server, etcd) | Managed by AWS                           |
| Worker Nodes           | EC2 (user-managed) or Fargate                | EC2 (managed/self-managed) or Fargate                   | Serverless, no EC2                       |
| Launch Types           | EC2, Fargate                                 | EC2 Node Groups, Fargate pods                            | Only Fargate                             |
| Networking             | bridge / host / awsvpc                        | awsvpc (ENI per pod)                                     | awsvpc (ENI per task/pod)               |
| Scaling                | Service Auto Scaling (tasks) + Cluster Auto Scaling (EC2) | HPA (pods), VPA, Cluster Autoscaler (nodes)             | Auto scales per task/pod automatically  |
| Load Balancing         | ALB / NLB                                    | ALB / NLB / Ingress                                      | Works with ECS/EKS services ALB/NLB     |
| IAM Integration        | IAM Roles for Tasks                           | IRSA (IAM Roles for Service Accounts)                    | Works with ECS/EKS IAM integration      |
| Secrets Management     | AWS Secrets Manager / SSM                     | AWS Secrets Manager / SSM                                 | Works with ECS/EKS                       |
| CI/CD                  | CodePipeline, CodeBuild, CodeDeploy           | Kubectl, Helm, ArgoCD, CodePipeline                      | Works with ECS/EKS pipelines             |
| Pros                   | Simple, AWS-native, easy for Docker workloads | Full Kubernetes API, portable, flexible                  | Serverless, zero infra management        |
| Cons                   | Docker only, AWS-specific                     | Complex, learning curve                                   | Limited customization, pay-per-resource |
| Exam Keywords          | Tasks, Services, Clusters, Task Definitions  | Pods, Deployments, Node Groups, Control Plane, IRSA      | Serverless tasks/pods, pay-per-resource |