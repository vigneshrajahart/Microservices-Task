##Microservices-Task — Kubernetes & Minikube Deployment##
Overview

This document provides detailed instructions for deploying and testing the User, Product, Order, and Gateway services using Kubernetes inside a Minikube cluster.
Each service runs as a separate deployment and communicates internally using ClusterIP Services.

Services and Endpoints
User Service

Service Name: user-service

Cluster URL: http://user-service:3000

Port: 3000

Endpoints:

List Users:

curl http://user-service:3000/users


If accessed via port-forward:

curl http://localhost:3000/users

Product Service

Service Name: product-service

Cluster URL: http://product-service:3001

Port: 3001

Endpoints:

List Products:

curl http://product-service:3001/products


If accessed via port-forward:

curl http://localhost:3001/products

Order Service

Service Name: order-service

Cluster URL: http://order-service:3002

Port: 3002

Endpoints:

List Orders:

curl http://order-service:3002/orders


If accessed via port-forward:

curl http://localhost:3002/orders

Gateway Service

Service Name: gateway-service

Cluster URL: http://gateway-service:3003/api

Port: 3003

Endpoints:

Users:

curl http://gateway-service:3003/api/users


Products:

curl http://gateway-service:3003/api/products


Orders:

curl http://gateway-service:3003/api/orders


If accessed via port-forward:

curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

Minikube Setup and Deployment Instructions
1. Start Minikube
minikube start --cpus=2 --memory=4096

2. Configure Docker to use Minikube’s Environment

For Linux/Mac:

eval $(minikube -p minikube docker-env)


For Windows PowerShell:

& minikube -p minikube docker-env --shell powershell | Invoke-Expression

3. Build Docker Images

Run the following commands from the project root:

docker build -t user-service:1.0 ./Microservices/user-service
docker build -t product-service:1.0 ./Microservices/product-service
docker build -t order-service:1.0 ./Microservices/order-service
docker build -t gateway-service:1.0 ./Microservices/gateway-service

4. Apply Kubernetes Manifests
kubectl apply -f k8s/deployments-and-services.yaml

5. Verify Deployments and Services
kubectl get pods
kubectl get svc


You should see all four pods and their respective services running successfully.

Testing Services
Option 1: Test via Port Forwarding

Forward the gateway service to access all APIs externally:

kubectl port-forward svc/gateway-service 3003:3003


Then run the following commands in another terminal:

curl http://localhost:3003/api/users
curl http://localhost:3003/api/products
curl http://localhost:3003/api/orders

Option 2: Test Within the Cluster

You can also test inter-service communication directly inside the gateway pod.

# Get the gateway pod name
kubectl get pods -l app=gateway-service

# Connect to the pod
kubectl exec -it <gateway-pod-name> -- /bin/sh


Then test inside the pod:

curl http://user-service:3000/users
curl http://product-service:3001/products
curl http://order-service:3002/orders

Logs and Verification

To verify service communication:

kubectl logs -l app=gateway-service
kubectl logs -l app=user-service
kubectl logs -l app=product-service
kubectl logs -l app=order-service


Check for successful API calls and responses in the logs.

Troubleshooting
Issue	Cause	Solution
ImagePullBackOff	Image not available in Minikube	Run eval $(minikube docker-env) before building images
CrashLoopBackOff	Port or env variable issue	Check logs with kubectl logs <pod-name>
Probe failing	Application startup delay	Increase initialDelaySeconds in probes
Gateway not routing	Incorrect URLs	Verify internal service URLs in gateway deployment
Service not reachable	Pod not ready or DNS issue	Run kubectl get endpoints and check readiness
Redeployment

If you modify any service code or Dockerfile:

docker build -t user-service:1.0 ./Microservices/user-service
kubectl rollout restart deployment/user-service


Repeat for the other services if needed.

Screenshots to Include in Submission

Include the following screenshots:

Output of kubectl get pods showing all pods in Running state

Output of kubectl get svc showing all ClusterIP services

Gateway service logs showing API routing

Results of curl commands for each API

Optional: Minikube dashboard screenshot

Save them in your documentation file:

Screenshots to Include in Submission.docx

Folder Structure
MICROSERVICES-TASK/
│
├── Microservices/
│   ├── user-service/
│   ├── product-service/
│   ├── order-service/
│   └── gateway-service/
│
├── k8s/
│   └── deployments-and-services.yaml
│
├── docker-compose.yml
├── README.md
└── Screenshots to Include in Submission.docx

Evaluation Summary
Section	Description	Marks
Deployments	Kubernetes manifests for all services	18
Services	Proper ClusterIP configuration	12
Minikube Setup & Validation	Successful setup and communication	15
Documentation & Testing	README and screenshots	5
Total	End-to-End Project	50 Marks
Author

Name: Vignesh Rajahart
Project: Microservices Task — Kubernetes & Minikube Deployment
Date: October 2025
Tools Used: Docker, Kubernetes, Minikube, kubectl