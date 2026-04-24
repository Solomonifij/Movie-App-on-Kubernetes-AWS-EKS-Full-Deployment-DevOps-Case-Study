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
 </> Bash

 eksctl create cluster --name solomon-prod-cluster --region us-east-1

```
---

2. ## Configure Cluster Access
```
</> bash

aws eks update-kubeconfig --region us-east-1 --name solomon-prod-cluster

```
---

3. ## Create Namespace (Isolation Layer)
```
</> Bash
kubectl create namespace movie-app-ns
kubectl config set-context --current --namespace=movie-app-ns

```
---
4. ## Deploy Application
```
</> Bash

kubectl apply -f .

```
---

5. ## Expose Services via LoadBalancer
```
</> Bash

kubectl get svc

```
Access application via:

```
http://<EXTERNAL-LOADBALANCER-DNS>

```
---

# **Kubernetes Concepts Applied**
## Deployments

Used to manage:
1. Replica scaling
2. Self-healing pods
3. Rolling updates

## Services

Used to expose pods internally and externally:
1. ClusterIP (internal communication)
2. NodePort (debugging)
3. LoadBalancer (AWS external access)

## Namespace

Used to isolate application resources:
1. movie-app-ns for all workloads
---
# **Real-World Challenges & Debugging**
## 1. IAM Authentication Failure
### Problem:
```
Unauthorized access to EKS cluster
```
### Cause:

IAM user not properly mapped in cluster access configuration

### Solution:

1. Added IAM access entry
2. Attached AmazonEKSClusterAdminPolicy
---
## 2. LoadBalancer Timeout Issue
### Problem:
Frontend URL returned:
```
ERR_CONNECTION_TIMED_OUT
```
### Cause:
1. NodePort + Classic LoadBalancer misbehavior
2. Traffic not properly routed to frontend service

### Investigation:
```
</> Bash
kubectl describe svc frontend-service
kubectl get endpoints
kubectl get pods

```
--- 

## 3. Namespace Confusion in OpenLens
### Problem:
Pods not visible in UI
### Cause:
Wrong namespace filter selected
### Fix:
Switched OpenLens view to:
```
movie-app-ns

```
---
# Key Learnings

1. Kubernetes networking is more critical than deployment itself
2. IAM misconfiguration can completely block cluster access
3. LoadBalancer behavior differs from NodePort expectations
4. Namespaces improve debugging and organization significantly
5. Observability tools (OpenLens) depend heavily on correct context

---
# Future Improvements
1. Implement AWS ALB Ingress Controller (recommended upgrade)
2. Add CI/CD pipeline using GitHub Actions
3. Introduce Helm for reusable deployments
4. Add monitoring (Prometheus + Grafana)
5. Improve frontend reliability with proper health checks
---

# Cleanup (Cost Control)
To avoid AWS charges:
```
</> Bash

eksctl delete cluster --name solomon-prod-cluster --region us-east-1

```
---

```
</> Markdown

##  Application Access

The application was successfully deployed and exposed using AWS LoadBalancer during testing.

> Note: The EKS cluster and associated resources were deleted after completion to avoid ongoing cloud costs.

The deployment validated:
- Kubernetes service exposure
- Pod networking
- LoadBalancer routing
- Full-stack communication between frontend and backend

```
---

```
</> Markdown

##  Project Status

✔ Successfully deployed on AWS EKS  
✔ Fully functional during runtime  
✔ Infrastructure cleaned up after validation  
✔ Project retained as a reproducible Kubernetes setup

```

# Author
## Solomon Sele Atalokhai (Ifijeh0
Cloud & DevOps Engineer




