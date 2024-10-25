<h1> Things to do </h1>

- Provide date on which the document was last edited
- Provide reference for the information
- Provide video link for the hands-on labs
---

- [Introduction](#introduction)
- [Core Concepts](#core-concepts)
  - [Stages](#stages)
  - [Endpoints](#endpoints)
  - [Caching](#caching)
  - [Canary Deployments](#canary-deployments)
  - [Deployment Versions and Rollbacks](#deployment-versions-and-rollbacks)
- [API Types](#api-types)
- [Throttling and Rate Limits](#throttling-and-rate-limits)
- [Security and Access Control](#security-and-access-control)
  - [Authorization](#authorization)
  - [API Keys](#api-keys)
  - [Resource Policies](#resource-policies)
- [Integrations and Mappings](#integrations-and-mappings)
  - [Mapping Templates](#mapping-templates)
  - [CORS Configuration](#cors-configuration)
- [Monitoring and Logging](#monitoring-and-logging)
- [Best Practices](#best-practices)
- [Resources](#resources)

---

# Introduction
- **API Gateway** provides a fully managed service to create, publish, and manage REST, HTTP, and WebSocket APIs.
- Facilitates efficient connection between clients and backend services, with support for multiple API types for diverse needs.
- **Key exam focus**: configuring, deploying, and managing APIs along with controlling access and securing integrations.

# Core Concepts
## Stages
- **Stages** represent distinct API versions that can be configured for various environments (development, production).
- **Stage Variables** are like environment variables for stage-specific configurations (e.g., setting the backend endpoint URL).

## Endpoints
- **Edge-Optimized**: Suitable for global clients, with reduced latency using CloudFront distribution.
- **Regional**: Hosted within specific AWS regions, suitable for low-latency local applications.
- **Private**: Limited to VPCs using VPC endpoints, ideal for internal applications.

## Caching
- **Stage-Level Caching** improves performance by reducing backend calls. Configurable size and TTL settings are available.
- Selective caching can be applied on individual resources or methods.

## Canary Deployments
- **Canary Deployments** allow staged rollouts for API changes by splitting traffic between current and new versions.
    - Canary percentage splits traffic to a subset of users to test new deployments.
    - Monitoring canary deployments helps detect potential issues before full-scale rollout.

## Deployment Versions and Rollbacks
- Deployment versions are uniquely identified and enable quick rollback to a stable version if an issue arises.
- Can be set up with an automated **CI/CD pipeline** for continuous delivery.

# API Types
1. **REST API**: Full-featured, configurable API supporting Lambda Authorizers, usage plans, and caching.
2. **HTTP API**: Lightweight, low-cost option ideal for simple integrations with Lambda and HTTP backends.
3. **WebSocket API**: Supports bidirectional communication for real-time use cases like chat applications and game updates.

# Throttling and Rate Limits
- **Throttling**: Limits the number of requests per second (RPS) at a method or stage level.
- **Burst Limit**: Handles sudden spikes by allowing a short burst of requests beyond the set RPS.
- Rate limits are useful in managing costs and preventing abuse.

# Security and Access Control
## Authorization
- **IAM Permissions**: Uses SigV4 for securely controlling API access through AWS roles and policies.
- **Cognito User Pools**: Offers OAuth support for token-based authentication.
- **Lambda Authorizers**: Custom token validation using a Lambda function to control access by request headers or parameters.

## API Keys
- Managed at the stage level and often tied to usage plans to limit access.
- **Usage Plans** define rate limiting, throttling, and burst limits per API key, ensuring access control and cost management.

## Resource Policies
- Policies are JSON-based and limit access based on conditions like IP ranges, VPCs, or source accounts.
- Effective for managing access to APIs within an organization or network boundary.

# Integrations and Mappings
## Mapping Templates
- **Mapping Templates**: Transform request and response payloads for seamless backend interaction.
    - Templates can be used to **convert incoming requests** to specific backend formats.
    - Supports **Velocity Template Language (VTL)** to specify transformations.
  
## CORS Configuration
- **CORS** allows cross-origin resource sharing, commonly needed when APIs are called from web applications on different domains.
- Easily enabled in API Gateway and includes configuration of allowed methods and headers.

# Monitoring and Logging
- **CloudWatch Metrics**: Monitors request counts, error rates, latency, and 4xx/5xx error counts.
- **Access Logging**: Logs detailed information on requests for auditing and debugging.
- **AWS X-Ray**: For tracing API calls across services, providing end-to-end request tracking.

# Best Practices
- **Enable Caching** to improve response times and reduce backend load.
- **Use Canary Deployments** for safe, gradual rollouts.
- Set up **Usage Plans and API Keys** for access management and cost control.
- Regularly monitor CloudWatch **metrics and logs** to ensure API health and troubleshoot issues.
- **CI/CD Pipelines** for automated, consistent deployments.

# Resources
- [AWS API Gateway Documentation](https://docs.aws.amazon.com/apigateway/)
- [AWS Notes by Tahseer](https://arkalim.notion.site/IAM-e1b1d6d4287644b8874dd7614f3c6d49#fd868bc3e20c40a3818fa77334f76be7)