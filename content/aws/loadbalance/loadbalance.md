## Load Balance

- [AWS Load Balancer (Elastic Load Balancing – ELB)](#aws-load-balancer-elastic-load-balancing--elb)
- [Why Load Balancer is Needed](#why-load-balancer-is-needed)
- [Types of AWS Load Balancers](#types-of-aws-load-balancers)
- [Important Load Balancer Concepts](#important-load-balancer-concepts)
- [When to Use Which Load Balancer](#when-to-use-which-load-balancer)
- [What is Cross-Zone Load Balancing?](#what-is-cross-zone-load-balancing)
- [Some more points](#some-more-points)


**Load Balancer** is one of the most important services for building scalable and highly available applications. Let’s break it down clearly with types, architecture, and real use cases.


### AWS Load Balancer (Elastic Load Balancing – ELB)

**AWS Elastic Load Balancing (ELB)** automatically distributes incoming traffic across multiple targets like:

- EC2 instances
- Containers (ECS / Kubernetes)
- IP addresses
- Lambda functions

### Why Load Balancer is Needed

Without a load balancer:
> User → EC2 Server

Problems:
- Single point of failure
- Server overload
- Poor scalability

With a load balancer:
> Users → Load Balancer → Multiple EC2 Servers

Benefits:
- High availability
- Automatic scaling
- Fault tolerance
- Health monitoring

### Types of AWS Load Balancers

AWS provides 4 types of load balancers.
- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)
- Classic Load Balancer (CLB) (legacy)

- **1. Application Load Balancer (ALB)**
    Entity: Application Load Balancer
    Works At - Layer 7 (Application Layer) of the OSI model.
    **Supports**
      - HTTP
      - HTTPS
      - WebSocket
      - gRPC
    **Features**
      - Path-based routing
      - Host-based routing
      - Microservices support
      - Container support
      - Lambda support


- **2. Network Load Balancer (NLB)**
    Entity: Network Load Balancer
    Works At - Layer 4 (Transport Layer)
    **Protocols:**
      - TCP
      - UDP
      - TLS
    **Features**
      - Ultra high performance
      - Millions of requests per second
      - Static IP support
      - Extremely low latency
    **Real Use Cases**
      - Gaming Servers
      - Financial trading systems

- **3. Gateway Load Balancer (GWLB)**
    Entity: Gateway Load Balancer
    **Purpose**
    Used to deploy network security appliances.
    Examples:
      - Firewalls
      - Intrusion detection
      - Packet inspection

- **4. Classic Load Balancer (CLB)**
    Entity: Classic Load Balancer
    Older version of load balancer.
    Works at:
      - Layer 4
      - Layer 7
    Limitations:
      - No advanced routing
      - No microservice support
    AWS recommends using ALB or NLB instead.


### Important Load Balancer Concepts

**1. Target Groups**
Load balancer sends traffic to target groups.
Targets can be:
- EC2 instances
- Containers
- IP addresses
- Lambda

**2. Health Checks**
Load balancer constantly checks instance health.
Example:
> GET /health

If unhealthy:
> ALB removes instance from rotation

**3. Listener**
Listener defines protocol + port.
Example:
```
HTTP : 80
HTTPS : 443
```

**Auto Scaling Integration**
Entity: Amazon EC2 Auto Scaling
Flow:
> Users → Load Balancer → Auto Scaling Group → EC2 Instances


### When to Use Which Load Balancer

**Use ALB when**
- Web applications
- REST APIs
- Microservices
- Containers (ECS / EKS)

**Use NLB when**
- Ultra high performance
- TCP/UDP traffic
- Static IP needed

**Use GWLB when**
- Security appliances
- Network inspection


### What is Cross-Zone Load Balancing?

**Cross-zone load balancing** is a feature where a load balancer **distributes incoming traffic evenly across all registered targets in all Availability Zones (AZs)**, instead of only balancing traffic within the same AZ as the incoming request.

- Without cross-zone balancing: Traffic from an AZ’s clients only goes to targets in the same AZ.
- With cross-zone balancing: Traffic from any AZ can go to targets in any AZ, improving utilization and performance.

***How It Works***
Imagine you have:
- 2 AZs: us-east-1a and us-east-1b
- Each AZ has 2 EC2 instances
- Traffic split is uneven (AZ1 gets 70% of requests, AZ2 gets 30%)

***Important Notes***
1. ALB - Cross-zone balancing **enabled by default**.
2. NLB - Cross-zone balancing is disabled by default, you can enable it.
3. CLB - Needs explicit enablement.

***Cost:***
- Cross-zone balancing may incur inter-AZ data transfer charges because traffic can cross AZs.


### Some more points

- ELB is region specific
- ***A listener*** is a process that checks for connection requests on a specific port and protocol on your load balancer. Think of it as the gatekeeper that says: “Who wants in and how should I handle them?”
- It may take sometime for the registration of the EC2 instances under the ELB to complete
- ELB has nothing to do with the outbound traffic
- ELD only has to do with inbound traffic destined to the EC2 registered instance and the respective return traffic
- You start to be charged hourly(also for partial hours). Once your ELB is active
- Deleting the ELB does not affect or delete the EC2 instance registered with it.

***What is a Node in ELB?***

In AWS Elastic Load Balancing, a node is essentially a load balancer instance running in a specific Availability Zone (AZ).

- Each node is the actual server that receives traffic from clients.
- When you create an ELB, AWS automatically deploys nodes in each AZ you enable.
- These nodes are managed by AWS — you don’t have to worry about the underlying servers.

***Key Points About ELB Nodes***
**1. Redundancy**
- AWS deploys at least one node per enabled AZ.
- If you enable multiple AZs, you get multiple nodes, one in each AZ.
- Helps ELB stay highly available.

**2. Elasticity**
- Nodes can scale automatically based on traffic.
- You never manage these nodes directly; AWS handles scaling.

**3. Target Routing**
- Each node routes traffic to the targets in the same AZ (without cross-zone enabled) or any AZ (with cross-zone enabled).

**4. Target Routing**
- Each node performs health checks on targets in its AZ (or cross-zone) to ensure only healthy targets receive traffic.

***Important Notes***
1. You never directly manage nodes. They are fully managed by AWS ELB service.
2. Number of nodes can increase automatically as traffic grows.
3. Nodes are the entry point for client requests, and the load balancer distributes traffic from these nodes to your targets.