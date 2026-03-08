## CloudFront
- [What is Amazon CloudFront](#what-is-amazon-cloudfront)
- [Why CloudFront is Needed](#why-cloudfront-is-needed)
- [Key Components of CloudFront](#key-components-of-cloudfront)
- [How CloudFront Works](#how-cloudfront-works)
- [Types of Content](#types-of-content)
- [Caching](#caching)
- [Time To Live](#time-to-live)
- [Cache Invalidation](#cache-invalidation)
- [CloudFront Security](#cloudfront-security)
- [CloudFront + S3](#cloudfront--s3)
- [CloudFront Edge Functions](#cloudfront-edge-functions)
- [Origin Access Control](#origin-access-control)

### What is Amazon CloudFront

Amazon CloudFront is a Content Delivery Network (CDN) service that delivers content to users with low latency and high transfer speeds.

**Simple Definition**
> CloudFront caches content in global edge locations and delivers it to users from the nearest location.

### Why CloudFront is Needed
Without CDN:
User (India) -> Server (USA)
Problems:
- High latency
- Slow loading
- High server load

With Amazon CloudFront:
User -> Nearest Edge Location -> Origin Server
Result:
- Faster content delivery
- Lower latency
- Reduced server load

### Key Components of CloudFront

**A. Edge Locations**
These are global data centers where content is cached.
Example:
- Delhi
- Mumbai
- London
- Tokyo
- New York

User gets data from the closest edge location.

**B. Origin**
Origin is the source of content.
Examples:
- Amazon Simple Storage Service
- Amazon EC2
- Elastic Load Balancing

**C. Distribution**
A distribution is the CloudFront configuration.
Two types:
- Web distribution → websites
- RTMP distribution → streaming (legacy)

***Today most use web distribution.***

### How CloudFront Works

***Step-by-step flow:***
- 1 User requests file
- 2 Request goes to nearest edge location
- 3 Edge checks cache

***If cached:***
- Edge → User (fast)

***If not cached:***
- Edge → Origin server
- Origin → Edge
- Edge caches response
- Edge → User

This is called cache miss.
Next request becomes cache hit.

### Types of Content

CloudFront can deliver:
- Static Content - (Images, CSS, Javascript, HTML, Videos)
- Dynamic Content - (API responses, Database queries, Login requests)

### Caching

CloudFront stores content in cache.
> Image.jpg cached for 24 hours
Benefits:
- Faster performance
- Less origin load
- Lower cost

### Time To Live

TTL determines how long content stays cached.
Types:
- Minimum TTL
- Default TTL
- Maximum TTL

### Cache Invalidation

Sometimes you update files.
But edge still has old version.
Solution:
> Cache Invalidation

### CloudFront Security

CloudFront adds strong security.

**A. HTTPS**
Uses SSL/TLS encryption.
Certificates managed via:

**B. AWS WAF**
Protects against attacks.
Example:
- SQL injection
- DDoS
- Bots

**C. Signed URLs**
Used for private content.
> User receives temporary access link.

### CloudFront + S3

User -> CloudFront -> S3 Bucket

### CloudFront Edge Functions

CloudFront supports serverless code.
Two options:
- CloudFront Functions - Lightweight functions for: (Header modification, Authentication, URL rewriting)
- Lambda@Edge - Runs Lambda at edge locations. (Authorization, Content customization, Security checks)

### Origin Access Control

Used to secure S3 bucket.
Without it: -> Users can access S3 directly
With OAC: -> Only CloudFront can access S3