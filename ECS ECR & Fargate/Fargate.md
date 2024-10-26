<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Fargate Architecture](#fargate-architecture)
- [Fargate vs EC2](#fargate-vs-ec2)
- [Task Definitions](#task-definitions)
- [Networking and Security](#networking-and-security)
    - [Security Best Practices:](#security-best-practices)
- [Scaling and Auto-scaling](#scaling-and-auto-scaling)
    - [Horizontal Scaling:](#horizontal-scaling)
- [Monitoring and Logging](#monitoring-and-logging)
    - [Monitoring Best Practices:](#monitoring-best-practices)
- [Best Practices](#best-practices)
- [Fargate Pricing](#fargate-pricing)
- [Resources](#resources)

# Introduction
- [AWS Fargate](https://docs.aws.amazon.com/AmazonECS/latest/userguide/what-is-fargate.html) is a **serverless compute engine** for containers that runs on **Amazon ECS** and **Amazon EKS**.
- It abstracts away the need to manage infrastructure by allowing developers to run containers without worrying about provisioning or scaling the underlying EC2 instances.
- With Fargate, you can focus entirely on application logic, while AWS manages everything else, including capacity, scaling, and patching.

# Fargate Architecture
- **Fargate** operates with **Amazon ECS** or **EKS** and enables the running of containerized applications directly.
  - No need to manage EC2 instances.
  - Fargate automatically provisions the necessary compute resources for your containers.
  - Each container runs in its own micro-VM for enhanced isolation and security.
- Fargate works with **Task Definitions**, which define how Docker containers should run, specifying the required CPU, memory, networking settings, and other configurations.

# Fargate vs EC2
- Fargate is an alternative to the traditional **EC2 Launch Type** in **Amazon ECS**.
  - **Fargate** is serverless and handles infrastructure management.
  - **EC2** requires you to manage your own EC2 instances, scaling policies, and networking.
  - **Fargate** uses micro-VMs for containers, offering improved isolation and security.
  - **EC2** is better suited for scenarios where you want to control the underlying infrastructure, such as using GPU instances or specific EC2 types.

| Feature               | Fargate                 | EC2 Launch Type        |
|-----------------------|-------------------------|------------------------|
| Instance Management    | Fully managed (Serverless) | Requires instance management |
| Scaling               | Automatic               | Manual (Auto Scaling needed) |
| Pricing Model          | Pay for vCPU and memory | Pay per instance        |
| Security              | Enhanced container isolation | Depends on EC2 settings |

# Task Definitions
- **Task Definitions** in Fargate describe how containers are to be deployed and run.
  - Specify **vCPU**, **Memory**, **Environment Variables**, **Networking Settings**, and **IAM Roles**.
  - Task definitions can define multiple containers running together in the same task (for example, a web server container and a logging container).
  - You can specify resource constraints for each container to ensure that tasks have the necessary CPU and memory allocation.

**Example Task Definition:**
```json
{
  "family": "my-fargate-task",
  "networkMode": "awsvpc",
  "containerDefinitions": [
    {
      "name": "my-container",
      "image": "nginx",
      "cpu": 256,
      "memory": 512,
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp"
        }
      ]
    }
  ],
  "requiresCompatibilities": [
    "FARGATE"
  ],
  "cpu": "256",
  "memory": "512"
}
```

# Networking and Security
- **AWS Fargate** uses **AWS VPC** to provide networking isolation and security.
  - Each task runs within its own dedicated VPC using the **awsvpc** network mode.
  - Tasks receive their own ENI (Elastic Network Interface) with private IP addresses.
  - Use **Security Groups** to control inbound and outbound traffic to Fargate tasks.
  - You can integrate **IAM Roles** at the task level to control access to other AWS services, such as S3 or DynamoDB.

### Security Best Practices:
- Always run Fargate tasks in private subnets for production workloads.
- Ensure proper **security groups** are configured to allow only necessary traffic.
- Use **IAM Task Roles** to delegate specific AWS permissions at the container level.

# Scaling and Auto-scaling
- **Fargate** supports **Auto-scaling** using **ECS Service Auto-scaling**.
  - Automatically scale your tasks based on demand using CloudWatch alarms and target tracking policies.
  - You can scale based on metrics like CPU, memory usage, or custom application metrics.
  - ECS Service Scheduler ensures that the desired number of tasks are always running, automatically launching or terminating tasks as necessary.

### Horizontal Scaling:
- Increase the number of tasks to handle higher demand or reduce them during low traffic.
- Use **Application Auto Scaling** to manage scaling policies.

# Monitoring and Logging
- **Amazon CloudWatch** provides monitoring and logs for Fargate tasks.
  - Track key metrics such as CPU and memory utilization using CloudWatch metrics.
  - Set up CloudWatch Alarms to alert you when tasks hit specific thresholds (e.g., CPU usage exceeding 80%).
  - Use **CloudWatch Logs** to capture container logs from Fargate tasks.
  
### Monitoring Best Practices:
- Monitor task-level metrics such as CPU, memory, and network traffic.
- Set up CloudWatch Alarms to notify you of performance issues.
- Use **X-Ray** for distributed tracing and gaining deeper insights into your application.

# Best Practices
- Use **Fargate Spot** for cost savings on non-critical tasks that can tolerate interruptions.
- Leverage **IAM Task Roles** to assign least privilege permissions to your tasks.
- Deploy containers in **multiple Availability Zones** for high availability and fault tolerance.
- Monitor task health and use **ECS task draining** to gracefully stop tasks during deployments or scale-down events.
- Regularly audit your task definitions to ensure they use the correct configurations and permissions.

# Fargate Pricing
- **Fargate** charges based on the amount of **vCPU** and **memory** used per task.
  - You only pay for the resources that your tasks consume.
  - Unlike EC2, there is no need to pay for idle instances, leading to better cost efficiency for burstable workloads.
  
**Pricing Factors:**
  - vCPU hours
  - Memory hours
  - Data transfer (if tasks communicate across VPCs or regions)

- Consider using **Fargate Spot** to save up to 70% for workloads that can tolerate interruptions.

# Resources
- [AWS Fargate Docs](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)