# **Overview**
This project demonstrates the deployment of a full-stack Movie Application on a Kubernetes cluster using AWS Elastic Kubernetes Service (EKS).

It includes:

1. React frontend
2. Backend API service
3. Docker containerization
4. Kubernetes orchestration
5. AWS Load Balancer exposure
6. IAM-based cluster authentication
7. Real-world debugging of cloud infrastructure issues

---

## **Architecture**
```
User
  ↓
AWS Load Balancer
  ↓
Kubernetes Service (Frontend / Backend)
  ↓
Pods (React Frontend + Backend API)

```
---

## **Tech Stack**

1. Kubernetes (EKS)
2. AWS (IAM, EC2, Load Balancer, VPC)
3. Docker
4. kubectl
5. React (Frontend)
6. Node.js / Spring Boot (Backend)
7. OpenLens (Cluster Visualization)

--- 

## **Project Structure**

```
movie-app-deployment/
│
├── k8s/
│   ├── frontend-deployment.yaml
│   ├── backend-deployment.yaml
│   └── namespace.yaml
│
└── services/
    ├── frontend-service.yaml
    └── backend-service.yaml
```
---

# **Deployment Workflow**
1. ## Create Kubernetes Cluster
 ```
 Bash

 eksctl create cluster --name solomon-prod-cluster --region us-east-1

```




