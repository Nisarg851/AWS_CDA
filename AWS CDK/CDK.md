<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Setting Up AWS CDK](#setting-up-aws-cdk)
- [Basic Concepts](#basic-concepts)
  - [Stacks](#stacks)
  - [Constructs](#constructs)
  - [App](#app)
- [Language Support](#language-support)
- [Permissions and Policies](#permissions-and-policies)
- [Defining Resources](#defining-resources)
    - [Infrastructure Code Example](#infrastructure-code-example)
    - [Context Variables and Parameters](#context-variables-and-parameters)
- [Environment Configurations](#environment-configurations)
- [Deploying a CDK Stack](#deploying-a-cdk-stack)
  - [CDK Commands](#cdk-commands)
  - [Advanced Deployment Strategies](#advanced-deployment-strategies)
- [Testing and Troubleshooting](#testing-and-troubleshooting)
  - [Validation and Debugging](#validation-and-debugging)
- [Best Practices](#best-practices)
- [Resources](#resources)

---

# Introduction
- The **AWS Cloud Development Kit (CDK)** allows defining AWS infrastructure using familiar programming languages, translating to CloudFormation templates.
- **Main Advantages**: Offers reusable constructs, manages dependencies, and supports higher-level abstractions for easier resource management.

# Setting Up AWS CDK
1. **Install Node.js** (required for AWS CDK CLI).
2. **Install AWS CDK CLI**: `npm install -g aws-cdk`.
3. **Verify installation**: `cdk --version`.
4. **Initialize Project**: Run `cdk init app --language <language>` to initialize the CDK app.

# Basic Concepts
## Stacks
- **Stacks** represent a logical grouping of resources for deployment, with each stack mapping to a CloudFormation stack in AWS.

## Constructs
- **Constructs** are reusable, composable components that represent AWS resources or patterns.
  - **L1 (Low-Level)**: Wraps CloudFormation resources directly.
  - **L2 (Higher-Level)**: Provides simplified interfaces for commonly used AWS resources.
  - **L3**: Encapsulates multiple L2 constructs to create complex solutions (e.g., fully configured VPC).

## App
- **App**: The root-level construct that contains one or more stacks, defining the complete infrastructure as code.

# Language Support
- CDK supports **TypeScript**, **JavaScript**, **Python**, **Java**, and **.NET**.
- Choose a language best suited to your workflow and familiarity.

# Permissions and Policies
- **IAM Roles** and **Policies** can be managed in CDK by defining permissions programmatically.
- **Managed Policies**: AWS-managed policies can be attached directly to resources.
- **Custom Policies**: Define custom permissions inline or as standalone policies.

# Defining Resources
- Resources are created using constructs, which wrap AWS services as code.
  
### Infrastructure Code Example
```typescript
import * as cdk from '@aws-cdk/core';
import * as s3 from '@aws-cdk/aws-s3';

export class MyS3Stack extends cdk.Stack {
  constructor(scope: cdk.Construct, id: string, props?: cdk.StackProps) {
    super(scope, id, props);

    new s3.Bucket(this, 'MyBucket', {
      versioned: true,
      removalPolicy: cdk.RemovalPolicy.DESTROY, // Automatically delete bucket when stack is deleted
    });
  }
}
```

### Context Variables and Parameters
- **Context Variables**: Allow passing configuration values into the CDK app, accessible using `cdk.context`.
- **Example**:
  ```typescript
  const bucketName = this.node.tryGetContext("bucketName");
  ```
- **Parameters**: Define input values that are determined at deploy time, adding flexibility across environments.
  ```typescript
  new cdk.CfnParameter(this, 'BucketName', { type: 'String', description: 'Name of the S3 Bucket' });
  ```

# Environment Configurations
- Environment configurations in CDK specify deployment environments (regions, account IDs).
  - **Cross-Environment Deployments**: Allows deploying resources across multiple accounts and regions.
  - **Example**:
    ```typescript
    const envUSA = { account: '123456789012', region: 'us-west-2' };
    new MyStack(app, 'MyStack', { env: envUSA });
    ```

# Deploying a CDK Stack
## CDK Commands
1. **Bootstrapping**: Run `cdk bootstrap` to set up AWS environment (only needed once per environment).
2. **Synthesize Template**: `cdk synth` generates CloudFormation template.
3. **Deploy Stack**: `cdk deploy` deploys resources defined in the stack.
4. **Destroy Stack**: Run `cdk destroy` to delete all stack resources.

## Advanced Deployment Strategies
- **Nested Stacks**: Use for complex projects, where stacks depend on other stacks.
- **Cross-Account Deployment**: Specify multiple environments within the same app, supported via permissions and configuration.

# Testing and Troubleshooting
## Validation and Debugging
- **Environment Variables**: Use variables to configure sensitive values and resources that differ across environments.
- **Testing Commands**:
  - **`cdk diff`**: Shows differences between deployed and local stack configuration.
  - **`cdk doctor`**: Troubleshoots setup issues.

# Best Practices
- **Organize Constructs**: Use modular constructs for improved readability and reusability.
- **IAM Policies**: Follow least privilege principle for defining roles and permissions.
- **Secrets and Configuration**: Use **AWS Secrets Manager** or **SSM Parameter Store** for secure data handling.
- **Use L2 Constructs**: Start with L2 constructs for simplified, managed configurations; opt for L1 when fine-grained control is needed.
- **Testing**: Use `cdk synth` and `cdk diff` for validating changes before deployment.
- **Cross-Account Permissions**: Clearly define permissions when deploying resources across accounts.

# Resources
- [AWS CDK Documentation](https://docs.aws.amazon.com/cdk/latest/guide/home.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)