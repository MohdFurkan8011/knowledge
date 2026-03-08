## Lambda

- [What AWS Lambda Actually Is](#what-aws-lambda-actually-is)
- [Lambda Architecture](#lambda-architecture)
- [Lambda Execution Model](#lambda-execution-model)
- [Lambda Lifecycle](#lambda-lifecycle)
- [Lambda Limits](#lambda-limits)
- [Lambda Scaling](#lambda-scaling)
- [Lambda Pricing](#lambda-pricing)
- [Lambda Function Structure](#lambda-function-structure)
- [Supported Languages](#supported-languages)
- [Lambda Deployment Methods](#lambda-deployment-methods)
- [Lambda Use Cases](#lambda-use-cases)
- [When NOT to Use Lambda](#when-not-to-use-lambda)
- [EC2 vs Lambda](#ec2-vs-lambda)
- [Spring Cloud Function](#spring-cloud-function)

### What AWS Lambda Actually Is

AWS Lambda is a serverless compute service from Amazon Web Services that lets you run code without managing servers.

Instead of deploying an application to a server (like Amazon EC2), you upload functions that run only when triggered.

***Basic flow:***
Event → Lambda Function → Result


### Lambda Architecture

Typical architecture uses several AWS services together.

Example serverless API:

Client (Web / Mobile)<br>
        ↓
API Gateway<br>
        ↓
Lambda Function<br>
        ↓
DynamoDB / RDS / S3


***Common services used with Lambda:***

- Amazon API Gateway → HTTP APIs
- Amazon S3 → file uploads trigger Lambda
- Amazon DynamoDB → serverless database
- Amazon EventBridge → scheduled jobs
- Amazon SQS → queue processing


### Lambda Execution Model

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
> User uploads image → S3 → Lambda → Resize image

Amazon Web Services offers both Amazon EC2 and AWS Lambda, but they solve different problems.


### Lambda Lifecycle

Execution lifecycle:
- Request arrives
- Lambda container created
- Code initialized
- Handler executed
- Response returned

***Cold Start***
When Lambda runs for the first time.

***Warm Start***
When container already exists.


### Lambda Limits

| Limit                 | Value            |
|-----------------------|------------------|
| Max runtime           | 15 minutes       |
| Memory                | 128 MB – 10 GB   |
| Deployment package    | 50 MB (zip)      |
| Concurrent executions | 1000 default     |
| Ephemeral storage     | 512MB – 10GB     |


### Lambda Scaling

Lambda automatically scales.

Example:<br>
> 1 request → 1 Lambda instance<br> 1000 requests → 1000 Lambda instances

***Each request gets its own isolated container.***
No load balancer needed.


### Lambda Pricing

Pricing is based on:

1. Number of requests
2. Execution time
3. Memory allocated

Example:<br>
Requests: 1M<br>
Execution time: 200 ms<br>
Memory: 512 MB

You pay only when the function runs.

Free tier:
1M requests/month
400,000 GB-seconds compute


### Lambda Function Structure

Example Java Lambda handler:

```java
public class HelloHandler implements RequestHandler<Map<String,String>, String> {

    @Override
    public String handleRequest(Map<String,String> event, Context context) {
        return "Hello " + event.get("name");
    }
}
```

### Supported Languages

Lambda supports:
- Java
- Python
- Node.js
- Go
- .NET
- Ruby


### Lambda Deployment Methods

You can deploy using:
1. ZIP upload
2. Docker container
3. Infrastructure as Code


### Lambda Use Cases
- API Backends
- File Processing
- Scheduled Jobs
- Stream Processing

### When NOT to Use Lambda

Avoid Lambda for:<br>
❌ Long-running tasks (>15 minutes)<br>
❌ Heavy CPU workloads<br>
❌ Large monolithic apps<br>
❌ Applications needing persistent connections

In those cases use:
- Amazon EC2
- Amazon ECS
- Amazon EKS

✅ Since you are already a Java/Spring developer, the most important advanced topic for you is:

Spring Boot on Lambda
Using: Spring Cloud Function

This allows running Spring apps as Lambda functions.


Here’s a clear comparison:

### EC2 vs Lambda

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
***Lambda:*** Pay only when code runs.<br>
***Example:***
- 1M requests/month → Lambda often cheaper.
- Heavy backend running 24/7 → EC2 cheaper.

### Spring Cloud Function

```java

<dependencies>

    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-function-context</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-function-adapter-aws</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>

    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
    </dependency>

</dependencies>

```

```java
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private String email;

}
```

```java
public interface UserRepository extends JpaRepository<User, Long> {
}
```

```java
@Component
public class UserFunction {

    @Autowired
    private UserRepository userRepository;

    @Bean
    public Function<User, User> saveUser() {
        return user -> userRepository.save(user);
    }
}
```

```java
public class LambdaHandler extends SpringBootRequestHandler<User, User> {
}
```

```java
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.hibernate.ddl-auto=update
```