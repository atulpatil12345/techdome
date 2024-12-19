# Kubernetes Deployment and Service Setup

This guide provides instructions for deploying a React app with a backend API and a MongoDB database using Kubernetes. The provided YAML files define the deployments and services for the frontend, backend, and database components.

## Prerequisites

- Kubernetes cluster (e.g., Minikube)
- kubectl installed and configured to access your Kubernetes cluster


### a. Apply the  Deployment and services

kubectl apply -f backend-deployment.yaml
kubectl apply -f db-deployment.yaml
kubectl apply -f frontend-deployment.yaml
kubectl apply -f backend-service.yaml 
kubectl apply -f db-service.yaml
kubectl apply -f frontend-service.yaml
