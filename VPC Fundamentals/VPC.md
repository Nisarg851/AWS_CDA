<h1>Things to do</h1>

- Provide the date when the document was last edited.
- Provide references for the information.
- Include video links for hands-on labs.
---
- [Introduction](#introduction)
- [VPC Components](#vpc-components)
  - [Subnets](#subnets)
  - [Internet Gateway](#internet-gateway)
  - [NAT Gateway/Instances](#nat-gatewayinstances)
  - [Network Access Control Lists (NACL)](#network-access-control-lists-nacl)
  - [Security Groups](#security-groups)
  - [VPC Peering](#vpc-peering)
  - [VPC Endpoints](#vpc-endpoints)
  - [VPC Flow Logs](#vpc-flow-logs)
- [Network Connectivity](#network-connectivity)
  - [Site-to-Site VPN](#site-to-site-vpn)
  - [Direct Connect](#direct-connect)
- [Additional Topics](#additional-topics)
- [Best Practices](#best-practices)
- [Resources](#resources)

# Introduction
- **Virtual Private Cloud (VPC)**: AWS service that provides logically isolated virtual networks where you can define your IP range, subnets, route tables, and network gateways.
- Each VPC has a dedicated CIDR block and can be further divided into subnets associated with specific availability zones.
- **AWS Region Bound**: A VPC is region-specific and cannot span across multiple regions.

# VPC Components
## Subnets
- **Subnets** divide the VPC into smaller segments. Each subnet must be associated with a single Availability Zone (AZ).
- Subnets can be either **public** (accessible to the internet via an Internet Gateway) or **private** (only accessible within the VPC).
- Public subnets typically contain resources that need direct access to the internet, while private subnets are used for backend resources.

## Internet Gateway
- A fully managed AWS component attached to a VPC to provide internet access to resources in public subnets.
- **One-to-One Mapping**: Each VPC can only have one Internet Gateway attached.

## NAT Gateway/Instances
- **NAT Gateway**: Managed AWS service that enables instances in private subnets to access the internet without exposing them to inbound internet traffic.
- **NAT Instances**: Alternative to NAT Gateways, requiring more configuration and management, usually used when cost is a concern.
- **Use Case**: Allows updates and software installation on instances in private subnets.

## Network Access Control Lists (NACL)
- Stateless firewall at the subnet level that controls inbound and outbound traffic.
- **Rules** are evaluated in numerical order, allowing or denying traffic based on IP, protocol, and port range.
- NACLs are stateless, meaning both inbound and outbound rules need to be explicitly defined.

## Security Groups
- **Stateful** firewall applied at the instance level, controlling inbound and outbound traffic based on rules.
- Each rule can specify an IP range, protocol, and port, and can be attached to multiple instances.
- Unlike NACLs, Security Groups automatically allow response traffic, making them stateful.

## VPC Peering
- Allows connection between two VPCs, enabling them to communicate privately without using an Internet Gateway.
- **Non-transitive**: A VPC peered with another VPC does not automatically have access to the networks of other VPCs peered to the same VPC.

## VPC Endpoints
- Enable private connections between a VPC and AWS services without using an Internet Gateway, NAT device, VPN, or Direct Connect.
- **Two Types**:
  - **Gateway Endpoints**: Support S3 and DynamoDB.
  - **Interface Endpoints**: Support various AWS services via Elastic Network Interfaces (ENIs).

## VPC Flow Logs
- Provides detailed traffic logs for monitoring and troubleshooting at the VPC, subnet, or instance level.
- **Use Case**: Useful for security audits, tracking network traffic patterns, and troubleshooting connectivity issues.

# Network Connectivity
## Site-to-Site VPN
- Connects an on-premises data center to AWS over the internet using a VPN.
- Provides a secure, encrypted connection, typically used when direct connections are not required or are cost-prohibitive.

## Direct Connect
- Dedicated, private connection from on-premises data center to AWS.
- Provides lower latency, more consistent network performance, and increased bandwidth compared to a Site-to-Site VPN.

# Additional Topics
- **Elastic IPs**: Static IPs allocated by AWS for use within your VPC, commonly used for resources needing a fixed IP.
- **Route Tables**: Directs network traffic within the VPC. Each subnet must be associated with a route table that determines the destination of outbound traffic.
- **Bastion Host**: A secure server placed in a public subnet for managing access to resources in private subnets.

# Best Practices
- Avoid hardcoding IPs and CIDR blocks in application code. Use environment variables or AWS-specific tools like Systems Manager Parameter Store.
- Enable VPC Flow Logs for auditing purposes but avoid logging unnecessary traffic to reduce costs.
- Use NAT Gateways instead of NAT Instances whenever possible, as they are fully managed and scale automatically.
- Limit VPC Peering to essential connections to avoid complex network topologies and unintended access.
- Implement least privilege principles in Security Groups and NACLs to enhance network security.

# Resources
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [AWS VPC Networking Overview](https://aws.amazon.com/vpc/faqs/)
- [VPC Best Practices - AWS Whitepaper](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/introduction.html)
- [AWS Notes by Tahseer](https://arkalim.notion.site/Notes-143374c83daa4d4991b07400056a2aa9)
