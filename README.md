# Production-Ready AWS EKS Infrastructure via Terraform

This repository provisions a secure, highly-available, and production-ready **Amazon EKS (Elastic Kubernetes Service)** cluster along with its custom **VPC network** on AWS using modular Terraform.

```mermaid
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
