<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [CloudFormation Concepts](#cloudformation-concepts)
  - [Templates](#templates)
  - [Stacks](#stacks)
  - [Change Sets](#change-sets)
- [CloudFormation Components](#cloudformation-components)
  - [Resources](#resources)
  - [Parameters](#parameters)
  - [Mappings](#mappings)
  - [Outputs](#outputs)
- [Stack Operations](#stack-operations)
- [Security and Permissions](#security-and-permissions)
- [Best Practices](#best-practices)
- [Resources](#resources-1)

# Introduction
- [AWS CloudFormation](https://docs.aws.amazon.com/cloudformation/latest/UserGuide/Welcome.html) is an Infrastructure as Code (IaC) service, enabling automation of AWS infrastructure deployment through JSON or YAML templates.
- CloudFormation supports multi-region deployment, which allows for global consistency of infrastructure.
- **Core Idea:** Define your infrastructure as a code template, deploy it as a stack, and manage changes safely over time.

# CloudFormation Concepts
## Templates
- Templates are JSON or YAML files containing the blueprint of AWS resources to be provisioned. 
- Each template includes a set of components: resources, parameters, mappings, conditions, and outputs.

## Stacks
- A stack is a collection of AWS resources managed as a single unit, deployed from a CloudFormation template.
- Updating a stack enables modifying or deleting resources in a controlled way without disrupting others.

## Change Sets
- Change Sets allow for review of changes before implementing them, reducing the risk of unintended modifications.

# CloudFormation Components
## Resources
- Define AWS resources to be created or modified (e.g., EC2 instances, S3 buckets).
- **Example**: 
  ```yaml
  Resources:
    MyBucket:
      Type: "AWS::S3::Bucket"
      Properties:
        BucketName: "example-bucket"
  ```

## Parameters
- Allow dynamic values to be passed into the template for customization.
- Example usage: specify instance types or environment variables.

## Mappings
- Static values used to customize templates, such as region-specific AMI IDs.
- **Example**:
  ```yaml
  Mappings:
    RegionMap:
      us-east-1:
        "HVM64": "ami-0ff8a91507f77f867"
  ```

## Outputs
- Export information about resources within the stack, such as URLs or instance IDs.

# Stack Operations
- **Create Stack**: Deploys resources based on the template.
- **Update Stack**: Modifies resources while maintaining dependencies and minimal disruption.
- **Delete Stack**: Removes resources and releases associated costs.

# Security and Permissions
- IAM roles and policies manage who can create, update, or delete CloudFormation stacks.
- Cross-account access can be achieved using service roles with proper permissions.

# Best Practices
- Use parameters and mappings to avoid hard-coding values.
- Implement Change Sets to preview updates before applying them.
- Organize templates by environment (e.g., dev, test, prod) to isolate resources and permissions.
- Use Outputs for inter-stack communication by exporting resource values.

# Resources
- [AWS CloudFormation Documentation](https://docs.aws.amazon.com/cloudformation/index.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)