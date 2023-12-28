# k8s-quick-start-tutorial

Welcome to this quick start tutorial about Kubertenes (k8s).

## Learning Objectives
- Learn basic Kubernetes commands
- Understand the different Kubernetes component
- Build a sample Frontend and Backend apllication using Kubernetes

## Prerequisites

- Basic familiarity with Linux Bash commands
- Basic Familiarity with Containers
- Any Viritual Machine

# Building a Frontend and Backend sample application 
## Detailed Track:

Follow the following tasks to build the application:
- [Task 0: Set up you testing envinoment](./task0.md)
- [Task 1: Basic kubectl commands](./task1.md)
- [Task 2: Building a sample application](./task2.md)
- [Task 3: Create the backend](./task3.md)
- [Task 4: Create the frontend](./task4.md)

## Fast Track:
Given that you have a K8s envinroment set, these are the commands needed to build the entire application:
### Create the secret (DB Username and Password)
```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
### Create Backend, ConfigMap and FrontEnd
```bash
kubectl apply -f example1-mognoApp/backend-mongo-db.yaml
kubectl apply -f example1-mognoApp/mongodb-configmap.yaml
kubectl apply -f example1-mognoApp/frontend-mongo-express.yaml
```
### Expose the Frontend Service
```bash
minikube service frontend-mongo-express
```
# Cleanup 

```bash
minikube delete
```
