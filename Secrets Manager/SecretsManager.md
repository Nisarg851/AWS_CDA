<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Core Concepts](#core-concepts)
    - [Secrets and Secret Rotation](#secrets-and-secret-rotation)
    - [Secret Types](#secret-types)
    - [Versioning and Lifecycle](#versioning-and-lifecycle)
- [Setting Up Secrets Manager](#setting-up-secrets-manager)
    - [Creating and Managing Secrets](#creating-and-managing-secrets)
    - [Encryption with KMS](#encryption-with-kms)
- [Accessing Secrets](#accessing-secrets)
- [Integrating with AWS Services](#integrating-with-aws-services)
- [Security and Access Control](#security-and-access-control)
    - [IAM Policies for Secrets Access](#iam-policies-for-secrets-access)
    - [Rotation Policies](#rotation-policies)
- [Monitoring and Auditing](#monitoring-and-auditing)
- [Best Practices](#best-practices)
    - [Enable Automatic Rotation for Supported Services](#enable-automatic-rotation-for-supported-services)
    - [Use Secure Access Patterns](#use-secure-access-patterns)
    - [Organize Secrets with Naming Conventions](#organize-secrets-with-naming-conventions)
    - [Apply Least Privilege Principle](#apply-least-privilege-principle)
    - [Regularly Rotate Non-Managed Secrets](#regularly-rotate-non-managed-secrets)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
    - [Access Denied Errors](#access-denied-errors)
    - [Failed Rotation Attempts](#failed-rotation-attempts)
    - [API Throttling](#api-throttling)
- [Resources](#resources)

---

# Introduction

- **AWS Secrets Manager** is a managed service that allows you to securely store, retrieve, and rotate secrets, such as database credentials, API keys, and tokens.
- It offers automatic secret rotation for supported services, enhancing security and reducing the management burden for credentials and other sensitive information.

# Core Concepts

### Secrets and Secret Rotation
- **Secrets** in AWS Secrets Manager are encrypted strings or key-value pairs used to store sensitive information.
- **Automatic Rotation**: AWS can automatically rotate secrets for supported databases and other resources on a customizable schedule, reducing the need for manual rotation.

### Secret Types
- **Basic Secrets**: Simple strings, like API keys or passwords.
- **Credentials**: Pairs of usernames and passwords for databases or other services.
- **API Tokens**: Used to authenticate requests to third-party services or other AWS resources.

### Versioning and Lifecycle
- Each update to a secret creates a new version, allowing rollback to previous versions if needed.
- Secrets Manager manages the lifecycle of each version, including stages like `AWSCURRENT` for the latest active version and `AWSPREVIOUS` for the previous version.

# Setting Up Secrets Manager

### Creating and Managing Secrets
- Secrets can be created via the AWS Console, CLI, or SDK and can contain a single string or multiple key-value pairs.
- When creating secrets, specify encryption settings and configure automatic rotation, if applicable.

### Encryption with KMS
- All secrets are encrypted at rest with AWS KMS, allowing you to use custom or default KMS keys for managing encryption and decryption permissions.

# Accessing Secrets

- **AWS SDK**: Use AWS SDK or CLI to retrieve secrets programmatically, often within applications or Lambda functions.
- **API Calls**: Use `GetSecretValue` API to access secrets securely in real-time without embedding sensitive data in application code.
- Secrets Manager provides **client-side caching** libraries (e.g., for Java and Python) that reduce API calls by caching secrets locally.

# Integrating with AWS Services

- **AWS Lambda**: Retrieve secrets within Lambda functions to avoid hardcoded credentials and enhance security.
- **Amazon RDS**: Automatically rotate and access database credentials directly within applications using Secrets Manager.
- **AWS ECS**: Use secrets as environment variables for ECS tasks and containers to securely pass sensitive data.

# Security and Access Control

### IAM Policies for Secrets Access
- **Fine-Grained Permissions**: Define granular IAM policies to control access to specific secrets, limiting permissions to only necessary users or roles.
- **Resource Policies**: Attach policies directly to secrets, specifying which AWS accounts, roles, or services can access them.

### Rotation Policies
- Configure rotation policies based on the requirements of the secret, with options for automatic or manual rotation and customizable intervals.
- Custom Lambda functions can be used to rotate secrets for services that AWS does not natively support.

# Monitoring and Auditing

- **AWS CloudTrail**: Logs all access to Secrets Manager, providing a comprehensive audit trail for monitoring changes and access requests.
- **CloudWatch**: Monitor metrics related to Secrets Manager usage, such as API call counts and error rates, to troubleshoot issues and maintain optimal performance.

# Best Practices

### Enable Automatic Rotation for Supported Services
- Use automatic rotation for managed databases and other supported resources to enhance security with minimal maintenance.

### Use Secure Access Patterns
- Access secrets only when needed and avoid hardcoding sensitive data in application code. Use environment variables or runtime retrieval methods instead.

### Organize Secrets with Naming Conventions
- Use a standardized naming convention (e.g., `/prod/db/credentials`) to manage secrets across environments and applications easily.

### Apply Least Privilege Principle
- Define IAM policies that grant only necessary access to secrets. Avoid broad permissions like `secretsmanager:*` where possible.

### Regularly Rotate Non-Managed Secrets
- For services without native rotation support, use custom Lambda functions to manage rotation periodically, ensuring that all sensitive data remains secure.

# Troubleshooting Common Issues

### Access Denied Errors
- Verify that the IAM role or user has the necessary permissions to access the specific secret and KMS key for decryption.

### Failed Rotation Attempts
- Check CloudWatch logs for the Lambda rotation function to identify errors and resolve issues.

### API Throttling
- If accessing secrets frequently, consider using client-side caching to reduce API calls and avoid throttling limits.

---

# Resources

- [AWS Secrets Manager Documentation](https://docs.aws.amazon.com/secretsmanager/latest/userguide/intro.html)
- [AWS Secrets Manager Pricing](https://aws.amazon.com/secrets-manager/pricing/)
- [AWS Security Best Practices for Secrets Management](https://aws.amazon.com/blogs/security/)
- [AWS Secrets Manager API Reference](https://docs.aws.amazon.com/secretsmanager/latest/APIReference/Welcome.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
