<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Amazon RDS Overview](#amazon-rds-overview)
- [RDS Read Replicas vs Multi-AZ](#rds-read-replicas-vs-multi-az)
- [Amazon Aurora Intro](#amazon-aurora-intro)
- [RDS Aurora Security](#rds-aurora-security)
- [RDS Proxy](#rds-proxy)
- [ElastiCache Overview](#elasticache-overview)
  - [ElastiCache: Memcached](#elasticache-memcached)
  - [ElastiCache: Redis](#elasticache-redis)
  - [Memcached vs Redis](#memcached-vs-redis)
- [ElastiCache Strategies](#elasticache-strategies)
- [Amazon MemoryDB for Redis Overview](#amazon-memorydb-for-redis-overview)
- [Resources](#resources)


# Amazon RDS Overview
- [Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html) stands for Relational Database Service.
- It is a fully managed service that simplifies the process of managing relational databases by automating tasks such as backups, patching, scaling, and replication.
- RDS supports multiple popular database engines, including:
  - MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, and Amazon Aurora.
- It provides important features like:
  - Automated backups for data protection.
  - Snapshots to capture point-in-time database states.
  - Multi-AZ deployments for high availability and disaster recovery.
  - Read replicas to scale out and improve read performance.
- RDS pricing varies based on instance type, storage, and the number of input/output operations (I/O).
- It offers storage options including general-purpose SSD for standard workloads and provisioned IOPS for high-performance requirements.
  
# RDS Read Replicas vs Multi-AZ
- **Read Replicas** are designed to improve read performance by allowing read traffic to be offloaded to replica databases.
  - They can be created in the same region or across regions.
  - Ideal for workloads where the primary database handles writes, and replicas manage heavy read operations.
  - Replicas can be promoted to standalone databases for disaster recovery or migration purposes.
- **Multi-AZ Deployments** focus on high availability and failover.
  - They automatically replicate data to a standby instance in a different Availability Zone (AZ).
  - In case of failure, automatic failover ensures minimal downtime.
  - Primarily suited for production databases that require strong availability guarantees and data protection.

# Amazon Aurora Intro
- [Amazon Aurora](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Overview.html) is a fully managed relational database engine optimized for performance and reliability.
- It is compatible with MySQL and PostgreSQL, offering the same features but delivering up to five times the throughput of standard MySQL or twice the performance of PostgreSQL.
- Aurora provides built-in high availability with up to 15 low-latency read replicas and automatic, continuous backups to Amazon S3.
- It scales automatically, adjusting to your application’s needs without downtime.
- Aurora is ideal for applications that demand enterprise-level performance, scalability, and resilience.
  
# RDS Aurora Security
- Amazon Aurora integrates tightly with [AWS security services](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.html) to ensure robust protection.
- **Encryption**: Aurora supports encryption at rest using AWS Key Management Service (KMS), securing data, backups, snapshots, and replicas.
- **VPC Support**: Aurora instances run inside an Amazon Virtual Private Cloud (VPC), isolating databases within a secure network environment.
- **IAM Integration**: Uses AWS Identity and Access Management (IAM) to control access to database resources.
- **Security Patches**: Aurora automatically applies security patches to your instances to protect against vulnerabilities.
- **SSL/TLS**: Encrypted connections between applications and Aurora instances are supported to prevent unauthorized access during data transmission.

# RDS Proxy
- [Amazon RDS Proxy](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) is a fully managed database proxy service designed to improve application scalability and resilience.
- It efficiently manages connections between your application and the database, preventing resource exhaustion in scenarios with a large number of connections.
- RDS Proxy reduces failover time by preserving application connections during database failovers, ensuring high availability.
- It supports Amazon RDS for MySQL, PostgreSQL, and Aurora databases.
- Ideal for applications with unpredictable workloads or those requiring quick failover times without connection drops.

# ElastiCache Overview
- [Amazon ElastiCache](https://docs.aws.amazon.com/AmazonElastiCache/latest/UserGuide/WhatIs.html) is a fully managed in-memory data store and cache service.
- Supports two popular engines:
  - **Memcached**: Simple key-value store, suitable for caching purposes.
  - **Redis**: More advanced features, including data structures (lists, sets, sorted sets), persistence, and pub/sub capabilities.
- It is designed to improve application performance by retrieving data from fast, managed in-memory caches instead of slower disk-based databases.
- ElastiCache helps reduce the load on your relational or NoSQL databases by caching frequently queried data.
- It also improves application performance by enabling faster data retrieval.

## ElastiCache: Memcached
- Memcached is a simple, high-performance, distributed memory caching system.
- It is ideal for use cases that require storing small, frequently accessed data in a fast, ephemeral cache.
- Supports horizontal scaling by adding or removing nodes.
- Lacks persistence, meaning the cached data is temporary and will be lost during failures or restarts.

## ElastiCache: Redis
- Redis is an advanced, open-source key-value store that supports more complex data structures such as lists, sets, and hashes.
- Redis offers **persistence**, allowing data to survive reboots and system failures.
- Features replication, high availability with Redis Sentinel, and automatic partitioning (sharding).
- Suitable for use cases requiring durable, in-memory caching or real-time applications like leaderboards and messaging systems.

## Memcached vs Redis
- **Memcached**: Lightweight, stateless caching engine, ideal for simple use cases where data persistence isn’t required. Scales easily but offers fewer features.
- **Redis**: More feature-rich with support for complex data types, persistence, and high availability. Recommended for advanced caching, session stores, or applications needing durable storage.
  
| Feature      | Memcached                    | Redis                                     |
| ------------ | ---------------------------- | ----------------------------------------- |
| Architecture | Simple, multi-threaded       | Single-threaded but supports replication  |
| Data types   | Key-value pairs              | Strings, lists, sets, hashes, sorted sets |
| Persistence  | No                           | Yes (with snapshots and AOF)              |
| Use cases    | Basic caching, session store | Advanced caching, analytics, pub/sub      |


# ElastiCache Strategies
- **Lazy Loading**:
  - Data is loaded into the cache only when it’s requested by the application, reducing the initial load on the cache but risking a cache miss.
  - Cache is populated on-demand, reducing unnecessary memory usage.
  - Cache miss penalty applies when the data isn’t in the cache, leading to slower first-time access.
  
- **Write-Through Caching**:
  - Every data write operation is automatically written to both the cache and the underlying database, ensuring the cache is always up-to-date.
  - Ensures the cache always holds the most up-to-date data.
  
- **Cache-aside**:
  - The application directly queries the cache.
  - If the data is not available, it fetches from the database and updates the cache.
  - Reduces unnecessary queries to the database.


# Amazon MemoryDB for Redis Overview
- [Amazon MemoryDB for Redis](https://docs.aws.amazon.com/memorydb/latest/devguide/what-is-memorydb.html) is a Redis-compatible, fully managed in-memory database service designed for ultra-fast, durable data access.
- It is optimized for applications requiring both high-performance caching and durable storage.
- Unlike ElastiCache, MemoryDB stores the entire data set in memory while also writing it to disk for durability, providing the speed of Redis with persistence for mission-critical applications.
- Ideal for scenarios where you need real-time data access with high throughput and durability, such as gaming leaderboards or financial services.

# Resources
- [Amazon RDS Docs](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Welcome.html)
- [Amazon Aurora Docs](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_AuroraOverview.html)
- [Amazon ElastiCache Docs](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/WhatIs.html)
- [MemoryDB Docs](https://docs.aws.amazon.com/memorydb/latest/devguide/Welcome.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
