<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Repositories](#repositories)
    - [Private Repositories](#private-repositories)
    - [Public Repositories](#public-repositories)
- [Image Pushing and Pulling](#image-pushing-and-pulling)
- [ECR Authentication](#ecr-authentication)
- [Image Scanning](#image-scanning)
- [ECR Lifecycle Policies](#ecr-lifecycle-policies)
- [ECR Security](#ecr-security)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- [ECR](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html) stands for Elastic Container Registry.
- It is a fully managed Docker container registry service that makes it easy to store, manage, and deploy container images.
- ECR integrates with ECS, EKS, and Lambda, enabling seamless deployment of containers.
- ECR is a regional service.

# Repositories
- An ECR **repository** is where container images are stored and managed.
- You can create both **private** and **public** repositories.

### Private Repositories
- These are accessible only within your AWS account.
- Use IAM policies to control access to private repositories.

### Public Repositories
- Public repositories allow you to share images with the world.
- They come with **ECR Public Gallery**, where users can browse and pull public images.

# Image Pushing and Pulling
- **Pushing**: Upload images to ECR from your local Docker environment or CI/CD pipeline.
- **Pulling**: Download images from ECR to your ECS, EKS, or local environment.
- Use Docker commands like `docker push` and `docker pull` with the correct ECR login.

# ECR Authentication
- ECR integrates with AWS IAM for authentication.
- Use the `aws ecr get-login-password` command to authenticate Docker to ECR.

# Image Scanning
- ECR provides **on-demand** and **automated image scanning** to detect vulnerabilities in your images.
- Integrates with **Amazon Inspector** for deeper security insights.

# ECR Lifecycle Policies
- **Lifecycle policies** automate the removal of old or unused images to optimize storage.
- Helps reduce costs by keeping only the images you need.

# ECR Security
- **IAM** policies control who can push, pull, and manage repositories and images.
- **Encryption**: All images are automatically encrypted at rest using **AWS KMS**.
- **VPC Endpoints**: Use VPC endpoints to privately access ECR without using the public internet.

# Best Practices
- Regularly **scan images** for vulnerabilities to ensure container security.
- Use **lifecycle policies** to automatically clean up old images and optimize costs.
- Avoid hardcoding credentials; rely on **IAM roles** for secure access.
- **Tag your images** properly to make version control easier.

# Resources
- [AWS ECR Docs](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)