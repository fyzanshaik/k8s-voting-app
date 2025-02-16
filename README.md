# Kubernetes Voting Application Demo

This is a microservices-based voting application deployed on Kubernetes that demonstrates the interaction between different services to count and display votes in real-time.

## Architecture Overview

![Architecture Diagram](image/README/1739721477252.png)

## Components

The application consists of five main components:

1. **Voting Frontend**

   -  Python/ASP.NET Core web application
   -  Provides UI for users to cast votes
   -  Exposes port 80 for web traffic

2. **Redis Queue**

   -  Acts as a temporary storage
   -  Collects new votes
   -  Enables asynchronous processing

3. **Worker Service**

   -  Built with .NET Core/Java
   -  Consumes votes from Redis
   -  Processes and stores votes in the database
   -  Handles the business logic

4. **PostgreSQL Database**

   -  Persistent storage for votes
   -  Backed by Docker volume
   -  Stores the final voting results

5. **Result Frontend**
   -  Node.js/ASP.NET Core SignalR webapp
   -  Displays real-time voting results
   -  Updates automatically using WebSocket

## Kubernetes Resources

The application uses the following Kubernetes resources:

-  **Pods**

   -  voting-app-pod
   -  redis-pod
   -  worker-app-pod
   -  postgres-pod
   -  result-app-pod

-  **Services**
   -  voting-service (NodePort)
   -  redis (ClusterIP)
   -  worker (ClusterIP)
   -  db (ClusterIP)
   -  result-service (NodePort)

## Deployment

1. Create the pods:

```bash
kubectl create -f voting-app-pod.yaml
kubectl create -f redis-pod.yaml
kubectl create -f worker-app-pod.yaml
kubectl create -f postgres-pod.yaml
kubectl create -f result-app-pod.yaml
```

2. Create the services:

```bash
kubectl create -f voting-service.yaml
kubectl create -f redis-service.yaml
kubectl create -f postgres-service.yaml
kubectl create -f result-service.yaml
```

## Accessing the Application

-  Voting Interface: `http://<node-ip>:30005`
-  Results Interface: `http://<node-ip>:30004`

## Monitoring

Check the status of your pods:

```bash
kubectl get pods
kubectl get svc
```

## Troubleshooting

If pods are in CrashLoopBackOff or Error state:

```bash
kubectl logs <pod-name>
kubectl describe pod <pod-name>
```
