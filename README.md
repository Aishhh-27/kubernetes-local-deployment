# Kubernetes Local Deployment with Minikube

## Project Overview

This project demonstrates how to deploy a **containerized Python Flask application** on a local Kubernetes cluster using **Minikube**.

The goal is to showcase core Kubernetes concepts such as **Deployments, Services, Ingress, ConfigMaps, Secrets, and Horizontal Pod Autoscaling (HPA)**.

The entire setup runs **locally without any cloud provider**, making it ideal for learning and demonstrating Kubernetes fundamentals.

---

# Architecture

Dockerized Flask App
↓
Kubernetes Deployment
↓
Kubernetes Service (NodePort)
↓
Ingress Controller
↓
Browser / Curl Request

---

# Tech Stack

* Docker
* Kubernetes
* Minikube
* kubectl
* Python (Flask)

---

# Project Structure

```
kubernetes-local-deployment
│
├── app
│   ├── app.py
│   └── requirements.txt
│
├── Dockerfile
│
└── k8s
    ├── deployment.yaml
    ├── service.yaml
    ├── configmap.yaml
    ├── secret.yaml
    ├── ingress.yaml
    └── hpa.yaml
```

---

# Prerequisites

Install the following tools:

* Docker
* kubectl
* Minikube

Verify installation:

```
docker --version
kubectl version --client
minikube version
```

---

# Start Kubernetes Cluster

```
minikube start --driver=docker
```

Verify cluster:

```
kubectl get nodes
```

---

# Build Docker Image

Use Minikube's Docker environment:

```
eval $(minikube docker-env)
```

Build image:

```
docker build -t flask-k8s-app .
```

---

# Deploy Kubernetes Resources

Apply ConfigMap:

```
kubectl apply -f k8s/configmap.yaml
```

Apply Secret:

```
kubectl apply -f k8s/secret.yaml
```

Deploy application:

```
kubectl apply -f k8s/deployment.yaml
```

Create service:

```
kubectl apply -f k8s/service.yaml
```

---

# Verify Deployment

Check pods:

```
kubectl get pods
```

Check services:

```
kubectl get svc
```

---

# Access Application

Get service URL:

```
minikube service flask-service --url
```

Example:

```
http://127.0.0.1:40591
```

Open this URL in a browser to access the application.

Expected output:

```
Hello from Kubernetes! ENV=development
```

---

# Enable Ingress

Enable ingress controller:

```
minikube addons enable ingress
```

Deploy ingress resource:

```
kubectl apply -f k8s/ingress.yaml
```

---

# Horizontal Pod Autoscaler

Enable metrics server:

```
minikube addons enable metrics-server
```

Apply autoscaler:

```
kubectl apply -f k8s/hpa.yaml
```

Check autoscaling:

```
kubectl get hpa
```

---

# Kubernetes Resources Used

This project demonstrates the following Kubernetes components:

* Deployment
* Service
* Ingress
* ConfigMap
* Secret
* Horizontal Pod Autoscaler

---

# Example Output

Pods running:

```
kubectl get pods
```

Service running:

```
kubectl get svc
```

Autoscaler status:

```
kubectl get hpa
```

---

# Learning Outcomes

* Containerizing applications using Docker
* Deploying applications to Kubernetes
* Managing configuration with ConfigMaps
* Securing sensitive data using Secrets
* Exposing services using NodePort and Ingress
* Scaling workloads automatically with HPA

---

# Future Improvements

* Helm chart for application deployment
* CI/CD pipeline with GitHub Actions
* Deployment to cloud Kubernetes (EKS / GKE)

---

# Author

Aishwarya Ganesh
