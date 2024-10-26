<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [How CloudFront Works](#how-cloudfront-works)
  - [Edge Locations](#edge-locations)
  - [Regional Edge Caches](#regional-edge-caches)
- [Distributions](#distributions)
- [Origin Types](#origin-types)
- [CloudFront Caching and TTL](#cloudfront-caching-and-ttl)
  - [Default Cache Behavior](#default-cache-behavior)
  - [Caching Policies](#caching-policies)
- [Security in CloudFront](#security-in-cloudfront)
  - [Field-Level Encryption](#field-level-encryption)
  - [Origin Access Control (OAC)](#origin-access-control-oac)
  - [AWS Shield and WAF Integration](#aws-shield-and-waf-integration)
- [Monitoring CloudFront](#monitoring-cloudfront)
- [Invalidations](#invalidations)
- [CloudFront Best Practices](#cloudfront-best-practices)
- [Resources](#resources)

# Introduction
- [Amazon CloudFront](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html) is a fast content delivery network (CDN) service that securely delivers data, videos, applications, and APIs to customers globally with low latency and high transfer speeds.
- CloudFront improves the performance of websites and applications by caching copies of your content at locations near the users, reducing latency and server load.
- CloudFront works with AWS services like **S3**, **EC2**, **Elastic Load Balancing**, and **AWS Lambda**, but can also integrate with non-AWS origins.

# How CloudFront Works
## Edge Locations
- CloudFront delivers content through a global network of **Edge Locations**, which are geographically distributed to bring content closer to the users.
- Users accessing content are routed to the nearest Edge Location to minimize latency.
- **Content Delivery Flow**:
  1. The user makes a request for content.
  2. CloudFront checks if the content is cached at the nearest Edge Location.
  3. If cached, it delivers the content from the edge.
  4. If not cached, CloudFront retrieves content from the **origin** and caches it at the edge.

## Regional Edge Caches
- These are larger caches located between the origin and the Edge Locations to cache content with longer TTLs (Time to Live) and reduce the number of origin fetches.
- Regional Edge Caches improve the efficiency of caching by extending content retention and serving content to Edge Locations from a regional cache.

# Distributions
- A **Distribution** is the blueprint for configuring how CloudFront will serve your content, including defining the content origin and how it is cached at Edge Locations.
- CloudFront supports two types of distributions:
  - **Web Distributions**: For HTTP and HTTPS protocols, commonly used for web applications, APIs, and media streaming.
  - **RTMP Distributions** (deprecated): Previously used for streaming media over Adobe Real-Time Messaging Protocol.

# Origin Types
- CloudFront can serve content from a variety of origins:
  - **S3 Buckets**: Ideal for static content like HTML, CSS, images, and videos.
  - **Custom Origins (EC2, ELB, etc.)**: Useful for dynamic content, such as API responses or web applications hosted on EC2 or behind an Elastic Load Balancer.
  - **Media Services**: CloudFront can be used to serve video content from AWS Elemental MediaPackage, MediaStore, or third-party media servers.

# CloudFront Caching and TTL
## Default Cache Behavior
- CloudFront caches content based on the **TTL (Time to Live)** values specified by the origin or the default TTL settings.
- Content is cached at Edge Locations, and any subsequent requests within the TTL are served from the edge, reducing load on the origin server.
- **TTL Settings**:
  - **Minimum TTL**: The shortest time an object can be cached before being checked for freshness.
  - **Maximum TTL**: The longest time an object can remain in cache without checking the origin for updates.
  - **Default TTL**: The time CloudFront caches content when no explicit headers are present.

## Caching Policies
- **Cache Control Headers**: You can control how CloudFront caches content using Cache-Control headers from the origin.
  - Example: `Cache-Control: max-age=60` caches the content for 60 seconds.
- **Custom Cache Policies**: Allow you to configure more granular caching behavior by specifying what to cache and how long to cache it, including HTTP headers and query string parameters.

# Security in CloudFront
## Field-Level Encryption
- CloudFront provides [Field-Level Encryption](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/field-level-encryption.html) to encrypt sensitive data, such as personally identifiable information (PII), before forwarding it to your origin servers.
- This adds an additional layer of security to meet stringent data protection requirements, especially for financial or healthcare-related applications.

## Origin Access Control (OAC)
- **OAC** is a feature that restricts access to your S3 buckets or other origins so that only CloudFront can fetch content.
- This ensures that your origin is protected from direct access, and requests are funneled through CloudFront, which provides caching and security controls like SSL termination and encryption in transit.

## AWS Shield and WAF Integration
- **AWS Shield**: CloudFront automatically integrates with AWS Shield Standard to provide basic DDoS protection.
- For more advanced protection, **AWS Shield Advanced** can be enabled.
- **AWS WAF (Web Application Firewall)**: CloudFront integrates seamlessly with WAF to help protect against common web exploits like SQL injection or cross-site scripting (XSS).
  - WAF rules can be defined to block, allow, or monitor (count) requests based on IP addresses, HTTP headers, or request bodies.

# Monitoring CloudFront
- **Amazon CloudWatch** provides detailed metrics for monitoring the performance and usage of CloudFront distributions.
- Metrics like cache hit rate, request counts, error rates, and bandwidth usage are critical for understanding your distribution's efficiency.
- **CloudFront Access Logs**: Enable logging to capture detailed information about every request made to CloudFront distributions, which can be stored in S3 and analyzed for security or performance auditing.

# Invalidations
- CloudFront caches content based on TTL settings, but you can **invalidate** objects to remove them from the cache before the TTL expires.
- Invalidations can be used when content updates are required immediately, like after a new website deployment or changes in static assets.
- Each invalidation request specifies one or more object paths, and charges apply based on the number of invalidations.

# CloudFront Best Practices
- **Use SSL/TLS Certificates**: To ensure secure communication between users and CloudFront, always enable SSL certificates for HTTPS connections.
- **Leverage Geo-Restriction**: Block or allow users from specific geographic locations using CloudFront's geo-restriction features.
- **Optimize Caching**: Fine-tune caching policies for better performance by setting appropriate TTL values based on the content type (static vs dynamic).
- **Monitor Cache Hit Rate**: A higher cache hit ratio improves performance and lowers the cost. Use CloudWatch to track this metric.
- **Version Static Assets**: For better cache management, use versioning for static assets, so updated content is served correctly.

# Resources
- [Amazon CloudFront Documentation](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/Introduction.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
