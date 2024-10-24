<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Fargate Launch Type](#fargate-launch-type)
    - [Task Definitions in Fargate](#task-definitions-in-fargate)
    - [Fargate vs EC2](#fargate-vs-ec2)
- [Fargate Networking](#fargate-networking)
    - [VPC Integration](#vpc-integration)
    - [Security Groups](#security-groups)
- [Auto Scaling in Fargate](#auto-scaling-in-fargate)
- [Fargate Pricing](#fargate-pricing)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- [Fargate](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html) is a serverless compute engine for containers.
- It works with both **Amazon ECS** and **Amazon EKS**.
- You do not need to manage any EC2 instances; AWS handles the provisioning and scaling.

# Fargate Launch Type
- **Fargate** allows you to run containers without managing servers.
- AWS handles infrastructure, scaling, and patching.
- You pay for the vCPU and memory resources used by the containers.

### Task Definitions in Fargate
- A **Task Definition** specifies how containers should be run, including CPU/memory requirements, networking, and the container image.
- You can define multiple containers in one task.

### Fargate vs EC2
- **Fargate**: Serverless, no need to manage infrastructure.
- **EC2**: You are responsible for managing EC2 instances, which provides more control but more overhead.

# Fargate Networking
### VPC Integration
- Fargate tasks run in your VPC, using the **AWS VPC Mode** for network isolation.
- Each task gets its own IP address within the VPC.

### Security Groups
- You can apply **security groups** to Fargate tasks for controlling inbound and outbound traffic.

# Auto Scaling in Fargate
- Fargate integrates with **ECS Service Auto Scaling**, allowing tasks to scale up or down based on demand.
- You can set scaling policies based on metrics like CPU usage, memory, or custom CloudWatch alarms.

# Fargate Pricing
- Fargate pricing is based on the **vCPU** and **memory** resources used by your tasks.
- No upfront costs; pay only for what you use.

# Best Practices
- Use **Fargate** to avoid the complexity of managing EC2 instances unless you need specific customizations.
- Set up **Auto Scaling** to handle traffic spikes efficiently.
- Apply **IAM Roles** to tasks instead of embedding credentials in your containers.
- Monitor tasks with **CloudWatch** and optimize costs by adjusting CPU and memory allocations based on task needs.

# Resources
- [AWS Fargate Docs](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/AWS_Fargate.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)