<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---
- [Introduction](#introduction)
- [S3 Lifecycle Rules with Analytics](#s3-lifecycle-rules-with-analytics)
    - [How to Implement](#how-to-implement)
- [S3 Event Notifications](#s3-event-notifications)
    - [Event Types:](#event-types)
    - [Use Case Example:](#use-case-example)
- [S3 Performance](#s3-performance)
    - [Best Practices:](#best-practices)
- [S3 Select and Glacier Select](#s3-select-and-glacier-select)
    - [How to Use:](#how-to-use)
    - [Use Case Example:](#use-case-example-1)
- [S3 Object Tags and Metadata](#s3-object-tags-and-metadata)
    - [Use Case Example:](#use-case-example-2)
- [Best Practices](#best-practices-1)
- [Resources](#resources)

# Introduction
- Amazon Simple Storage Service (S3) is an object storage service provided by AWS that offers industry-leading scalability, data availability, security, and performance.
- S3 is designed for 99.999999999% (11 9's) of durability, making it a reliable solution for storing critical data.
- It offers advanced features like lifecycle management, event notifications, data retrieval options, and tagging, allowing users to optimize cost, performance, and security.

# S3 Lifecycle Rules with Analytics
- **Lifecycle Rules:** 
  - Allow users to automate the transition of objects between different S3 storage classes, such as moving infrequently accessed objects to S3 Glacier or deleting outdated objects to save costs.
  - Example: A rule might transition objects older than 30 days to S3 Standard-IA (Infrequent Access) and delete them after a year.

- **S3 Storage Class Analysis:**
  - Provides insights into access patterns of objects, helping users decide when to transition objects to more cost-effective storage classes.
  - Users can configure lifecycle rules based on this analysis to automate data movement, optimizing storage costs.

### How to Implement
1. Enable **S3 Storage Class Analysis** on the bucket to monitor access patterns.
2. Configure a **Lifecycle Policy** based on the analysis results to transition or delete objects.

- **Use Case Example:** Storing logs that are frequently accessed in the first month and rarely after that. Set a rule to move these logs to S3 Glacier after 30 days.

# S3 Event Notifications
- **Overview:** 
  - S3 Event Notifications allow users to automatically trigger actions when specific events occur on an S3 bucket, such as object creation or deletion.
  - Supports integration with AWS Lambda, Amazon SQS, and Amazon SNS, enabling various automated workflows.

### Event Types:
  - **s3:ObjectCreated:** Triggered when a new object is created (e.g., PUT, POST).
  - **s3:ObjectRemoved:** Triggered when an object is deleted.
  - **s3:ObjectRestore:** Triggered when an archived object is restored.

### Use Case Example:
- Trigger a Lambda function to process images uploaded to an S3 bucket and create thumbnails automatically.

# S3 Performance
- **Scalability:** 
  - S3 automatically scales to handle high request rates. It can support thousands of PUT and GET requests per second.
- **Optimizing Performance:** 
  - For optimal performance, use **multipart uploads** for large files and **byte-range fetches** for parallel downloads.
  - **Intelligent Request Routing:** S3 can distribute requests across partitions, improving performance. 
  - For high-throughput workloads, consider enabling **S3 Transfer Acceleration**, which uses AWS global edge locations to speed up data transfers.

### Best Practices:
- Use **prefix randomization** to improve performance by avoiding "hot spots" where too many requests are directed to a single prefix.

# S3 Select and Glacier Select
- **S3 Select:** 
  - Allows users to query a subset of data from an S3 object using SQL expressions. This reduces the amount of data transferred and accelerates the retrieval process.
  - Example: Retrieve specific columns from a CSV file stored in S3 without downloading the entire file.

- **Glacier Select:** 
  - Similar to S3 Select but designed for querying archived data in Amazon S3 Glacier. Users can extract data directly from archives without fully restoring the object.

### How to Use:
1. Enable S3 Select on the bucket.
2. Use SQL expressions to query specific data directly from S3.

### Use Case Example:
- Analyzing large log files stored as CSV in S3 to retrieve error entries without downloading the entire file.

# S3 Object Tags and Metadata
- **Object Tags:** 
  - Key-value pairs assigned to S3 objects to categorize and manage data. Tags can be used for access control, lifecycle policies, and cost allocation.
  - Example: Tagging objects with `environment:production` and `project:analytics` for filtering and billing purposes.

- **Metadata:**
  - User-defined metadata provides additional information about objects. It can be used to store descriptive data such as content type, encoding, or any other custom information.
  - **System Metadata** includes properties like object size, last modified date, and ETag.

### Use Case Example:
- Implementing a tagging strategy for cost allocation and lifecycle management. For instance, applying a `delete_after` tag to objects to determine when they should be deleted.

# Best Practices
- Use **Lifecycle Rules** with analytics to optimize storage costs based on data access patterns.
- Enable **Event Notifications** for real-time data processing and automation.
- Utilize **S3 Select** to query large datasets efficiently without full object retrieval.
- Implement **Multipart Uploads** for large files to enhance upload performance and reliability.
- Apply **Tags** strategically for cost allocation, access control, and automation.

# Resources
- [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [AWS S3 Lifecycle Policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/lifecycle-configuration-examples.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
