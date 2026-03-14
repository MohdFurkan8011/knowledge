## Virtual Private Cloud

- [Introduction](#introduction)
- [Why VPC Exists](#why-vpc-exists)
= [Main Components of a VPC](#main-components-of-a-vpc)

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

- **CIDR Block (IP Range)** Classless Inter-Domain Routing
When creating a VPC, you define an IP range using CIDR notation.
Example:
> 10.0.0.0/16
> 10.0.0.0 – 10.0.255.255
This means your VPC has 65,536 private IP addresses.

- **Subnets**
A subnet divides the VPC into smaller networks.
Example:
```
VPC: 10.0.0.0/16
Subnet 1 (Public)  : 10.0.1.0/24
Subnet 2 (Private) : 10.0.2.0/24
Subnet 3 (Private) : 10.0.3.0/24
```
