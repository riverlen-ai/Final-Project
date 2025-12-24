# Flask Application Deployment on Kubernetes (Minikube)

This project demonstrates how to deploy a simple Flask application on a Kubernetes cluster using Minikube.  
It includes Deployment, Service (LoadBalancer), ConfigMap, Secret, CronJob, and health probes.

---

## Project Structure

**Flask Application**
**Docker Image:** `lena2017/myflaskapp:02`
**Kubernetes Components:**
  Deployment
  Service (LoadBalancer)
  ConfigMap
  Secret
  Liveness & Readiness Probes
  CronJob that triggers the API
**Local Access via Minikube**

---

##  Prerequisites

Minikube  
kubectl  
Docker  
Python 3.10+

---

## Access the Application

minikube service myflask-service --url

