# EKS.

Amazon Elastic Kubernetes Service (EKS) is a managed Kubernetes service that allows you to run Kubernetes clusters in AWS without 
having to install, operate, or maintain the control plane.

## Key components of an EKS cluster:
#### Control Plane (Managed by AWS)
  - Kubernetes API server
  - etcd (key-value store for cluster state)
#### Automated scaling & updates
  - Worker Nodes (Managed by You)
  - EC2 instances or Fargate (serverless)
Runs your applications as Kubernetes Pods


## Advantages of EKS
- Fully Managed Control Plane
- High Availability & Scalability
- Secure & Integrated with AWS Services
-  Cost Optimization
-  Kubernetes Compliance & Updates

## Different ways to spin the EKS cluster
- AWS Console
- AWS CLI
- AWS Cloud formation
- Devops tools Terraform
- EKSCTL


## What is eksctl and commands associated with it.
- CLI tool for creating EKS cluster.
- eksctl is a command-line tool for creating, managing, and deleting Amazon Elastic Kubernetes Service (EKS) clusters.
It simplifies working with EKS by automating cluster setup and configuration.
-  Abstracts creating VPC, subnets, security groups ..etc
-  
