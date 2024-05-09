# Nginx Service Deployment Guide with AWS Blue-Green Deployment

## Overview
This guide outlines the deployment process for the Nginx service using AWS Blue-Green deployment strategy. Nginx acts as the front-facing server directing traffic to the backend Phalcon service. We utilize AWS services such as ECS Fargate, CodePipeline for CI/CD, AWS App Mesh, AWS Cloud Map, ALB (Application Load Balancer), and NLB (Network Load Balancer) for effective deployment and service orchestration.

### Technologies Used:
- AWS ECS Fargate
- AWS CodePipeline
- AWS App Mesh
- AWS Cloud Map
- AWS ECR (Elastic Container Registry)
- ALB (Application Load Balancer)
- NLB (Network Load Balancer)

## Deployment Steps

### 1. Docker Configuration
- **Dockerfile**: Defines the Nginx container setup.
- **appspec.yaml**: Specifies the ECS service and its configurations.

### 2. Task Definition
- **taskdef.json**: Defines the ECS task configuration for Nginx.

### 3. Nginx Configuration
- **nginx.conf**: Nginx server configuration handling routing and PHP requests.

### 4. Deployment Strategy
#### Blue-Green Deployment
- Blue-Green deployment ensures zero-downtime deployment and rollback capabilities by creating a separate set of resources for the new version (Green) while keeping the old version (Blue) intact.
  
### 5. ALB and NLB Configuration
- **ALB**: Routes traffic to Nginx.
- **NLB**: Routes traffic to Phalcon backend (PHP).

### 6. AWS App Mesh Integration
- **Proxy Configuration**: Manages traffic routing and service discovery between Nginx and Phalcon containers using AWS App Mesh.

## How It Works
1. **CodePipeline**: Initiates deployment upon code changes.
2. **Build & Test (CI)**: Code changes are built and tested.
3. **Blue-Green Deployment**:
   - **Blue Environment**: Existing stable environment.
   - **Green Environment**: New environment with updates.
4. **Traffic Routing**:
   - **ALB**: Routes traffic to the Nginx container in the Blue or Green environment.
   - **NLB**: Routes traffic to the Phalcon backend (PHP).
5. **AWS App Mesh**:
   - Facilitates seamless communication between Nginx and Phalcon containers.
   - Provides service discovery and routing capabilities.
6. **Rollback**:
   - If issues arise, rollback to the stable Blue environment is seamless.

## Conclusion
This deployment strategy ensures reliable and scalable deployment of the Nginx service with minimal downtime and risk. By leveraging AWS services like ECS, CodePipeline, ALB, NLB, and AWS App Mesh, the deployment process is streamlined, offering flexibility and efficiency in managing containerized applications.
