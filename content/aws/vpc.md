## Virtual Private Cloud

- [Introduction](#introduction)
- [Why VPC Exists](#why-vpc-exists)
- [Main Components of a VPC](#main-components-of-a-vpc)
- [Example Real Architecture](#example-real-architecture)
- [VPC vs Traditional Network](#vpc-vs-traditional-network)
- [Benefits of VPC](#benefits-of-vpc)
- [VPC for a Web App](#vpc-for-a-web-app)
- [Advanced VPC Features](#advanced-vpc-features)
- [Simple Analogy](#simple-analogy)
- [Practice](#practice)

### Introduction

A Virtual Private Cloud (VPC) is a logically isolated private network inside a public cloud provider’s infrastructure where you can run your servers, databases, and applications with full control over networking.

It works like your own private data center inside the cloud, where you control IP addresses, routing, security, and connectivity.

### Why VPC Exists

Without a VPC, cloud resources would be in a **shared public network**, which would be insecure.

A VPC allows you to:
- Isolate your resources
- Control network traffic
- Secure your applications
- Design custom network architecture

Example:
- Internet
- Cloud Provider
- Your VPC (private network)
  - Web Servers
  - Databases
  - Microservices

### Main Components of a VPC

- **1. CIDR Block (IP Range)** Classless Inter-Domain Routing
    CIDR Block (IP Range) stands for Classless Inter-Domain Routing block.
    It is a method used to define a range of IP addresses in networks such as an AWS VPC or subnet.

    CIDR Format
    ```
    IP_address/prefix_length
    10.0.0.0/16
    10.0.0.0 – 10.0.255.255
    ```

    This means your VPC has 65,536 private IP addresses.

- **2. Subnets**
    A subnet divides the VPC into smaller networks.
    Example:
    ```
    VPC: 10.0.0.0/16
    Subnet 1 (Public)  : 10.0.1.0/24
    Subnet 2 (Private) : 10.0.2.0/24
    Subnet 3 (Private) : 10.0.3.0/24

    ### Why `/16` is bigger than `/24`

    | CIDR | Calculation | Total IPs |
    |------|-------------|-----------|
    | /16  | 2^(32-16)   | 65,536    |
    | /24  | 2^(32-24)   | 256       |
    | /28  | 2^(32-28)   | 16        |

    ```
    ***Types***:
    - ***Public Subnet***
    A subnet is public if its route table contains a route to an Internet Gateway.
    Resources can access the internet.
    Examples:
    - Web servers
    - Load balancers
    - ***Private Subnet***
    A subnet is private if it does NOT have a route to the Internet Gateway.
    No direct internet access.
    Examples:
    - Databases
    - Backend services

    | Feature                 | Public Subnet | Private Subnet                |
    |-------------------------|---------------|-------------------------------|
    | Internet Gateway route  | Yes           | No                            |
    | Public IP allowed       | Yes           | Usually No                    |
    | Internet access         | Direct        | Via NAT                       |
    | Use cases               | Web servers   | Databases, backend services   |


- **3. Route Tables**
    Route tables control where network traffic goes.
    Example routes:
    | Destination | Target           |
    |-------------|------------------|
    | 10.0.0.0/16 | Local            |
    | 0.0.0.0/0   | Internet Gateway |

    > If traffic goes to internet → send via Internet Gateway

- **4. Internet Gateway (IGW)**
    An ***Internet Gateway*** allows communication between:
    > VPC  <----> Internet
    Without IGW:
    - Instances cannot reach the internet.
    Used mainly by:
    > Public subnets

- **5. NAT Gateway(Network Address Translation)**
    Network Address Translation (NAT) allows instances in a private subnet to access the internet while preventing the internet from initiating connections to those instances.

    Common AWS NAT Components
    1. NAT Gateway (managed by AWS)
    2. NAT Instance (EC2-based NAT server, older approach)

    Example Use Case
    - Your EC2 instance is in a private subnet.
    - It needs to download updates from the internet.
    - The instance sends traffic → NAT Gateway → Internet Gateway → Internet.

    Return traffic comes back through the same NAT gateway.

    > Private EC2 → NAT Gateway → Internet Gateway → Internet

    Key Points
    - NAT works outbound only (private → internet).
    - Located in a public subnet.
    - Used by private subnets via route tables.

- **6. Security Groups**
    A security group is a virtual firewall for instances.
    Example rules:

    ***Inbound:***
    | Port | Protocol | Source    |
    |------|----------|-----------|
    | 22   | SSH      | My IP     |
    | 80   | HTTP     | 0.0.0.0/0 |
    | 443  | HTTPS    | 0.0.0.0/0 |

    ***Outbound:***
    > Allow all

- **7. Network Access Control List (NACL)**
    It is a stateless firewall used to control inbound and outbound traffic at the subnet level in a VPC.
    Features:
    - Stateless
    - Allow and deny rules
    - Works before security groups

    | Rule        | Action |
    |-------------|--------|
    | Allow HTTP  | Allow  |
    | Block IP    | Deny   |

- **8. Elastic IP**
    ***Elastic IP (EIP)*** is a static public IPv4 address provided by AWS that you can allocate to your AWS account and attach to an EC2 instance.

    Unlike a normal public IP, **an Elastic IP remains the same even if you stop and start the instance.**

    **Key Features**
    | Feature             | Description                                   |
    |---------------------|-----------------------------------------------|
    | Static Public IP    | Fixed public IPv4 address                     |
    | Reusable            | Can be reassigned to another EC2 instance     |
    | Account owned       | Allocated to your AWS account                 |
    | Internet reachable  | Used for public internet communication        |


- **9. VPC Peering**
    VPC Peering is a networking connection that allows two VPCs (Virtual Private Clouds) to communicate privately using AWS’s internal network.

    It enables resources (like EC2 instances) in different VPCs to communicate using private IP addresses.
    **Key Characteristics**
    | Feature                     | Description                                   |
    |-----------------------------|-----------------------------------------------|
    | Private Communication       | Traffic stays within AWS network              |
    | No Internet Gateway needed  | Direct VPC-to-VPC communication               |
    | Uses Private IP             | Instances communicate via private IP addresses|
    | One-to-one connection       | One peering connection links two VPCs         |

    Steps to Set Up VPC Peering
    - Create a VPC Peering Connection
    - Accept the peering request
    - Update route tables in both VPCs

- **10. VPN Gateway**
    A **VPN Gateway** in AWS is a **Virtual Private Network gateway** that allows you to securely connect your on-premises network to your AWS VPC over the internet using an encrypted tunnel.

    In AWS, the commonly used component is the AWS **Virtual Private Gateway**.

    **Purpose**
    A VPN Gateway enables secure communication between your local data center and AWS without exposing traffic publicly.
    > On-Premise Network ⇄ Internet (Encrypted VPN Tunnel) ⇄ VPN Gateway ⇄ VPC

    **Main Components**
    | Component                     | Description                                      |
    |-------------------------------|--------------------------------------------------|
    | Virtual Private Gateway (VGW) | AWS side of the VPN connection                   |
    | Customer Gateway (CGW)        | Your on-premises router or firewall              |
    | VPN Tunnel                    | Encrypted IPSec connection between AWS and your network |

    **Types of AWS VPN**
    | VPN Type        | Description                                      |
    |-----------------|--------------------------------------------------|
    | Site-to-Site VPN| Connects your office/data center to AWS          |
    | Client VPN      | Allows individual users to connect to AWS securely |

### Example Real Architecture

```
               Internet
                   |
             Load Balancer
                   |
           ------------------
           |                |
       Public Subnet    Public Subnet
       (Web Server)     (Web Server)
           |
        NAT Gateway
           |
       Private Subnet
        (App Server)
           |
       Private Subnet
         (Database)
```

### VPC vs Traditional Network

| Feature        | VPC          | Traditional Data Center |
|----------------|--------------|-------------------------|
| Hardware       | Virtual      | Physical                |
| Scalability    | Unlimited    | Limited                 |
| Setup time     | Minutes      | Weeks                   |
| Cost           | Pay as you go| High upfront            |

### Benefits of VPC

- Security
- Custom Networking
- High Availability
- Scalability

### VPC for a Web App

```
VPC
 |
 |-- Public Subnet
 |      |
 |      Load Balancer
 |
 |-- Private Subnet
 |      |
 |      Spring Boot API
 |
 |-- Private Subnet
        |
        PostgreSQL DB
```

### Advanced VPC Features

***VPC Endpoints***
Private connection to AWS services without internet.
> EC2 → S3 (private network)

***Flow Logs***
Monitor network traffic.

***PrivateLink***
Secure service sharing between VPCs.

### Simple Analogy

Think of a ***VPC like an apartment building:***

| Cloud Component   | Real World           |
|-------------------|----------------------|
| VPC               | Apartment building   |
| Subnet            | Floor                |
| Instance          | Apartment            |
| Security Group    | Door lock            |
| Internet Gateway  | Building entrance    |

### Practice

- **Create OWN VPC**
  - Create a VPC, create subnets for this, and install a ec2 instace using this VPC and subnet from Networking option while creating the instace.
  - Your instace can not get connected and can not access the internet.
  - **Internet Gateway** Give the ability of accessing internet to VPC, create a Internet Gateway,
  - After attaching the **internet gateway with VPC**, we need to modify the route table.
  - Edit route, add 0.0.0.0/0 - select target as internet gateway
  - After editing the route table, we can connect the instance, and can update the EC2 instance as well.
  - As we attach a route table with VPC, all subnets are assocated with this route table.

- **How to access private Instace**
  - With the help of **Jump Server or Bastion Host** we can talk with private EC2
  - In this, a public EC2 talk to private EC2, with the help of SSH key

- **How to access internet into this private instance**
  - **NAT(Network Address Translation)**
    - with the help of **NAT(Network Address Translation)** A private EC2 can access internet.
    - We launch a EC2 instace in public VPC with **NAT - AMI(Amazon Machine Image)**
    - This NAT instace should have a Elastic IP
    - After this, we need to add an entry into route table of private VPN subnet route
    - 0.0.0.0/0 and select instace from target.
    - Then go to NAT instace and Setting > Networking > Change source/designation check - check stop
    - **NAT Instance is recommended by Amazon** - Limited data bandwith, Single point of fail, scalbility issue, out of memory
  - **NAT Gateway**
    - Create a NAT gateway and assign a elastic IP address
    - Go to route table, 0.0.0.0/0 and select NAT gateway from target
    - It is fully managed by AWS, so there is no issue of failure

- **Network Access Control List**
  - 