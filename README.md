# Azure AKS Production Deployment Project

This project focuses on deploying a secure application on a Production-grade Kubernetes cluster using Azure AKS.

It includes end-to-end infrastructure provisioning using Azure, Kubernetes, Terraform, CI/CD pipelines, ArgoCD, Helm, ExternalDNS and CertManager.

## Task/Assignment 📝

Create your own repository and complete the task there. You may take any app or create an app, your choice.

**The Goal:**

You will deploy a cloud-native application on Azure AKS using best practices for infrastructure provisioning, CI/CD automation, and security. You'll also set up GitOps automation with ArgoCD and dynamic DNS updates.

When complete, the application should for example be accessible via HTTPS at: `https://aks.<your-domain>` or `https://aks.labs.<your-domain>`

## Deliverables

- Infrastructure as code using Terraform modules for AKS and related Azure services.
- CI/CD pipelines automating security scans, Docker image builds, and application deployments to AKS.
- Dynamic DNS and SSL/TLS certificate management for secure endpoints.
- Monitoring of AKS and application health with dashboards using Prometheus and Grafana.
- GitOps-driven automated deployments via ArgoCD.

## Project Tasks 🔧

### 1. Azure Infrastructure Setup (Terraform)

- Create an AKS cluster, Virtual Network, Resource Groups, and Network Security Groups using Terraform.
- Use reusable Terraform modules for infrastructure components. Ensure proper state management is in place.
- Configure networking with private subnets for the AKS cluster and public subnets for load balancing.
- Define Azure Active Directory integration for the Kubernetes cluster and ensure Network Security Groups limit access to only required resources.

### 2. NGINX Ingress Controller

- Deploy and configure the NGINX Ingress Controller on the AKS cluster using Helm charts or Kubernetes manifests.
- Configure the controller to route incoming traffic to the correct Kubernetes services.
- Set up rules for HTTPS using TLS certificates managed by CertManager (see task below).

### 3. CertManager (SSL/TLS Management)

- Install and configure CertManager on the cluster.
- Set up Let's Encrypt or a custom CA to generate SSL certificates automatically for the application.
- Integrate the certificates with the NGINX Ingress Controller for secure HTTPS connections.

### 4. Dynamic DNS Updates (ExternalDNS)

- Deploy ExternalDNS on the AKS cluster to automate DNS record management.
- Configure ExternalDNS to dynamically update DNS records in Azure DNS (or Cloudflare) based on changes in Kubernetes ingress resources.
- Ensure the DNS updates reflect the public endpoint of the application when services or ingresses change.

### 5. CI/CD Pipelines: Automate Everything 🚀

#### Pipeline 1: Terraform

- Automate Terraform deployments for provisioning AKS and related Azure resources.
- Integrate state management using a remote backend (e.g., Azure Storage Account and Blob Container + State Locking).
- Scan the Terraform code using Checkov to catch misconfigurations and ensure compliance with security best practices.

#### Pipeline 2: Docker, Security, and Kubernetes

- Build and push the Docker image of your application to Azure Container Registry (ACR) using the pipeline.
- Use Trivy to scan the Docker image for vulnerabilities.

### 6. GitOps with ArgoCD

- Set up ArgoCD to automate the deployment of Kubernetes manifests from your Git repository to the AKS cluster.
- Ensure the deployment is triggered (synchronised) automatically when changes are pushed to the repo.
- Create a GitOps workflow where the cluster state is reconciled with the desired state defined in the Git repository. (check sync settings)

### 7. Monitoring and Observability

- Deploy Prometheus to collect metrics from the Kubernetes cluster, including pods, nodes, cluster, etc.
- Set up Grafana to visualise the metrics and create custom dashboards or use (community dashboards).

### 8. Architecture and Documentation

Create a clear and well designed architecture diagram using draw.io, Cloudairy, or Mermaid. Also create a clear README documenting your project, the goal, the components, and how it was done.

## Useful Links 🔗

- [Terraform Docs](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs)
- [AKS Documentation](https://docs.microsoft.com/en-us/azure/aks/)
- [ArgoCD Docs](https://argo-cd.readthedocs.io/)
- [Checkov Security Scanning](https://www.checkov.io/)
- [Azure Container Registry](https://docs.microsoft.com/en-us/azure/container-registry/)
- [Azure DNS](https://docs.microsoft.com/en-us/azure/dns/)

## Key Azure Services Used

- **Azure Kubernetes Service (AKS)** - Managed Kubernetes cluster
- **Azure Container Registry (ACR)** - Container image registry
- **Azure Virtual Network** - Network infrastructure
- **Azure DNS** - DNS management
- **Azure Active Directory** - Identity and access management
- **Azure Storage Account** - Terraform state backend
- **Network Security Groups** - Network security rules
- **Azure Resource Groups** - Resource organisation and management

---

## Getting Started

1. Clone this repository
2. Set up your Azure credentials and subscription
3. Configure Terraform backend for state management
4. Follow the tasks in order as outlined above
5. Deploy and test your application

## Prerequisites

- Azure CLI installed and configured
- Terraform installed
- kubectl installed
- Helm installed
- Docker installed
- Git repository for GitOps workflow

## Example Project Structure

```
├── terraform/
│   ├── modules/
│   ├── environments/
│   └── main.tf
├── k8s-manifests/
│   ├── ingress/
│   ├── cert-manager/
│   └── monitoring/
├── ci-cd/
│   └── pipelines/
├── app/
│   ├── Dockerfile
│   └── src/
└── docs/
    └── architecture-diagram
```
