<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [ECS Architecture](#ecs-architecture)
    - [Key Components:](#key-components)
- [Key Features](#key-features)
- [Task Definitions](#task-definitions)
    - [Example Task Definition:](#example-task-definition)
- [Clusters](#clusters)
    - [Cluster Types:](#cluster-types)
- [Services](#services)
    - [Service Types:](#service-types)
- [ECS Launch Types](#ecs-launch-types)
- [Networking Modes](#networking-modes)
- [Scaling](#scaling)
    - [Scaling Strategies:](#scaling-strategies)
- [Monitoring and Logging](#monitoring-and-logging)
    - [CloudWatch Integration:](#cloudwatch-integration)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- [Amazon Elastic Container Service (ECS)](https://docs.aws.amazon.com/AmazonECS/latest/userguide/what-is-ecs.html) is a fully managed container orchestration service that enables you to run and manage Docker containers at scale.
- ECS is designed for high availability and integrates seamlessly with other AWS services, allowing you to build robust microservices architectures.

# ECS Architecture
- ECS architecture consists of two primary components:
  - **Clusters**: A logical grouping of tasks or services.
  - **Tasks**: A single running instance of a task definition, which is the blueprint for your application.

### Key Components:
- **Task Definitions**: Specify the Docker image, CPU, memory, and network settings for your containers.
- **Service**: Ensures that a specified number of tasks are always running and can load balance traffic between them.

# Key Features
- **Fully Managed**: ECS handles the orchestration and management of containers, allowing developers to focus on building applications.
- **Integration with AWS Services**: Works well with other AWS services like Elastic Load Balancing, IAM, CloudWatch, and more.
- **Task Scheduling**: Offers different scheduling strategies to optimize resource utilization and minimize costs.
- **Security**: Supports IAM roles for tasks, enabling secure access to other AWS services.

# Task Definitions
- A **Task Definition** is a JSON file that describes one or more containers that form your application.
- It specifies:
  - The Docker image to use.
  - Required CPU and memory.
  - Port mappings and environment variables.
  - Networking and IAM roles.

### Example Task Definition:
```json
{
  "family": "my-task",
  "containerDefinitions": [
    {
      "name": "my-container",
      "image": "my-image:latest",
      "memory": 512,
      "cpu": 256,
      "essential": true,
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80
        }
      ]
    }
  ]
}
```

# Clusters
- An **ECS Cluster** is a logical grouping of tasks or services.
- Clusters can consist of either:
  - **EC2 Instances**: Managed directly by ECS.
  - **Fargate**: Serverless compute engine for running containers without managing servers.

### Cluster Types:
- **EC2 Launch Type**: You manage the EC2 instances that run your containers.
- **Fargate Launch Type**: You don’t need to provision or manage servers; you define and run your containers without having to worry about the underlying infrastructure.

# Services
- An **ECS Service** is used to run and maintain a specified number of instances of a task definition simultaneously.
- Services can be configured with load balancers and auto-scaling policies to handle varying loads.

### Service Types:
- **Replica Service**: Maintains a specified number of tasks.
- **Daemon Service**: Runs one task on each available container instance.

# ECS Launch Types
- **EC2 Launch Type**: Requires provisioning and managing EC2 instances. Suitable for applications needing fine-grained control over the environment.
- **Fargate Launch Type**: Serverless option, simplifying the container management process. Best for developers focusing on deploying applications without worrying about the infrastructure.

# Networking Modes
- ECS supports different networking modes, including:
  - **Bridge Mode**: The default mode where containers share the host’s network stack.
  - **Host Mode**: Containers use the host's network directly.
  - **AWS VPC Mode**: Assigns a unique private IP address to each container. This is the recommended mode for tasks.

# Scaling
- ECS provides built-in support for scaling applications based on demand.
- **Service Auto Scaling** allows you to automatically adjust the desired count of tasks in your service up or down based on CloudWatch metrics.

### Scaling Strategies:
- **Target Tracking Scaling**: Automatically adjusts based on a specified target value (e.g., CPU utilization).
- **Step Scaling**: Allows you to set specific scaling actions based on CloudWatch alarms.

# Monitoring and Logging
- **Amazon CloudWatch** is used to monitor ECS resources and applications.
- You can track metrics like CPU and memory usage, task counts, and more.
- **Logging** can be configured to send container logs to CloudWatch Logs, enabling easy access and analysis.

### CloudWatch Integration:
- Use CloudWatch Alarms to trigger actions based on metrics and events.

# Best Practices
- Use **IAM Roles** for tasks to grant permissions securely.
- Optimize your task definitions by specifying appropriate resource requirements.
- Regularly review and adjust auto-scaling policies based on application load.
- Implement monitoring and logging to identify and troubleshoot issues quickly.

# Resources
- [AWS ECS Docs](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/Welcome.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)