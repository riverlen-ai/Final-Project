# Flask Application Deployment on Kubernetes

## with Jenkins CI/CD & Helm

This project demonstrates an **end-to-end DevOps flow** for deploying a Flask application on Kubernetes using **Docker, Helm, and Jenkins CI/CD**.

---

## Part 1 – Flask Application on Kubernetes (Minikube)

### Overview

A simple Flask application is containerized and deployed on a Kubernetes cluster running on Minikube using standard Kubernetes resources.

### Kubernetes Components

* **Deployment** – Runs the Flask application pods
* **Service (LoadBalancer)** – Exposes the application externally
* **ConfigMap** – Application configuration
* **Secret** – Sensitive data
* **Liveness & Readiness Probes** – Health checks
* **CronJob** – Periodic API trigger

### Access the Application

```bash
minikube service myflask-service --url
```

### Prerequisites

* Minikube
* kubectl
* Docker
* Python 3.10+

---

## Part 2 – Containerization

* Flask application packaged using a **Dockerfile**
* Docker image built locally or via CI
* Image used by the Kubernetes Deployment

---

## Part 3 – Helm Chart

The application is packaged as a **Helm Chart** to enable:

* Versioned releases
* Consistent deployments
* Centralized configuration via `values.yaml`

### Helm Templates Include

* Deployment
* Service
* ConfigMap & Secret
* Horizontal Pod Autoscaler (HPA)

---

## Part 4 – CI/CD with Jenkins

### Jenkins Pipeline (Jenkinsfile)

The Jenkins pipeline runs on **Kubernetes-based Jenkins agents** and includes the following stages:

1. **Build** – Build Docker image
2. **Test** – Run Python tests with pytest
3. **Lint** – Validate Helm chart using `helm lint`
4. **Deploy** – Deploy or upgrade using Helm

```bash
helm upgrade --install final-project ./helm/final-project
```

---

## Part 5 – Security & RBAC

To allow Jenkins to deploy resources into Kubernetes:

### ServiceAccount

* A dedicated ServiceAccount named `helm-deployer`
* Located in the Jenkins namespace
* Used by Jenkins agent pods

### RBAC Configuration

* **Role** with permissions for:

  * Deployments
  * Services
  * ConfigMaps
  * Secrets
  * HorizontalPodAutoscalers (autoscaling)
* **RoleBinding** connects the Role to the ServiceAccount

### Usage in Jenkinsfile

```groovy
serviceAccount 'helm-deployer'
```

This ensures Jenkins has the required permissions to run Helm deployments.

---

## Architecture Diagram (Logical Flow)

```
Developer
   |
   v
GitHub Repository
   |
   v
Jenkins Pipeline (Kubernetes Agent)
   |
   |-- Build Docker Image
   |-- Run Tests (pytest)
   |-- Helm Lint
   |
   v
Helm
   |
   v
Kubernetes Cluster (Minikube)
   |
   |-- Deployment
   |-- Service
   |-- ConfigMap
   |-- Secret
   |-- HPA
   |-- CronJob
```

---

## Summary

This project demonstrates:

* Flask application deployment on Kubernetes
* Docker-based containerization
* Helm-based release management
* Full CI/CD automation using Jenkins
* Secure Kubernetes access using ServiceAccounts and RBAC

It represents a complete **DevOps pipeline from code to production-like deployment**.

---

If you want, I can also:

* Shorten this into a **submission-ready README**
* Convert it into **slides**
* Create a **visual architecture diagram (Mermaid / Draw.io)**
