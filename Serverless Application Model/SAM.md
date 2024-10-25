<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Key Concepts](#key-concepts)
  - [Templates](#templates)
  - [Supported Resources](#supported-resources)
  - [Intrinsic Functions](#intrinsic-functions)
- [Defining Resources](#defining-resources)
  - [Lambda Functions](#lambda-functions)
  - [API Gateway Integration](#api-gateway-integration)
  - [Event Sources](#event-sources)
  - [DynamoDB Integration](#dynamodb-integration)
- [Deployment and Version Control](#deployment-and-version-control)
  - [SAM CLI](#sam-cli)
  - [Stack Policies](#stack-policies)
- [Best Practices](#best-practices)
- [Resources](#resources)

---

# Introduction
- **AWS Serverless Application Model (AWS SAM)** is an open-source framework used for building serverless applications on AWS.
- Simplifies the process of defining and deploying serverless resources like **Lambda, API Gateway, DynamoDB, and S3**.
- Uses YAML or JSON templates with resources defined in a **simplified syntax** that compiles into CloudFormation.

# Key Concepts
## Templates
- SAM templates are **CloudFormation extensions** with resources, properties, and functions unique to serverless applications.
- The template file is often named `template.yaml` and includes metadata to define the application structure and behavior.

## Supported Resources
- **AWS::Serverless::Function**: Defines a Lambda function with simplified syntax for environment variables, memory, timeouts, etc.
- **AWS::Serverless::Api**: Integrates with API Gateway to expose Lambda as HTTP endpoints.
- **AWS::Serverless::Table**: Simplified resource definition for DynamoDB tables.

## Intrinsic Functions
- SAM supports intrinsic functions like `!Ref`, `!Sub`, and `!GetAtt` for dynamic referencing of resources.
- `!Ref` returns the logical ID of a resource, while `!Sub` allows string substitution, and `!GetAtt` retrieves resource attributes.

# Defining Resources
## Lambda Functions
- **AWS::Serverless::Function**: Defines Lambda, including runtime, handler, memory, and environment variables.
    - Example:
      ```yaml
      Resources:
        MyFunction:
          Type: AWS::Serverless::Function
          Properties:
            Handler: index.handler
            Runtime: nodejs16.x
            MemorySize: 128
            Timeout: 10
            Events:
              ApiEvent:
                Type: Api
                Properties:
                  Path: /endpoint
                  Method: get
      ```

## API Gateway Integration
- API Gateway can be set up directly within the Lambda function resource or as a standalone `AWS::Serverless::Api`.
- **DefinitionUri** allows importing Swagger/OpenAPI files for complex API configurations.

## Event Sources
- SAM supports multiple event sources to trigger Lambda functions, including **S3, DynamoDB Streams, SNS, SQS, CloudWatch Events**, and **API Gateway**.
    - Example for S3 Trigger:
      ```yaml
      Events:
        S3Event:
          Type: S3
          Properties:
            Bucket: !Ref MyBucket
            Events: s3:ObjectCreated:*
      ```

## DynamoDB Integration
- **AWS::Serverless::SimpleTable** simplifies DynamoDB configuration.
- Alternatively, **AWS::DynamoDB::Table** provides full control over settings like read/write capacity.

# Deployment and Version Control
## SAM CLI
- **SAM CLI** allows local development, testing, and deployment of serverless applications.
    - `sam init` initializes a SAM application.
    - `sam build` packages the code with dependencies.
    - `sam deploy` deploys the application to AWS using the template.
- Supports **local testing** of Lambda functions and API Gateway.

## Stack Policies
- **Stack Policies** protect resources from unintended changes during updates.
- Defined at the deployment level, SAM enforces policies to avoid accidental deletions or modifications.

# Best Practices
- **Use Nested Stacks** for large applications to improve modularity.
- **API Gateway Caching** can improve performance and reduce backend load.
- **Enable Version Control** for Lambda functions using `AutoPublishAlias` to manage revisions.
- Monitor with **AWS CloudWatch Metrics and X-Ray** for performance insights.
- **Continuous Integration** with SAM CLI and CodePipeline for automated deployments.

# Resources
- [AWS SAM Documentation](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)