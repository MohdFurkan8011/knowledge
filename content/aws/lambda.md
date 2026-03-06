### Lambda

1. **What AWS Lambda Actually Is**

AWS Lambda is a serverless compute service from Amazon Web Services that lets you run code without managing servers.

Instead of deploying an application to a server (like Amazon EC2), you upload functions that run only when triggered.

***Basic flow:***
Event → Lambda Function → Result

2. **Lambda Architecture**

Typical architecture uses several AWS services together.
Example serverless API:
Client (Web / Mobile)
        ↓
API Gateway
        ↓
Lambda Function
        ↓
DynamoDB / RDS / S3


***Common services used with Lambda:***

- Amazon API Gateway → HTTP APIs
- Amazon S3 → file uploads trigger Lambda
- Amazon DynamoDB → serverless database
- Amazon EventBridge → scheduled jobs
- Amazon SQS → queue processing

3. **Lambda Execution Model**

Lambda is event-driven.
A function runs when triggered by an event source.

Common triggers:

| Trigger            | Example        |
|--------------------|---------------|
| HTTP Request       | API Gateway   |
| File Upload        | S3 upload     |
| Database Change    | DynamoDB stream |
| Queue Message      | SQS           |
| Scheduled Task     | Cron job      |

Example:
| User uploads image → S3 → Lambda → Resize image


Amazon Web Services offers both Amazon EC2 and AWS Lambda, but they solve different problems.

Here’s a clear comparison:

# EC2 vs Lambda

| Feature | EC2 (Elastic Compute Cloud) | Lambda |
|--------|------------------------------|--------|
| Type | Virtual servers | Serverless functions |
| Server Management | You manage OS, updates, scaling | AWS manages everything |
| Execution Model | Long-running applications | Event-driven functions |
| Billing | Pay for running VM (per second/hour) | Pay per request + execution time |
| Startup Time | Always running | Cold start possible |
| Scaling | Manual or auto-scaling groups | Automatic scaling |
| Max Runtime | Unlimited | 15 minutes per execution |
| Use Cases | Web servers, databases, full backend apps | APIs, event processing, automation |


🖥️ EC2 (Traditional Cloud Server)

With Amazon EC2 you get a virtual machine.

***You control***
- OS
- CPU/RAM
- Installed software
- Scaling configuration

***Typical uses***
- Hosting a Spring Boot backend
- Running databases
- Running Docker containers
- Full backend services

***Cost Difference***

***EC2:*** Pay while server is running (even if idle).
***Lambda:*** Pay only when code runs.
***Example:***
1M requests/month → Lambda often cheaper.
Heavy backend running 24/7 → EC2 cheaper.