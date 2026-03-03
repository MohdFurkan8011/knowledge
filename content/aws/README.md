# AWS

- [SNS](#sns)
- [CloudFront](#cloudfront)

### SNS
Amazon Web Services Simple Notification Service (SNS) is a fully managed pub/sub (publish–subscribe) messaging service used to send notifications and messages between distributed systems, microservices, and end users.

***It supports:***
- Application-to-Application (A2A) messaging
- Application-to-Person (A2P) messaging

***Core concept***
#### Topics
A **topic** is a global logical access point where publishers send messages.
**Publishers**
Services or applications that send messages to SNS topics.
Example
- EC2
- S3
- Lamda
- Custom applications

#### Subscribers
Endpoints that receive messages
Supported protocols:
- HTTP / HTTPS
- Email
- SMS
- Lambda
- SQS
- Mobile push notifications

#### Message types

***Standard***
Standard SNS guarantees at-least-once delivery, not exactly-once.
To make sure a message is never lost, SNS may retry delivery — and retries can cause duplicates.
SNS is a distributed, multi-AZ, highly available system.

In distributed systems, there are 3 delivery guarantees:

At most once (may lose message)

At least once (may duplicate)

Exactly once (complex + slower)

SNS Standard chooses:

✅ High availability
✅ High throughput
✅ At-least-once delivery

To achieve this, duplicates are possible.

***Why exactly duplicates happen?***
1. Network failure after delivery
Scenario:
- SNS sends message to SQS/HTTP endpoint
- Subscriber successfully processes it
- ACK response gets lost due to network issue
- SNS assumes failure
- SNS retries delivery

2. Subscriber timeout
- HTTP endpoint does not respond within timeout
- Lambda times out
- Temporary system delay

SNS retries
Even if processing completed internally.

This is why:
***Consumers must be idempotent.***
An operation is idempotent if:
Processing the same message multiple times produces the same result.

***How to handle duplicates properly***
1. Use unique IDs
2. Use database constraints
3. Use of FIFO, if duplicates are unacceptable

***Why does SNS Standard deliver duplicates?***
Because SNS guarantees at-least-once delivery to ensure no message loss. If acknowledgments are lost or subscriber responses timeout, SNS retries delivery, which can result in duplicate messages. Therefore, consumers must implement idempotency.

***FIFO***
FIFO - First-in-first-out
SNS FIFO provides:

✅ Strict ordering

✅ Exactly-once message delivery

✅ Deduplication support

It solves the duplicate + ordering issues of Standard SNS.

***Why FIFO Was Introduced?***

Standard SNS:

At-least-once delivery
Best-effort ordering
Possible duplicates
For financial systems, payments, trading, inventory — this is risky.

***Guarantees Provided by SNS FIFO***
1. ***Exactly-Once Delivery (With Conditions)***
SNS FIFO ensures:
- No duplicate message delivery (within deduplication window)
- Exactly-once to each subscribed FIFO SQS queue

⚠ Important:
Exactly-once guarantee works only if:
- Subscriber is FIFO SQS
- Deduplication ID is used properly

2. ***Strict Ordering***
Messages are delivered in the exact order they are published.
But ordering is enforced within a Message Group, not globally.

#### Core concepts of FIFO
1. Topic naming rule - must end with: .fifo ex. order-events.fifo

2. Message group ID(very important) ex. MessageGroupId
***What it does***
- Ensures ordering within that group
- Each group processes sequentially
- Different groups can process in parallel

3. Message Deduplication ID
- Used to prevent duplicate messages.
You must provide:
MessageDeduplicationId

OR enable:
Content-based deduplication

Deduplication Window
SNS FIFO prevents duplicates within:
5-minute deduplication interval
If same DeduplicationId is sent within 5 minutes → ignored.

Cannot subscribe:
- Standard SQS
- Email
- SMS
- HTTP endpoints

FIFO is mainly for system-to-system communication.

⚡ Throughput Limits

FIFO has lower throughput than Standard.
By default:

300 messages per second per MessageGroup
3000 messages/sec with batching
High throughput mode increases this.

Standard vs FIFO Comparison
| Feature      | Standard                  | FIFO                         |
|--------------|---------------------------|------------------------------|
| Ordering     | Best effort               | Strict (per Message Group)   |
| Duplicate    | Possible                  | Prevented (5-minute window)  |
| Throughput   | Very high                 | Moderate                     |
| Fanout       | Yes                       | Limited (FIFO only targets)  |
| Use case     | Notifications, alerts     | Financial workflows, orders  |

#### SNS Message Structure Types
- Plain String Message
- JSON structured Message
- Raw Message Delivery
By default, SNS wraps the message inside metadata.
Example of default delivery to SQS:

```json
{
  "Type": "Notification",
  "MessageId": "...",
  "TopicArn": "...",
  "Message": "Your actual message"
}
```

If you enable Raw Message Delivery:
Only this is sent:
Your actual message

4. Message Attributes (Very Important)
SNS supports message attributes.
```json
{
  "eventType": "order_placed",
  "priority": "high"
}
```
Why important?

Used for filter policies.
Subscriber filter example:
```json
{
  "eventType": ["order_placed"]
}
```

| Message attributes enable selective message routing without creating multiple topics.

5. SMS Message types 
supports: Trasactional, Promotional SMS, OTP type
***In India***

- DLT registration required
- Sender ID approval needed
- Template pre-approval required

6. Message Filtering types
Exact, prefix match, anything-but, numeric

7. Large Message Handling
SNS limit
- 256 KB per message
If we need larger:

***Common pattern:***
- Store payload in S3
- Send S3 object reference in SNS


### CloudFront

- Cloud frontis a global service
- Amazon cloudfront is a webservices that speeds up distribution of your static and dynamic web content, such as .html, .css, .js and image files to users.
- Cloudfront delivers your content through a worldwide network of data centers called Edge locations.
- When a user request content that you are serving with coludfront, the user is routed(via DNS resolution) to the edge location that provides the lowest latency so that content is delivered with the best performance.
- If the content s already in the edge location with the lowest latency, cloudfront delivers it immediately.
- This dramatically reduces the number of network that your user's request must pass through which improves performance.
- If not, cloudfront retceives it from an amazon s3 bucket or an http/webservers that you have identified as the sorce for the definitive version of your content from origin servers.
- Cloudfront also keeps persistent connection with origin servers so file are fetched from the origin as quickly as possible.

***We can acces Amazon CloudFront in the following ways***
1. AWS management console
2. AWS SDK
3. Cloudfront API
4. AWS command line interface

***Cloudfront edge locations***
- Edge locations are not tied to availability zones or regions
- Amazon coludfront has 216 points of presence - 205 edge location and 11 regional edge caches in 84 cities across 42 countries.

#### Cloudfront Regional Edge cache
- Amazon cloud front has added several regional edge cache location globally at close proximity to your viewers.
- They are located between your origin webserver and the global edge locations that serve content directly to your viewer
- As objects become less popular, individual edge locations may remove these objects to make room for popular content.
- Regional edge cache working as a alternative of origin to reduce the burden of origin.
- Regional edge cache have a large cache width than any individual edge location, so object remains in the cache longer at the nearest regional edge caches.

***Cloudfront regional edge cache working***
- When a viewer makes a request on your website or through your applications, DNS routes the request to the cloud front edge location that can best serve the user's request.
- This location is typically the nearest cloudfront edge location in terms of latency.
- In the edge location, cloudfront checks its cache for the requested files.
- If the files are in the cache, cloudfront returns them to the user.
- If the files are not in the cache, the edge servers go to the nearest regional edge cache to fetch the object.
- Regional edge caches have feature panity with edge locations for eg. a cache invalidation request removes an object from both edge caches and regional edge cache before it expires.
- The next time a viewer request the object, cloudfront returns to the origin to fetch the latest version of the object.
- Proxy method PUT/POST/PATCH/OPTIONS/DELEE go directly to the origin from the edge locations and do not proxy through the regional edge caches.
- Dynamic content as determined at request time, does not flow through origin edge cache, but goes directly to the origin.