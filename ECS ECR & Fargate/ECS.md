<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [ECS Cluster](#ecs-cluster)
- [Task Definitions](#task-definitions)
    - [Task Role](#task-role)
    - [Network Modes](#network-modes)
- [Launch Types](#launch-types)
    - [EC2 Launch Type](#ec2-launch-type)
    - [Fargate Launch Type](#fargate-launch-type)
- [Service Types](#service-types)
- [Scaling ECS](#scaling-ecs)
- [ECS Security](#ecs-security)
- [Monitoring ECS](#monitoring-ecs)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- [ECS](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html) stands for Elastic Container Service.
- It is used to run and manage Docker containers on AWS.
- ECS works with two launch types: **EC2** (where you manage instances) and **Fargate** (serverless).
- ECS is regional, but can use multiple Availability Zones (AZs) for high availability.

# ECS Cluster
- A **cluster** is a logical group of services or tasks managed by ECS.
- A cluster can contain both EC2 instances and tasks running on Fargate.

# Task Definitions
- A **Task Definition** is a blueprint for running containers.
- It defines the image, CPU, memory, and networking settings.

### Task Role
- An IAM role that provides secure access to AWS resources for your ECS tasks.

### Network Modes
- **Bridge Mode**: Traditional Docker networking.
- **Host Mode**: Binds directly to the instance’s network.
- **AWS VPC Mode**: Each container gets its own IP address within your VPC (recommended).

# Launch Types
### EC2 Launch Type
- You manage EC2 instances in the cluster.
- You are responsible for scaling, patching, and securing instances.

### Fargate Launch Type
- Fargate is a serverless compute engine.
- No need to manage infrastructure; AWS handles scaling and management for you.

# Service Types
- **Replica Service**: Ensures the defined number of task copies are running.
- **Daemon Service**: Runs exactly one task on each instance (good for tasks like logging or monitoring).

# Scaling ECS
- **Horizontal Scaling**: Increases or decreases the number of running tasks based on demand.
- **Vertical Scaling**: Increases or decreases the resources (CPU/memory) allocated to tasks.

# ECS Security
- ECS integrates with **IAM** for task roles and service access.
- Use **Security Groups** for network-level security.
- Encrypt data with **AWS KMS** for sensitive information.

# Monitoring ECS
- ECS works with **CloudWatch** for logs and performance metrics.
- **CloudTrail** helps track API calls and user activity.

# Best Practices
- Use **Fargate** to avoid managing infrastructure unless specific EC2 control is needed.
- Set up **Auto Scaling** for traffic spikes.
- Use **IAM Roles** for access instead of embedding credentials in containers.
- Monitor and audit with **CloudWatch** and **CloudTrail**.

# Resources
- [AWS ECS Docs](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)