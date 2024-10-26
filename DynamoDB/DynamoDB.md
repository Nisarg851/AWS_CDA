<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Core Concepts](#core-concepts)
  - [Tables and Items](#tables-and-items)
  - [Primary Keys](#primary-keys)
  - [Indexes](#indexes)
- [Data Management](#data-management)
  - [Provisioned and On-Demand Capacity](#provisioned-and-on-demand-capacity)
  - [Read/Write Units](#readwrite-units)
    - [Read Capacity Units (RCUs)](#read-capacity-units-rcus)
    - [Write Capacity Units (WCUs)](#write-capacity-units-wcus)
- [Advanced Features](#advanced-features)
  - [Streams](#streams)
  - [Transactions](#transactions)
  - [Time-to-Live (TTL)](#time-to-live-ttl)
- [Security and Access Control](#security-and-access-control)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- **DynamoDB** is a fully managed NoSQL database service for storing and retrieving data at any scale.
- Supports **Key-Value** and **Document** data models.
- Commonly used for high-scale applications needing low-latency access.

# Core Concepts
## Tables and Items
- **Table**: A collection of items.
- **Item**: A single data record in a table (up to 400 KB).
- **Attributes**: Key-value pairs in an item, can be of various data types.

## Primary Keys
- **Partition Key**: The unique primary key that determines the item’s partition.
- **Composite Key**: Consists of a **Partition Key** and **Sort Key** for more precise data retrieval.

## Indexes
- **Global Secondary Index (GSI)**: Has a different partition and/or sort key; supports additional query patterns.
- **Local Secondary Index (LSI)**: Uses the same partition key as the main table but a different sort key; allows additional sorting on queries.

# Data Management
## Provisioned and On-Demand Capacity
- **Provisioned Capacity**: Manually define read/write capacity units; cost-effective for predictable traffic.
- **On-Demand Capacity**: Auto-scales for unpredictable workloads; charges based on usage.

## Read/Write Units
### Read Capacity Units (RCUs)
1. **Strongly Consistent Reads**: 
   \[
   \text{RCUs required} = \left(\frac{\text{Item Size (KB)}}{4}\right) \times 1
   \]
   For every 4 KB, 1 RCU is needed.

2. **Eventually Consistent Reads**: 
   \[
   \text{RCUs required} = \left(\frac{\text{Item Size (KB)}}{4}\right) \times 0.5
   \]
   Every 4 KB requires 0.5 RCUs.

### Write Capacity Units (WCUs)
- **Write Operations**: 
  \[
  \text{WCUs required} = \left(\frac{\text{Item Size (KB)}}{1}\right)
  \]
  For every 1 KB, 1 WCU is needed.

# Advanced Features
## Streams
- **DynamoDB Streams**: Tracks data changes in real-time, useful for triggering Lambda functions or data pipelines.

## Transactions
- **Transactional Reads** (both `GetItem` and `BatchGetItem`) **require twice the standard RCUs** to ensure consistency.

  - **Transactional Write** operations (e.g., `PutItem`, `UpdateItem`, `DeleteItem`) **require twice the standard WCUs** per 1 KB.

## Time-to-Live (TTL)
- **TTL**: Automatically deletes expired items; useful for managing ephemeral data.

# Security and Access Control
- **IAM Policies**: Control access to tables, indexes, and items.
- **VPC Endpoint**: Access DynamoDB privately without internet routing.
- **Encryption**: Data is encrypted at rest using AWS managed keys by default.

# Best Practices
- Use **Indexes** to optimize query patterns, but limit to necessary attributes to reduce costs.
- Choose **Partition Keys** wisely to avoid “hot partitions” and ensure even workload distribution.
- For **Provisioned Capacity**, enable **Auto Scaling** to adapt to changing demands.

# Resources
- [AWS DynamoDB Documentation](https://docs.aws.amazon.com/dynamodb/index.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)