<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Elastic Beanstalk Architecture](#elastic-beanstalk-architecture)
- [Supported Platforms](#supported-platforms)
- [Application Deployment](#application-deployment)
    - [Deployment Options](#deployment-options)
    - [Environment Tiers](#environment-tiers)
- [Environment Configuration](#environment-configuration)
    - [Load Balancing and Auto Scaling](#load-balancing-and-auto-scaling)
    - [Environment Variables](#environment-variables)
    - [Instance Configuration](#instance-configuration)
- [Scaling and Load Balancing](#scaling-and-load-balancing)
- [Monitoring, Logging, and Alarms](#monitoring-logging-and-alarms)
- [Blue/Green Deployment](#bluegreen-deployment)
- [Best Practices](#best-practices)
- [Elastic Beanstalk and CI/CD](#elastic-beanstalk-and-cicd)
- [Elastic Beanstalk Pricing](#elastic-beanstalk-pricing)
- [Resources](#resources)

# Introduction
- [Elastic Beanstalk](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html) is an AWS PaaS service used to deploy web applications.
- It abstracts infrastructure management by automatically provisioning and managing services like **EC2**, **Load Balancers**, **Auto Scaling**, and **RDS**.
- Beanstalk supports seamless deployment, scaling, and monitoring of applications.

# Elastic Beanstalk Architecture
- The architecture of Elastic Beanstalk includes a **Managed Environment**, where AWS creates the necessary infrastructure for your application.
- It supports both **Web Server** and **Worker Environments**:
  - **Web Server Environment** handles HTTP requests, load balancing, and scaling.
  - **Worker Environment** is for background processing jobs and integrates with Amazon SQS (Simple Queue Service) for task execution.
  
# Supported Platforms
- **Elastic Beanstalk** supports multiple platforms for deploying applications, including:
  - **Java**, **Node.js**, **Python**, **PHP**, **Ruby**, **.NET**, **Go**, and **Docker**.
- Docker is used for custom environments where you define your runtime and dependencies.

# Application Deployment
- Deploy applications through **Application Versions**:
  - Application versions can be source code files, binaries, or Docker images.
  - Each application can have multiple environments, making it easier to manage staging, production, or testing environments.

### Deployment Options
- Elastic Beanstalk offers several deployment strategies:
  - **All at once**: Deploys to all instances simultaneously, which might cause downtime.
  - **Rolling**: Deploys to a few instances at a time, then moves to the next set of instances.
  - **Rolling with Additional Batch**: Adds new instances during deployment to avoid reducing capacity.
  - **Immutable**: Creates a completely new set of instances for deployment, ensuring rollback without affecting production.
  - **Blue/Green**: Switches traffic from the old environment to the new one without affecting live users.

### Environment Tiers
- **Web Server Environment**:
  - Processes web requests and handles scaling, load balancing, and monitoring automatically.
  - Typically runs application servers like Apache, NGINX, or Tomcat.
- **Worker Environment**:
  - Handles background tasks or jobs using Amazon SQS and can be scaled based on demand.

# Environment Configuration
### Load Balancing and Auto Scaling
- **Elastic Load Balancer (ELB)** is used in Web Server Environments to distribute traffic across multiple EC2 instances.
- **Auto Scaling** ensures the application can scale based on traffic or custom CloudWatch metrics.
  - You can set policies to trigger scaling when CPU usage or memory usage crosses a certain threshold.
  
### Environment Variables
- Elastic Beanstalk allows the configuration of environment variables for different environments.
  - This is useful for database connection strings, API keys, or any configuration that changes between environments.

### Instance Configuration
- Configure EC2 instance type (CPU, memory, storage) directly within Elastic Beanstalk.
  - You can use **On-Demand**, **Reserved**, or **Spot** instances depending on the cost and use case.

# Scaling and Load Balancing
- **Auto Scaling**: Automatically adds or removes EC2 instances based on demand.
  - Scale-out when traffic increases and scale-in during periods of low traffic.
- **Elastic Load Balancer**: Distributes incoming traffic evenly across multiple EC2 instances.
  - Health checks ensure that traffic is only routed to healthy instances.

# Monitoring, Logging, and Alarms
- **Amazon CloudWatch** is integrated to monitor the health of environments.
  - You can track key metrics such as CPU usage, request count, and memory consumption.
- Logs can be accessed directly from the Elastic Beanstalk console or sent to **Amazon S3** for persistence.
- Set up **CloudWatch Alarms** to notify you when specific thresholds are exceeded.

# Blue/Green Deployment
- **Blue/Green Deployment** allows for zero-downtime deployments:
  - Deploy a new version (Green Environment) and test it, then switch traffic over from the old version (Blue Environment).
  - If an issue arises in the new version, traffic can be routed back to the old environment quickly.

# Best Practices
- Use **Immutable Deployment** for mission-critical applications to avoid risks during deployment.
- Set up **Blue/Green Deployment** to minimize downtime and ensure rollback capabilities.
- Use **Managed Updates** to automatically update the platform to the latest version, ensuring security and stability.
- Regularly monitor the application with **CloudWatch** and configure custom metrics based on your application’s needs.

# Elastic Beanstalk and CI/CD
- Elastic Beanstalk can be integrated with **AWS CodePipeline** and **CodeBuild** to create a full CI/CD pipeline.
  - You can automate the entire process of building, testing, and deploying your application.
  - It supports hooks like **GitHub** or **Bitbucket** for continuous integration.

# Elastic Beanstalk Pricing
- Elastic Beanstalk is free to use, but you pay for the underlying resources (EC2, RDS, S3, etc.).
  - Pricing depends on the EC2 instance type, database, and other resources used in the environment.
  - It's best to review the **AWS Pricing Calculator** for detailed cost analysis.

# Resources
- [AWS Elastic Beanstalk Docs](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/Welcome.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)