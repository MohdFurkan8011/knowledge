## AMI - Amazon Machine Image

- [What is an AMI](#what-is-an-ami)
- [How AMI Works](#how-ami-works)
- [Types of AMIs](#types-of-amis)
- [How to Create Your Own AMI](#how-to-create-your-own-ami)
- [How to Launch an Instance From Your AMI](#how-to-launch-an-instance-from-your-ami)

### What is an AMI

An Amazon Machine Image (AMI) is a template used to launch virtual servers in Amazon Elastic Compute Cloud.

It contains everything needed to start an instance:

- 🖥 Operating System (Linux, Windows, etc.)
- 📦 Installed software (Java, Node, Angular, etc.)
- ⚙ Configuration (startup scripts, environment settings)
- 💾 Storage snapshot of the root volume (usually Amazon Elastic Block Store)

Think of an AMI as a snapshot template of a server.
Every time you launch an EC2 instance from it, you get a copy of that server setup.


### How AMI Works

- Create or choose an AMI
- Launch an EC2 instance using the AMI
- AWS creates a virtual machine using that template
- Instance starts with the same OS + software configuration

Example:

AMI contains:

- Ubuntu
- Java 21
- Spring Boot
- Docker

When you launch an instance → it already has ***everything installed***.

### Types of AMIs

- AWS Provided
    Example:
    - Amazon Linux
    - Ubuntu
    - Windows Server

- Marketplace AMIs
    Examples:
    - MongoDB server
    - Kubernetes cluster images
    - Security appliances

- Custom AMIs - Created by you from your configured EC2 instance.
    Example:
    - Java + Spring Boot server
    - Node + Angular build server
    - Docker development environment


### How to Create Your Own AMI

- 1. Launch an EC2 instance
    - Launch Instance
    - Choose OS (Ubuntu/Amazon Linux)
    - Install your software

- 2. Stop the instance (recommended)
    - EC2 → Instance → Stop

- 3. Create Image
    - Select instance
    - Click Actions
    - Select Image and Templates
    - Click Create Image

### How to Launch an Instance From Your AMI

- Go to EC2 → AMIs
- Select your AMI
- Click Launch Instance