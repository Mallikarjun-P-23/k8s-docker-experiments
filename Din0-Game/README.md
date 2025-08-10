# 🦕 Chrome Dino Game - Kubernetes Deployment

A simple Kubernetes deployment of the classic Chrome Dino Game using NGINX as a web server.

## 📋 Project Overview

This project demonstrates how to:
- Containerize a static HTML game using Docker and NGINX
- Deploy the application to Kubernetes with 3 replica pods
- Expose the service using NodePort for browser access
- Manage the deployment lifecycle

## 📁 Project Structure

```
Din0-Game/
├── Dockerfile              # Docker configuration for NGINX container
├── index.html              # Chrome Dino Game HTML file
├── dino-deployment.yaml     # Kubernetes deployment and service manifests
└── README.md               # This file
```

## 🛠️ Prerequisites

Before starting, ensure you have the following tools installed:

- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

## 🚀 Deployment Steps

### Step 1: Start Minikube Cluster

```bash
# Start Minikube with Docker driver
minikube start --driver=docker
```

### Step 2: Configure Docker Environment

```bash
# Set Docker environment to use Minikube's Docker daemon
eval $(minikube docker-env)
```

### Step 3: Build Docker Image

```bash
# Build the Docker image locally
docker build -t dino-nginx .
```

### Step 4: Deploy to Kubernetes

```bash
# Apply the deployment and service manifests
kubectl apply -f dino-deployment.yaml
```

### Step 5: Verify Deployment

```bash
# Check if pods are running
kubectl get pods

# Check service status
kubectl get services

# Get detailed information about the deployment
kubectl get deployment dino-deploy
```

### Step 6: Access the Game

```bash
# Get the service URL
minikube service dino-service --url
```

Open the URL in your browser to play the Chrome Dino Game!

## 🎮 How to Play

- Press **SPACEBAR** or **UP ARROW** to make the dino jump
- Avoid the cacti and pterodactyls
- Try to achieve the highest score!

## 📊 Kubernetes Resources

### Deployment Configuration
- **Name**: `dino-deploy`
- **Replicas**: 3
- **Container Image**: `dino-nginx`
- **Container Port**: 80

### Service Configuration
- **Name**: `dino-service`
- **Type**: NodePort
- **Port**: 80
- **NodePort**: 30001
- **Target Port**: 80

## 🔍 Troubleshooting

### Check Pod Status
```bash
kubectl describe pods
```

### View Pod Logs
```bash
kubectl logs -l app=dino
```

### Check Service Endpoints
```bash
kubectl get endpoints dino-service
```

### Access via NodePort (Alternative)
```bash
# Get Minikube IP
minikube ip

# Access via: http://<minikube-ip>:30001
```

## 🧹 Cleanup Commands

When you're done playing, clean up the resources:

```bash
# Delete the deployment and service
kubectl delete -f dino-deployment.yaml

# Stop Minikube
minikube stop

# Delete Minikube cluster (optional)
minikube delete
```

## 📝 Additional Commands

### Scale the Deployment
```bash
# Scale to 5 replicas
kubectl scale deployment dino-deploy --replicas=5

# Scale back to 3 replicas
kubectl scale deployment dino-deploy --replicas=3
```

### Update the Game
```bash
# If you modify index.html, rebuild and redeploy
docker build -t dino-nginx .
kubectl rollout restart deployment dino-deploy
```

## 🎯 Learning Objectives

This project helps you understand:
- Docker containerization of static web applications
- Kubernetes Deployments and ReplicaSets
- Kubernetes Services and NodePort exposure
- kubectl command-line operations
- Local development with Minikube

## 🤝 Contributing

Feel free to fork this project and submit pull requests for improvements!

## 📄 License

This project is for educational purposes. The Chrome Dino Game is inspired by the original Chrome offline game.