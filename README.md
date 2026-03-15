# eks-iac

> 🇧🇷 [Português](#português) | 🇺🇸 [English](#english)

---

## Português

Infraestrutura como Código e manifests Kubernetes para provisionamento e configuração de um cluster EKS na AWS, com pipeline CI/CD via Azure DevOps.

### Arquitetura

- **EKS** cluster com managed node groups
- **ALB Ingress Controller** para gerenciamento de tráfego
- **Cluster Autoscaler** para escalonamento dinâmico
- **CloudFront + S3** para entrega de conteúdo estático
- **ECR** para registro de imagens de container
- **CloudWatch + Fluentd** para logs centralizados
- **IAM** roles e policies seguindo o princípio de menor privilégio

### Estrutura

```
eks-iac/
├── tf/                          # Infraestrutura Terraform
│   ├── main.tf
│   ├── eks.tf
│   ├── network.tf
│   ├── iam.tf
│   ├── ecr.tf
│   ├── cloudfront.tf
│   ├── s3.tf
│   ├── locals.tf
│   ├── variables.tf
│   └── s3-backend-state.tf      # Estado remoto no S3
├── manifests-k8s/               # Manifests Kubernetes
│   ├── cluster_loadbalancer/    # AWS Load Balancer Controller
│   ├── cluster_autoscaler/      # Cluster Autoscaler
│   ├── observability/           # Configuração de alta disponibilidade
│   ├── logs/                    # Fluentd + CloudWatch agent
│   ├── iam/                     # Policies e trust roles IAM
│   ├── rbac/                    # RBAC para ALB
│   └── deploy-manifests.sh      # Script de deploy
└── azure-pipelines.yaml         # Pipeline CI/CD
```

### Como usar

**Provisionando a infraestrutura**

```bash
cd tf/

terraform init
terraform plan
terraform apply
```

**Deploy dos manifests Kubernetes**

```bash
cd manifests-k8s/

# Configurar kubeconfig
aws eks update-kubeconfig --name <cluster-name> --region <region>

# Deploy de todos os manifests
bash deploy-manifests.sh
```

---

## English

Infrastructure as Code and Kubernetes manifests for provisioning and configuring an EKS cluster on AWS, with CI/CD pipeline via Azure DevOps.

### Architecture

- **EKS** cluster with managed node groups
- **ALB Ingress Controller** for traffic management
- **Cluster Autoscaler** for dynamic scaling
- **CloudFront + S3** for static content delivery
- **ECR** for container image registry
- **CloudWatch + Fluentd** for centralized logging
- **IAM** roles and policies following least-privilege principles

### Structure

```
eks-iac/
├── tf/                          # Terraform infrastructure
│   ├── main.tf
│   ├── eks.tf
│   ├── network.tf
│   ├── iam.tf
│   ├── ecr.tf
│   ├── cloudfront.tf
│   ├── s3.tf
│   ├── locals.tf
│   ├── variables.tf
│   └── s3-backend-state.tf      # Remote state on S3
├── manifests-k8s/               # Kubernetes manifests
│   ├── cluster_loadbalancer/    # AWS Load Balancer Controller
│   ├── cluster_autoscaler/      # Cluster Autoscaler
│   ├── observability/           # High availability config
│   ├── logs/                    # Fluentd + CloudWatch agent
│   ├── iam/                     # IAM policies and trust roles
│   ├── rbac/                    # RBAC for ALB
│   └── deploy-manifests.sh      # Deployment script
└── azure-pipelines.yaml         # CI/CD pipeline
```

### Usage

**Provisioning infrastructure**

```bash
cd tf/

terraform init
terraform plan
terraform apply
```

**Deploying Kubernetes manifests**

```bash
cd manifests-k8s/

# Configure kubeconfig
aws eks update-kubeconfig --name <cluster-name> --region <region>

# Deploy all manifests
bash deploy-manifests.sh
```

---

## Stack

![AWS](https://img.shields.io/badge/Amazon_AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white)
![Kubernetes](https://img.shields.io/badge/kubernetes-326ce5.svg?&style=for-the-badge&logo=kubernetes&logoColor=white)
![Azure DevOps](https://img.shields.io/badge/Azure_DevOps-0078D7?style=for-the-badge&logo=azure-devops&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)
