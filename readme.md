# Kubernetes Frontend-Backend Demo
## Overview
### This project demonstrates a simple two-tier application deployed on Kubernetes
- **Frontend**: Serves the web application.
- **Backend**: Provides an API endpoint that returns a success response.
- **Services**: Enable communication between frontend and backend.
- **Ingress**: Exposes the frontend and backend to the outside world using a single domain.

## Architecture
```
Browser
   │
   ▼
Ingress Controller (nginx)
   ├── /      → frontend-service → frontend Pod(s)
   └── /api   → backend-service  → backend Pod(s)
```
## Files

- **frontend-pod.yaml** → Deployment for frontend pods
- **frontend-service.yaml** → ClusterIP service for frontend
- **backend-pod.yaml** → Deployment for backend pods
- **backend-service.yaml** → ClusterIP service for backend
- **ingress-config.yaml** → Ingress routing / → frontend and /api → backend

  ## apply steps

## create pod

# frontend pod 
```
kubectl create -f frontend-pod.yaml
```
# backend pod 
```
kubectl create -f backend-pod.yaml
```
# to check the pods
```
kubctl get pods
```
# frontend service 
```
kubectl create -f frontend-service.yaml
```
# frontend pod 
```
kubectl create -f backend-service.yaml
```
# to check the services
```
kubectl get svc(or service)
```
# to apply the ingress to expose the application to public
```
kubectl create -f ingress-config.yaml
```
# to get the public domain name 
```
kubectl get ingress
```
# output
```
NAME              CLASS   HOSTS   ADDRESS                          PORTS   AGE
frontend-ingress  nginx   *       <your public domain name >  80      5m

```
