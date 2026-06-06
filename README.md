# Kubernetes Voting Application on AWS EKS

## Project Overview

This project demonstrates the deployment of a multi-tier containerized voting application on Amazon EKS (Elastic Kubernetes Service). The application consists of multiple microservices communicating through Redis and PostgreSQL while being managed by Kubernetes Deployments and Services.

The objective of this project was to gain hands-on experience with Kubernetes concepts such as Deployments, Services, Labels, Selectors, Pod Networking, Service Discovery, and application troubleshooting in a production-like environment.

---

## Architecture

The application consists of the following components:

* Voting Application (Frontend)
* Redis (In-memory data store)
* Worker Service
* PostgreSQL Database
* Result Application (Frontend)

Application Flow:

Vote App → Redis → Worker → PostgreSQL → Result App

---

## Technologies Used

* Amazon Web Services (AWS)
* Amazon EKS
* EC2
* Kubernetes
* Docker
* Redis
* PostgreSQL
* AWS CLI
* kubectl
* eksctl
* Git & GitHub

---

## Kubernetes Resources

The project includes the following Kubernetes manifests:

| File                      | Description                   |
| ------------------------- | ----------------------------- |
| 1-voting-app-pod.yaml     | Voting Application Deployment |
| 2-voting-app-service.yaml | Voting Application Service    |
| 3-redis-pod.yaml          | Redis Deployment              |
| 4-redis-service.yaml      | Redis Service                 |
| 5-postgres-pod.yaml       | PostgreSQL Deployment         |
| 6-postgres-service.yaml   | PostgreSQL Service            |
| 7-result-app-pod.yaml     | Result Application Deployment |
| 8-result-app-service.yaml | Result Application Service    |
| 9-worker-app-pod.yaml     | Worker Application Deployment |

---

## Deployment Steps

### Create EKS Cluster

```bash
eksctl create cluster \
  --name voting-cluster \
  --region us-east-1 \
  --nodegroup-name workers \
  --node-type t3.medium \
  --nodes 2
```

### Configure kubectl

```bash
aws eks update-kubeconfig \
  --region us-east-1 \
  --name voting-cluster
```

### Deploy Application

```bash
kubectl apply -f .
```

### Verify Resources

```bash
kubectl get pods
kubectl get svc
kubectl get deployments
```

---

## Troubleshooting Performed

During implementation, several issues were identified and resolved:

### AWS CLI Pager Issue

* AWS CLI attempted to use the default pager.
* Resolved by disabling CLI pager.

### kubectl Installation Issue

* kubectl was not available in PATH.
* Installed and verified using kubectl version.

### Deployment Selector Immutability

* Encountered immutable selector error while modifying deployment labels.
* Resolved by recreating the deployment.

### PostgreSQL Authentication Failure

* Worker service failed to authenticate with PostgreSQL.
* Corrected database credentials and redeployed components.

### Service Selector Mismatch

* Result application service selector did not match pod labels.
* Updated labels and redeployed application.

### Application Connectivity Validation

* Used logs, endpoints, services, selectors, and pod labels to perform root cause analysis.

---

## Key Kubernetes Concepts Practiced

* Deployments
* ReplicaSets
* Pods
* Services
* LoadBalancer Services
* ClusterIP Services
* Labels and Selectors
* Service Discovery
* Pod Networking
* Application Logging
* Troubleshooting and Root Cause Analysis

## Learning Outcomes

* Successfully deployed a multi-tier application on Amazon EKS.
* Understood Kubernetes service communication patterns.
* Practiced troubleshooting application and infrastructure issues.
* Learned the importance of labels, selectors, endpoints, and service discovery.
* Gained hands-on experience with real-world Kubernetes debugging scenarios.

---

## Author

Lohith Tallapudi

DevOps Engineer | AWS | Kubernetes | Docker | Terraform | CI/CD

