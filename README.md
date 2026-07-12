# 🚀 StreamingApp – CI/CD Deployment on AWS EKS

## 📌 Project Overview

This project demonstrates a complete DevOps CI/CD pipeline for deploying a MERN-based Streaming Application on Amazon EKS using Docker, Jenkins, Amazon ECR, Helm, and CloudWatch.

The application is containerized, automatically built through Jenkins, pushed to Amazon Elastic Container Registry (ECR), and deployed on Amazon Elastic Kubernetes Service (EKS). Monitoring and logging are enabled using Amazon CloudWatch Container Insights.

---

# 🏗️ Architecture

```
GitHub Repository
        │
        ▼
 GitHub Webhook
        │
        ▼
 Jenkins Pipeline
        │
        ▼
 Docker Build
        │
        ▼
 Amazon ECR
        │
        ▼
 Amazon EKS
        │
        ▼
 Helm Deployment
        │
        ▼
Frontend + Backend + MongoDB
        │
        ▼
Amazon CloudWatch
```
![Uploading image.png…]()

---

# 🛠 Tech Stack

| Category | Technology |
|-----------|------------|
| Source Control | Git, GitHub |
| CI/CD | Jenkins |
| Containerization | Docker |
| Container Registry | Amazon ECR |
| Orchestration | Kubernetes (Amazon EKS) |
| Package Manager | Helm |
| Monitoring | Amazon CloudWatch |
| Logging | CloudWatch Logs |
| Database | MongoDB |
| Cloud | AWS |

---

# 📂 Repository Structure

```
StreamingApp/
│
├── frontend/
│   ├── Dockerfile
│   └── source code
│
├── hello-service/
│   ├── Dockerfile
│   └── source code
│
├── profile-service/
│   ├── Dockerfile
│   └── source code
│
├── helm-chart/
│   ├── Chart.yaml
│   ├── values.yaml
│   └── templates/
│
├── Jenkinsfile
│
└── README.md
```

---

# ⚙️ Project Workflow

## Step 1 – Fork Repository

Forked the original project repository into GitHub.

```
GitHub
        ↓
Fork Repository
```

---

## Step 2 – Dockerization

Created Docker images for

- Frontend
- Hello Service
- Profile Service

Built images using Docker.

```
docker build
```

---

## Step 3 – Amazon ECR

Created Amazon ECR repositories

- streaming-frontend
- streaming-hello-service
- streaming-profile-service

Pushed Docker images to ECR.

---

## Step 4 – Jenkins CI Pipeline

Installed Jenkins on AWS EC2.

Configured

- Git
- Docker
- AWS Credentials
- Amazon ECR Login

Pipeline stages

- Checkout Source
- Build Frontend Image
- Build Hello Service Image
- Build Profile Service Image
- Verify AWS Credentials
- Login to Amazon ECR
- Tag Images
- Push Images to Amazon ECR

Pipeline execution is automatically triggered using GitHub Webhooks.

---

## Step 5 – GitHub Webhook

Configured GitHub Webhook to trigger Jenkins automatically after every push.

```
GitHub Push
        │
        ▼
 Jenkins Build
```

---

# ☸ Kubernetes Deployment

Amazon EKS Cluster created using eksctl.

Verified cluster

```
kubectl get nodes
```

Deployed application using Helm.

```
helm install streaming-app .
```

Verified deployment

```
kubectl get pods

kubectl get svc

helm list
```

---

# 📦 Kubernetes Components

Deployments

- Frontend
- Hello Service
- Profile Service
- MongoDB

Services

- Frontend LoadBalancer
- Hello Service ClusterIP
- Profile Service ClusterIP
- MongoDB ClusterIP

---

# 📊 Monitoring

Configured

- Amazon CloudWatch Agent
- Fluent Bit
- Container Insights

Verified

- Cluster Metrics
- Node Metrics
- Memory Utilization
- CPU Utilization
- Logs

---

# 🔁 CI/CD Flow

```
Developer
     │
     ▼
Git Push
     │
     ▼
GitHub
     │
     ▼
Webhook
     │
     ▼
Jenkins
     │
     ▼
Docker Build
     │
     ▼
Amazon ECR
     │
     ▼
Amazon EKS
     │
     ▼
Helm Upgrade
```

---

# 📋 Jenkins Pipeline

Pipeline Stages

- Checkout Source
- Build Frontend Image
- Build Hello Service Image
- Build Profile Service Image
- Verify AWS Credentials
- Login Amazon ECR
- Tag Docker Images
- Push Images to Amazon ECR

---

# 📊 AWS Services Used

- IAM
- EC2
- ECR
- EKS
- CloudWatch
- CloudWatch Logs
- VPC
- Security Groups
- Auto Scaling Groups
- Elastic Load Balancer

---

# 🖥 Verification Commands

### Kubernetes

```bash
kubectl get nodes
```

```bash
kubectl get pods
```

```bash
kubectl get svc
```

```bash
helm list
```

---

### Jenkins

Verified

- Successful Pipeline Execution
- Automatic Webhook Trigger

---

### CloudWatch

Verified

- Container Insights
- Cluster Monitoring
- Node Monitoring
- Pod Monitoring

---

# 📷 Project Screenshots

The following screenshots are included in the repository.

- GitHub Repository
- Jenkins Dashboard
- Jenkins Successful Pipeline
- GitHub Webhook
- Amazon ECR Repositories
- EKS Cluster
- kubectl get nodes
- kubectl get pods
- kubectl get svc
- Helm Deployment
- Frontend Application
- CloudWatch Container Insights
- CloudWatch Agent Pods

---

# ✅ Project Outcome

Successfully implemented a complete DevOps CI/CD pipeline for a MERN application using AWS services.

Achievements

✔ Git Version Control

✔ Docker Containerization

✔ Amazon ECR

✔ Jenkins CI/CD

✔ GitHub Webhook Automation

✔ Amazon EKS Deployment

✔ Helm Package Management

✔ CloudWatch Monitoring

✔ Centralized Logging

✔ Automated Image Deployment

---

# 👨‍💻 Author

**Rupesh Borole**
