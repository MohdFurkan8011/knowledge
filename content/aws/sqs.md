## SQS - Simple Queue Service

- [What is Amazon SQS](#what-is-amazon-sqs)
- [Why SQS is Needed](#why-sqs-is-needed)
- [Core Components of SQS](#core-components-of-sqs)
- [Message Lifecycle](#message-lifecycle)
- [Key Concepts](#key-concepts)
- [Types of SQS Queues](#types-of-sqs-queues)
- [Dead Letter Queue](#dead-letter-queue)
- [SQS Message Size](#sqs-message-size)
- [SQS Integrations](#sqs-integrations)
- [Important](#important)
- [Real World Architecture Example](#real-world-architecture-example)
- [When to Use SQS](#when-to-use-sqs)
- [Internal Architecture of SQS](#internal-architecture-of-sqs)
- [At-Least-Once Delivery](#at-least-once-delivery)
- [Exactly-Once Processing](#exactly-once-processing)
- [Message Group ID](#message-group-id)
- [Throughput Limits](#throughput-limits)
- [Message Delay](#message-delay)

### What is Amazon SQS?

Amazon Simple Queue Service (SQS) is a fully managed message queue service used to decouple applications.

It allows different parts of a system to communicate asynchronously.

Simple Definition
> SQS is a message queue where one service sends messages and another service processes them later.

### 2. Why SQS is Needed

Imagine a web application:

User uploads image → server processes image → stores result.
Without SQS:
> User → Web Server → Image Processing → Database

If image processing is slow:
- Web server becomes slow
- Requests pile up
- System crashes

With SQS:
> User → Web Server → SQS Queue → Worker Server → Database

Now:
- Web server just sends message to queue
- Worker processes later
- System becomes scalable and reliable

### Core Components of SQS

**A. Producer**
Service that sends message to queue
Example:
- Web app
- Lambda
- EC2

**B. Queue**
Temporary storage of messages.
Example:
- Message 1
- Message 2
- Message 3

**C. Consumer**
Service that reads messages and processes them
Example:
- Worker server
- Lambda
- Microservice

### Message Lifecycle

Step by step process:
- 1 Producer sends message
- 2 Message stored in queue
- 3 Consumer polls the queue
- 4 Consumer processes message
- 5 Message deleted from queue

### Key Concepts

**A. Message Retention**
- How long SQS stores a message.
- Range: 1 minute → 14 days
- Default: 4 days
- If message not processed → it stays until retention expires.

**B. Visibility Timeout**
When a consumer reads a message:
The message becomes ***invisible to other consumers temporarily***.

**This prevents duplicate processing.**

**C. Long Polling**
Consumer waits for messages instead of repeatedly asking.
Without Long Polling:
> Consumer → SQS
> No message
> Consumer → SQS
> No message
**Waste of API calls.**

With Long Polling:
> Consumer waits up to 20 seconds
> If message arrives → returned immediately

Benefits:
- Lower cost
- Faster processing
- Less empty responses

### Types of SQS Queues

There are 2 types.

**A. Standard Queue**
Default queue.

Features:
> Unlimited throughput
> Best effort ordering
> At least once delivery - Message may be delivered **more than once**.
> High performance systems

Example:
- Logs
- Image processing
- Data pipelines

**B. FIFO Queue (First In First Out)**
Features:
- Strict message ordering
- Exactly-once processing

Limitations:
- Lower throughput
- Requires Message Group ID

Use cases:
- Banking transactions
- Order processing
- Payment systems

### Dead Letter Queue

If a message fails processing multiple times → it goes to Dead Letter Queue.
Example:
- Worker tries processing message
- Fails
- Retries
- Fails again
- Retries again

After max retries:
- Message moved to DLQ

Benefits:
- Debug failed messages
- Prevent queue blocking

### SQS Message Size

Maximum message size: - 256 KB

If message bigger:
- Amazon Simple Storage Service (S3)
- Store payload in S3 and send S3 link in SQS message.

### SQS Integrations

SQS works with many AWS services.
Common integrations:
- AWS Lambda
- Amazon EC2
- Amazon Simple Notification Service
- AWS Step Functions
- Amazon Simple Storage Service

Example architecture:
> S3 Upload
> SNS Notification
> SQS Queue
> Lambda Worker

### Important

| Feature             | Standard        | FIFO           |
|---------------------|-----------------|---------------|
| Ordering            | Not guaranteed  | Guaranteed     |
| Delivery            | At least once   | Exactly once   |
| Throughput          | Very high       | Lower          |
| Duplicate messages  | Possible        | No             |

### Real World Architecture Example

E-commerce order system:
> User places order
> Order Service
> SQS Queue
> Inventory Service
> Payment Service
> Shipping Service

Benefits:
- Loose coupling
- Fault tolerance
- Scalable microservices

### When to Use SQS

Use SQS when:
- Decouple microservices
- Handle traffic spikes
- Asynchronous processing
- Background jobs
- Task queues

### Internal Architecture of SQS
SQS is a distributed system.

When you send a message to Amazon Simple Queue Service, AWS stores it across multiple servers.
Why?
- High availability
- Fault tolerance
- Durability

Even if one server fails → message still exists.
This is why AWS guarantees -> Durability of messages

### At-Least-Once Delivery

***Standard Queue***
Standard queues guarantee:
> At least once delivery

Meaning:
> A message may be delivered more than once.

Why duplicates happen?
Because SQS replicates messages across servers.
If a server fails while deleting a message:
> Delete succeeded on Node1
> Delete failed on Node2

Node2 may deliver the message again.
So your application must be **idempotent**.

### Exactly-Once Processing

***FIFO queues solve duplication.***
Using **Amazon Simple Queue Service FIFO queue:
> Exactly once processing
> Strict ordering

***How it works internally:***
Deduplication ID
Each message has:
> MessageDeduplicationId

If the same message arrives again within 5 minutes, SQS ignores it.

### Message Group ID
FIFO also uses:
> MessageGroupId

This controls parallel processing.
Example queue:
> Group A → Order1
> Group A → Order2
> Group B → Order3
> Group B → Order4

Processing:
> Worker1 → Group A
> Worker2 → Group B

Ordering guaranteed inside a group.
But different groups run **in parallel**.

### Throughput Limits

**Standard Queue**
> Nearly unlimited throughput
Millions of messages per second.

**FIFO Queue**
Classic FIFO:
> 300 messages/sec
With batching:
> 3000 messages/sec
With High Throughput FIFO:
> 70000 messages/sec

### Message Delay

SQS allows delaying messages.
> Delay = 10 minutes
Producer sends message.
It becomes visible only after: 10 minutes