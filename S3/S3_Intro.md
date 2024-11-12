<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---
- [Introduction](#introduction)
- [S3 Bucket Policy](#s3-bucket-policy)
- [S3 Website Overview](#s3-website-overview)
- [S3 Versioning](#s3-versioning)
- [S3 Replication](#s3-replication)
- [S3 Storage Classes Overview](#s3-storage-classes-overview)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- **Amazon S3 (Simple Storage Service):** Amazon S3 is an object storage service designed to store and retrieve any amount of data from anywhere on the web.
- **Scalability:** S3 is built to handle large-scale data storage needs, providing virtually unlimited storage capacity.
- **Durability and Availability:** S3 offers a durability of 99.999999999% (11 nines) and high availability, making it a reliable choice for storing critical data.
- **Global Reach:** Amazon S3 is a regional service, with data stored in specific regions and replicated across multiple Availability Zones for durability.

# S3 Bucket Policy
- **Bucket Policy:** A bucket policy is a resource-based policy attached to an S3 bucket that defines the permissions for users and services accessing the bucket.
- **Structure:** Bucket policies are JSON documents that specify the actions (e.g., `s3:GetObject`, `s3:PutObject`), resources (bucket or object ARN), and conditions under which the actions are allowed or denied.
- **Access Control:** Bucket policies can be used to manage public access to objects, restrict IP addresses, enforce HTTPS, and more.
- **Example:**
  ```json
  {
      "Version": "2024-11-11",
      "Statement": [
          {
              "Effect": "Allow",
              "Principal": "*",
              "Action": "s3:GetObject",
              "Resource": "arn:aws:s3:::my-bucket/*",
              "Condition": {
                  "IpAddress": {"aws:SourceIp": "192.0.2.0/24"}
              }
          }
      ]
  }
  ```
- **Managed vs. Custom Policies:** AWS provides managed policies for common use cases, but you can also create custom bucket policies based on specific requirements.

# S3 Website Overview
- **Static Website Hosting:** Amazon S3 can be configured to host static websites by serving HTML, CSS, and JavaScript files directly from the bucket.
- **Configuration:** To enable website hosting:
  - Enable "Static Website Hosting" on the bucket settings.
  - Specify the index and error documents (e.g., `index.html` and `error.html`).
- **Endpoint:** The website is accessible via an endpoint in the format: `http://<bucket-name>.s3-website-<region>.amazonaws.com`.
- **Use Cases:** S3 static website hosting is ideal for blogs, portfolios, and other static content without server-side logic.

# S3 Versioning
- **Purpose:** Versioning in S3 allows you to keep multiple versions of an object in the same bucket, helping to protect against accidental overwrites and deletions.
- **Enabling Versioning:** Versioning can be enabled or suspended on an S3 bucket but cannot be disabled once enabled.
- **How it Works:**
  - Each object version is assigned a unique version ID.
  - When an object is deleted, a "delete marker" is added instead of removing the object permanently.
- **Benefits:**
  - **Data Recovery:** You can easily retrieve and restore previous versions of objects.
  - **Compliance:** Helps in maintaining data integrity and adhering to compliance requirements.
- **Example:** If you upload a file named `report.pdf` multiple times, each version is stored in the bucket with a different version ID.

# S3 Replication
- **Overview:** S3 Replication enables automatic, asynchronous copying of objects across different AWS regions (Cross-Region Replication - CRR) or within the same region (Same-Region Replication - SRR).
- **Use Cases:**
  - **Disaster Recovery:** Replicate data to another region for improved disaster recovery.
  - **Compliance:** Meet regulatory requirements for data storage in specific locations.
  - **Latency Reduction:** Store data closer to users for faster access.
- **Configuration:**
  - Requires enabling versioning on both source and destination buckets.
  - Define a replication rule specifying source bucket, destination bucket, and optional filters (prefix or tag-based).
- **Example Rule:**
  ```json
  {
      "Role": "arn:aws:iam::account-id:role/replication-role",
      "Rules": [
          {
              "Status": "Enabled",
              "Filter": {},
              "Destination": {
                  "Bucket": "arn:aws:s3:::destination-bucket"
              }
          }
      ]
  }
  ```

# S3 Storage Classes Overview
- **Introduction:** S3 offers different storage classes to optimize costs based on data access patterns, durability, and retrieval requirements.
- **Storage Classes:**
  - **S3 Standard:** High durability, availability, and performance for frequently accessed data.
  - **S3 Intelligent-Tiering:** Automatically moves data between two access tiers (frequent and infrequent) based on changing access patterns.
  - **S3 Standard-IA (Infrequent Access):** Lower-cost option for infrequently accessed data, with retrieval charges.
  - **S3 One Zone-IA:** Lower-cost storage for infrequently accessed data stored in a single Availability Zone.
  - **S3 Glacier:** Low-cost archival storage with retrieval times ranging from minutes to hours.
  - **S3 Glacier Deep Archive:** Lowest-cost storage for long-term data archiving, with retrieval times of up to 12 hours.
- **Choosing the Right Class:** Select based on access frequency, retrieval times, and cost requirements. For example, use S3 Standard for high-access data and S3 Glacier for archived data.

# Best Practices
- **Enable Versioning:** Helps in recovering from accidental deletes and maintaining data integrity.
- **Use Bucket Policies Wisely:** Restrict access using least privilege principles and implement IAM roles for secure access management.
- **Implement Replication for Disaster Recovery:** Set up CRR or SRR based on business continuity needs.
- **Leverage S3 Storage Classes:** Analyze data access patterns to choose the appropriate storage class and reduce costs.
- **Secure Data with Encryption:** Use server-side encryption (SSE-S3, SSE-KMS) to protect data at rest.

# Resources
- [AWS S3 Documentation](https://docs.aws.amazon.com/s3/index.html)
- [AWS S3 Best Practices](https://aws.amazon.com/s3/best-practices/)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
- 
