<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---
- [Introduction](#introduction)
- [Amazon S3 Security](#amazon-s3-security)
  - [S3 Encryption](#s3-encryption)
  - [S3 Default Encryption](#s3-default-encryption)
- [Cross-Origin Resource Sharing (CORS)](#cross-origin-resource-sharing-cors)
- [Multi-Factor Authentication (MFA) Delete](#multi-factor-authentication-mfa-delete)
- [Access Logs](#access-logs)
- [Presigned URLs](#presigned-urls)
- [S3 Access Points](#s3-access-points)
- [S3 Object Lambda](#s3-object-lambda)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- **Amazon S3 (Simple Storage Service)** is a scalable object storage service from AWS, known for its durability, availability, and security.
- It provides a range of features to ensure data security, including encryption, access control, and logging capabilities.
- **Security** in Amazon S3 is a shared responsibility. While AWS secures the infrastructure, customers must configure S3 bucket policies, access controls, and encryption settings to protect their data.

# Amazon S3 Security
## S3 Encryption
- **Encryption** is a critical aspect of securing data stored in Amazon S3. It ensures that the data is protected both in transit and at rest.
  - **Server-Side Encryption (SSE):**
    - Data is encrypted by AWS before it is stored and decrypted when accessed.
    - **SSE-S3:** Uses AES-256 encryption keys managed by AWS.
    - **SSE-KMS:** Uses AWS Key Management Service (KMS) to manage keys, allowing for more granular control and audit logs.
    - **SSE-C:** Customers manage their encryption keys while AWS handles the encryption/decryption process.
  - **Client-Side Encryption (CSE):** Data is encrypted by the client before it is uploaded to S3, providing an additional layer of security.

## S3 Default Encryption
- **Default Encryption** allows you to enforce encryption for all objects stored in a specific bucket without specifying encryption settings at the time of upload.
- By configuring default encryption, you can automatically encrypt every new object using either **SSE-S3** or **SSE-KMS**, ensuring data protection without manual intervention.

# Cross-Origin Resource Sharing (CORS)
- **CORS** configuration in S3 allows you to specify which external domains can access the objects in your bucket.
- It is primarily used for web applications where the client-side code needs to access S3 resources from a different domain.
- The CORS configuration is defined using JSON and can specify allowed HTTP methods (GET, PUT), origins, and headers.

# Multi-Factor Authentication (MFA) Delete
- **MFA Delete** provides an additional layer of security by requiring MFA to delete objects or versions in an S3 bucket.
- It prevents accidental or malicious deletions, ensuring that only authorized users with physical access to an MFA device can perform delete operations.
- To enable MFA Delete, the bucket versioning must be enabled, and it can only be configured via the AWS CLI.

# Access Logs
- **S3 Access Logs** capture detailed information about requests made to an S3 bucket, such as the requester's IP address, operation type, and timestamp.
- These logs can be stored in another S3 bucket and analyzed using tools like **AWS Athena** for security auditing and monitoring purposes.
- Access logs help in tracking access patterns, identifying unauthorized access, and troubleshooting issues.

# Presigned URLs
- **Presigned URLs** provide a secure way to grant temporary access to specific S3 objects without making them publicly accessible.
- They are generated using the AWS SDK or CLI and include a signature that is valid for a specified duration.
- This feature is often used for allowing users to upload or download files without exposing the S3 bucket publicly.

# S3 Access Points
- **S3 Access Points** simplify managing data access for large datasets stored in Amazon S3 by providing custom access configurations for specific use cases.
- Each access point has its own hostname, access policies, and network configurations, making it easier to enforce security requirements at scale.
- Access points can be restricted to specific VPCs, enhancing security by ensuring that only authorized network traffic can access the data.

# S3 Object Lambda
- **S3 Object Lambda** allows you to add custom code to process data as it is retrieved from S3.
- With Object Lambda, you can modify the content of S3 objects on-the-fly, enabling use cases like data transformation, redaction, or formatting without altering the original data stored in the bucket.
- It integrates with AWS Lambda, enabling secure, serverless processing of S3 objects.

# Best Practices
- **Enable Encryption:** Use default encryption to ensure all objects are encrypted automatically.
- **Implement Versioning and MFA Delete:** Protect against accidental deletions by enabling bucket versioning and MFA Delete.
- **Use Access Logs:** Monitor bucket access patterns and detect unauthorized access using access logs.
- **Limit Public Access:** Use S3 Access Points and bucket policies to control access, and avoid making buckets publicly accessible.
- **Secure Data Transfers:** Use HTTPS for secure data transfers and enforce bucket policies to deny unencrypted (HTTP) requests.

# Resources
- [AWS S3 Documentation](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)
- [AWS S3 Security Best Practices](https://docs.aws.amazon.com/AmazonS3/latest/userguide/security-best-practices.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
