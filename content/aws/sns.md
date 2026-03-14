## SNS

- [What is Amazon SNS](#what-is-amazon-sns)
- [Why SNS is Needed](#why-sns-is-needed)
- [Core Components of SNS](#core-components-of-sns)
- [How SNS Works](#how-sns-works)
- [SNS Message Delivery](#sns-message-delivery)
- [Supported Subscriber Types](#supported-subscriber-types)
- [SNS Fan-Out Pattern](#sns-fan-out-pattern)
- [SNS Message Filtering](#sns-message-filtering)
- [Message Size Limit](#message-size-limit)
- [SNS Security](#sns-security)
- [SNS FIFO Topics](#sns-fifo-topics)
- [SNS VS SQS](#sns-vs-sqs)
- [SNS Monitoring](#sns-monitoring)

### What is Amazon SNS

Amazon Simple Notification Service is a fully managed Pub/Sub (publish–subscribe) messaging service used to send messages to multiple subscribers simultaneously.

**Simple Definition**
> SNS allows one service to publish a message, and that message is delivered to many subscribers at the same time.

## Why SNS is Needed

Imagine an order system.
When an order is placed:
- Send email to customer
- Send SMS notification
- Update inventory service
- Send event to analytics service

**Without SNS:**
Order Service
   |----> Email Service
   |----> SMS Service
   |----> Inventory Service
   |----> Analytics Service

Tightly coupled system.

**With Amazon Simple Notification Service:**
```
Order Service
     |
     v
SNS Topic
 |      |      |
Email  SQS   Lambda
```

### Core Components of SNS

- **1. Topic**
   - A topic is a communication channel.
   - Publishers send messages to a topic.

- **2. Publisher**
   Service that sends messages to the topic.
   Examples:
   - AWS Lambda
   - Amazon EC2
   - Applications
   - Microservices

- **3. Subscriber**
   Services that receive the message.
   Example subscribers:
   - Amazon SQS
   - AWS Lambda
   - Email
   - SMS
   - HTTP endpoints

### How SNS Works

Step-by-step:
- 1 Publisher sends message
- 2 Message goes to SNS topic
- 3 SNS pushes message to all subscribers

### SNS Message Delivery

Important concept.
SNS uses push delivery.
1. Publisher → SNS → Subscribers
SNS automatically sends messages to subscribers.
2. SQS → Pull model
3. Consumers poll queue

### Supported Subscriber Types

SNS can deliver messages to many endpoints.
Common ones:
- Amazon SQS
- AWS Lambda
- HTTP / HTTPS endpoints
- Email
- SMS
- Mobile push notifications

### SNS Fan-Out Pattern

Fan-out pattern means:
> One message → many receivers

### SNS Message Filtering

SNS supports message filtering.
```json
{
 "type": "order",
 "region": "india"
}
```

Subscribers can filter messages.
- Queue1 → receives only "order"
- Queue2 → receives only "payment"

### Message Size Limit

SNS message size: -> 256 KB
For larger payloads use: -> Amazon Simple Storage Service - Send S3 reference in SNS message.

### SNS Security

Security features include:
- **1. IAM Policies**
Access control using: - AWS Identity and Access Management

- **2. Encryption**
SNS supports encryption using: - AWS Key Management Service

- **3. Access Control**
You can restrict:
- Which service can publish
- Which service can subscribe

### SNS FIFO Topics

SNS also supports FIFO topics.
Features:
- Strict ordering
- Exactly-once delivery

### SNS VS SQS

| Feature   | SNS       | SQS              |
|-----------|-----------|------------------|
| Model     | Pub/Sub   | Queue            |
| Delivery  | Push      | Pull             |
| Consumers | Many      | Usually one      |
| Ordering  | Not guaranteed | FIFO available |

### SNS Monitoring

Metrics monitored using:
> Amazon CloudWatch