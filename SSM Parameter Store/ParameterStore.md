<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Core Concepts](#core-concepts)
    - [Parameters and Parameter Types](#parameters-and-parameter-types)
    - [Versioning and Parameter History](#versioning-and-parameter-history)
    - [Parameter Tiers](#parameter-tiers)
- [Setting Up Parameter Store](#setting-up-parameter-store)
    - [Creating Parameters](#creating-parameters)
    - [Parameter Encryption with KMS](#parameter-encryption-with-kms)
- [Accessing Parameters](#accessing-parameters)
- [Integrating with Other AWS Services](#integrating-with-other-aws-services)
- [Security and Access Control](#security-and-access-control)
    - [IAM Policies and Resource-Level Permissions](#iam-policies-and-resource-level-permissions)
    - [Parameter Policies](#parameter-policies)
- [Monitoring and Auditing](#monitoring-and-auditing)
- [Best Practices](#best-practices)
    - [Use SecureString for Sensitive Data](#use-securestring-for-sensitive-data)
    - [Apply Least Privilege Principle](#apply-least-privilege-principle)
    - [Enable Versioning for Configuration Changes](#enable-versioning-for-configuration-changes)
    - [Organize Parameters by Environment and Application](#organize-parameters-by-environment-and-application)
    - [Use Advanced Tier for Large-Scale Applications](#use-advanced-tier-for-large-scale-applications)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)
    - [Access Denied Errors](#access-denied-errors)
    - [Parameter Not Found](#parameter-not-found)
    - [Failed to Decrypt SecureString](#failed-to-decrypt-securestring)
- [Resources](#resources)

---

# Introduction

- **AWS Systems Manager Parameter Store** is a secure, scalable service that provides a centralized repository for storing and managing configuration data, secrets, and secure strings.
- Parameter Store integrates well with other AWS services, such as EC2, Lambda, ECS, and more, for use in applications, automation, and DevOps workflows.

# Core Concepts

### Parameters and Parameter Types
- **Parameters** are configuration items stored as key-value pairs, such as database connection strings, API keys, passwords, or custom application settings.
- **Parameter Types**:
  - **String**: Stores plaintext data.
  - **StringList**: Stores comma-separated list values (e.g., IP addresses).
  - **SecureString**: Encrypts sensitive information using AWS KMS.

### Versioning and Parameter History
- Each parameter is versioned to maintain a history of changes, allowing for rollback to previous versions if needed.
- Each version change is logged, which helps track changes over time for auditing.

### Parameter Tiers
- **Standard**: Limited to 10,000 parameters per account, suitable for most general-purpose configurations.
- **Advanced**: Supports up to 100,000 parameters and higher payload sizes, with features like parameter policies for lifecycle management.
- **Intelligent-Tiering**: Optimizes storage cost based on parameter usage patterns.

# Setting Up Parameter Store

### Creating Parameters
- Parameters can be created through the AWS Console, CLI, SDK, or AWS CloudFormation.
- Define the name, type, and optional description and set any required encryption options.

### Parameter Encryption with KMS
- **SecureString** parameters require encryption, leveraging AWS KMS for key management.
- KMS-managed keys ensure secure handling of sensitive data with fine-grained access control.

# Accessing Parameters

- Parameters can be accessed via the SSM console, AWS CLI, or SDK.
- Parameters are accessed in applications or scripts using `GetParameter` or `GetParameters` API calls, with options to decrypt when fetching SecureString values.
- Parameters can be used in Lambda functions, EC2 user data, and ECS tasks by referencing them directly.

# Integrating with Other AWS Services

- **AWS Lambda**: Retrieve parameters dynamically to avoid hardcoding secrets in the code.
- **AWS EC2**: Store configuration settings and reference them in user data scripts to configure instances on launch.
- **AWS ECS**: Use Parameter Store to pass secrets and configurations to containers at runtime.
- **AWS CloudFormation**: Dynamically reference parameters in stack templates for automated deployments.

# Security and Access Control

### IAM Policies and Resource-Level Permissions
- Define **IAM policies** to control access to parameters, ensuring only authorized users or services can read or write to specific parameters.
- Use **resource-level permissions** to grant granular access to sensitive parameters.

### Parameter Policies
- Parameter policies enforce lifecycle rules for parameters:
  - **Expiration**: Deletes parameters after a specified period.
  - **No Change**: Prevents parameter updates within a specified timeframe.
  - **Notification**: Sends SNS notifications when a parameter approaches expiration.

# Monitoring and Auditing

- **CloudWatch**: Monitor SSM Parameter Store API requests to track usage and potential issues.
- **CloudTrail**: Log all API calls to SSM Parameter Store for auditing changes to parameters.

# Best Practices

### Use SecureString for Sensitive Data
- Encrypt sensitive parameters like passwords and secrets with **SecureString** and **KMS** to ensure data security.

### Apply Least Privilege Principle
- Restrict access to parameters using IAM roles and policies. Avoid granting full access to Parameter Store if only specific parameters are required.

### Enable Versioning for Configuration Changes
- Use versioning to track configuration changes and provide a way to roll back to previous versions if necessary.

### Organize Parameters by Environment and Application
- Use a naming convention to organize parameters (e.g., `/dev/app-name/param-name`) for easier management across multiple environments.

### Use Advanced Tier for Large-Scale Applications
- Advanced parameters are ideal for large-scale applications with a high number of parameters and frequent updates.

# Troubleshooting Common Issues

### Access Denied Errors
- Check IAM policies to ensure the user or role has the necessary permissions for parameter access.

### Parameter Not Found
- Verify the parameter name and ensure the correct path and environment are specified.

### Failed to Decrypt SecureString
- Ensure that the IAM role has decryption permissions for the KMS key associated with the SecureString parameter.

---

# Resources

- [AWS SSM Documentation](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)
- [AWS Parameter Store API Reference](https://docs.aws.amazon.com/systems-manager/latest/APIReference/Welcome.html)
- [SSM Parameter Store Pricing](https://aws.amazon.com/systems-manager/pricing/)
- [AWS Security Blog on Managing Secrets](https://aws.amazon.com/blogs/security/)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
