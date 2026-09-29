# Production-Ready AWS EKS Infrastructure via Terraform

This repository provisions a secure, highly-available, and production-ready **Amazon EKS (Elastic Kubernetes Service)** cluster along with its custom **VPC network** on AWS using modular Terraform.
📐 Architecture Overview
graph TD
    subgraph AWS_Cloud ["AWS Cloud Region (us-east-1)"]
        subgraph VPC ["VPC (10.0.0.0/16)"]

            subgraph Public_Subnets ["Public Subnets (10.0.1.0/24, 10.0.2.0/24)"]
                IGW["Internet Gateway"]
                NAT["NAT Gateway"]
            end

            subgraph Private_Subnets ["Private Subnets (10.0.10.0/24, 10.0.20.0/24)"]
                ControlPlane["EKS Control Plane"]
                Nodes["EKS Worker Nodes"]
            end

        end
    end

    IGW -->|Inbound / Outbound Routing| NAT
    NAT -->|Outbound Internet Access| Nodes
    ControlPlane -->|K8s API Management| Nodes
🛠️️ Tech Stack & Key Features
Infrastructure as Code: Terraform (v5.x AWS Provider)

Container Orchestration: Amazon EKS (v20.x EKS Module, K8s 1.30)

Node OS: Amazon Linux 2023 (AL2023_x86_64_STANDARD)

Networking: Dedicated VPC with isolated Public/Private Subnets and NAT Gateway

Security: Strict IAM Roles, Private Worker Nodes, and Version Control Locking

🚀 Usage & Deployment Guide
Prerequisites
AWS CLI configured with valid administrator permissions.

Terraform CLI (v1.5+) installed on your machine.

kubectl for managing Kubernetes resources.

1. Clone the Repository
Bash
git clone https://github.com/wahablabs/terraform-aws-eks-pipeline.git
cd terraform-aws-eks-pipeline
2. Initialize Infrastructure Code
Bash
terraform init
3. Review Provisioning Plan
Bash
terraform plan
4. Deploy EKS Cluster & Networking
Bash
terraform apply --auto-approve
5. Configure kubectl Access
Once applied, configure your local Kubernetes context:

Bash
aws eks update-kubeconfig --region us-east-1 --name devops-portfolio-eks
kubectl get nodes
6. Clean Up & Destroy Resources
To avoid ongoing AWS charges, destroy the environment:

Bash
terraform destroy --auto-approve