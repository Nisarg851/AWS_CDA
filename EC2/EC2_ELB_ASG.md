<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Prerequisite: AWS Fundamentals for EC2 and Load Balancing](#prerequisite-aws-fundamentals-for-ec2-and-load-balancing)
- [EC2 Overview: High Availability and Scalability](#ec2-overview-high-availability-and-scalability)
- [Elastic Load Balancing (ELB) Overview](#elastic-load-balancing-elb-overview)
- [Application Load Balancer (ALB)](#application-load-balancer-alb)
- [Network Load Balancer (NLB)](#network-load-balancer-nlb)
- [Gateway Load Balancer (GLB)](#gateway-load-balancer-glb)
- [ELB Sticky Sessions](#elb-sticky-sessions)
- [ELB Cross-Zone Load Balancing](#elb-cross-zone-load-balancing)
- [ELB SSL Certificates](#elb-ssl-certificates)
- [ELB Connection Draining](#elb-connection-draining)
- [Auto Scaling Groups (ASG) Overview](#auto-scaling-groups-asg-overview)
- [ASG Scaling Policies](#asg-scaling-policies)
- [ASG Instance Refresh](#asg-instance-refresh)
- [References](#references)

---

# Prerequisite: AWS Fundamentals for EC2 and Load Balancing
Before diving into the specifics, it’s essential to understand how EC2, load balancing, and auto-scaling support cloud application resilience and scalability.

- **Compute Services**: AWS EC2 offers virtual machines with a wide range of instance types.
- **Load Balancing**: Ensures distribution of incoming application traffic across multiple instances.
- **Auto Scaling**: Dynamically adjusts the number of EC2 instances based on demand to optimize cost and performance.

# EC2 Overview: High Availability and Scalability
- **Definition**: Amazon EC2 provides resizable compute capacity in the cloud with flexible options to handle variable workloads.
- **High Availability**:
  - **Multi-AZ Deployment**: Ensures instance availability across multiple Availability Zones.
  - **Elastic IP Addresses**: Static IP addresses for failover and redundancy.
- **Scalability**:
  - **On-Demand and Spot Instances**: Allow scaling based on demand while managing costs.
  - **Elastic Load Balancing**: Distributes incoming traffic across instances for seamless scaling.
- **Use Cases**: Web applications, data processing, microservices, or any workloads requiring scalable compute.

# Elastic Load Balancing (ELB) Overview
- **Purpose**: ELB distributes incoming application traffic across multiple targets (e.g., EC2, Lambda, IPs) to enhance fault tolerance and availability.
- **Types of Load Balancers**:
  - **Application Load Balancer (ALB)**: Operates at Layer 7, ideal for HTTP/HTTPS applications with advanced request routing.
  - **Network Load Balancer (NLB)**: Operates at Layer 4, optimized for handling millions of requests per second with low latency.
  - **Gateway Load Balancer (GLB)**: Integrates with third-party firewalls and security appliances.

# Application Load Balancer (ALB)
- **Layer 7**: Routes based on HTTP/HTTPS, supporting complex application logic.
- **Key Features**:
  - **Content-Based Routing**: Routes requests based on URL paths, headers, or query strings.
  - **WebSocket Support**: Maintains persistent connections for real-time applications.
  - **Host-Based Routing**: Directs traffic based on hostname in requests.
- **Use Cases**: Microservices, web apps requiring SSL termination, and applications with session stickiness requirements.

# Network Load Balancer (NLB)
- **Layer 4**: Operates at the transport layer, providing TCP/UDP load balancing with minimal latency.
- **Key Features**:
  - **Static IP Support**: Ideal for applications requiring a fixed IP for endpoint access.
  - **High Throughput**: Handles extreme levels of request traffic, making it suitable for latency-sensitive applications.
  - **Cross-Zone Load Balancing**: Option to distribute traffic evenly across AZs.
- **Use Cases**: Gaming, real-time financial transactions, and workloads needing a static IP.

# Gateway Load Balancer (GLB)
- **Purpose**: Combines security appliance functions with load balancing, commonly used with third-party network appliances.
- **Features**:
  - **Traffic Distribution**: Balances traffic across firewall or security devices.
  - **Seamless Integration**: Works with partner appliances and VPC endpoints.
  - **Inline Security Appliances**: Integrates with services like Palo Alto or Fortinet firewalls.
- **Use Cases**: Advanced network security applications, intrusion detection systems, and virtual firewalls.

# ELB Sticky Sessions
- **Purpose**: Ensures a user’s session persists with a single backend instance to maintain session state.
- **Functionality**:
  - **Session Affinity**: Associates a client session with a specific instance.
  - **Duration**: Configurable session length, adjustable based on application requirements.
- **Use Cases**: Stateful applications like shopping carts, web portals, and applications requiring user session continuity.

# ELB Cross-Zone Load Balancing
- **Overview**: Distributes incoming traffic evenly across all instances in all enabled AZs, optimizing resource utilization.
- **Benefits**:
  - **Improved Availability**: Balances traffic, even if instances are unevenly distributed.
  - **Cost-Efficiency**: Avoids overloading a single AZ by utilizing resources across zones.
- **Use Cases**: Applications with instances distributed across multiple AZs needing even traffic distribution.

# ELB SSL Certificates
- **Purpose**: Allows HTTPS traffic for secure communication between the client and the load balancer.
- **Configuration**:
  - **SSL/TLS Certificate Manager**: AWS Certificate Manager (ACM) simplifies certificate management.
  - **Custom SSL Policy**: Enforce strong ciphers and protocols for enhanced security.
- **Use Cases**: E-commerce, financial services, or any application requiring encrypted client-server communication.

# ELB Connection Draining
- **Purpose**: Ensures graceful handling of connections by keeping connections alive during instance de-registration or scaling events.
- **Features**:
  - **Customizable Timeout**: Set time for ongoing requests to complete before instance removal.
  - **Graceful Failover**: Ensures user requests complete smoothly during scale-in.
- **Use Cases**: Recommended for applications with long-lived connections or significant stateful requests.

# Auto Scaling Groups (ASG) Overview
- **Purpose**: ASGs manage EC2 instance scaling by maintaining the required number of instances according to demand.
- **Components**:
  - **Launch Templates**: Specify instance configuration, networking, and storage.
  - **Health Checks**: Automatically replace instances marked as unhealthy.
  - **Scaling Policies**: Adjusts the number of instances based on dynamic needs.
- **Use Cases**: Applications with variable workloads, batch processing, web services with unpredictable traffic.

# ASG Scaling Policies
- **Types**:
  - **Target Tracking Scaling**: Adjusts instances to maintain a predefined target, such as CPU utilization.
  - **Step Scaling**: Scales in response to metric thresholds with incremental adjustments.
  - **Scheduled Scaling**: Configures scaling based on predictable traffic patterns (e.g., nightly batch jobs).
- **Best Practices**: Define clear thresholds and alarms to trigger scaling events effectively.
- **Use Cases**: Optimal for managing applications with predictable demand patterns or steady growth.

# ASG Instance Refresh
- **Purpose**: Automates instance updates in an ASG, replacing instances without impacting application availability.
- **Features**:
  - **Rolling Update**: Replaces instances gradually, controlling disruption.
  - **Health Checks**: Ensures only healthy instances are kept in the group.
  - **Triggering Events**: Can be triggered manually or in response to new launch templates.
- **Use Cases**: Useful for updating software, patching OS, and replacing older instances with minimal disruption.

---

# References
- [AWS Docs](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
