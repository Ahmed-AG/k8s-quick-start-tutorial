# k8s-quick-start-tutorial

Welcome to this quick start tutorial about Kubertenes (k8s).

## Learning Objectives
- Understand the different Kubernetes component
- Learn basic Kubernetes commands
- Build a sample Frontend and Backend application using Kubernetes

## Prerequisites

- Basic familiarity with Linux Bash commands
- Basic familiarity with Containers (This is a recommended [Docker Crash Course](https://github.com/Resistor52/DockerCrashCourse/blob/main/README.md)) 
- Any Virtual Machine

# Building a Frontend and Backend sample application 
## Detailed Track:

Follow the following tasks to build the application:
- [Task 0: Set up your testing environment](./task0.md)
- [Task 1: Basic kubectl commands](./task1.md)
- [Task 2: Building a sample application](./task2.md)
- [Task 3: Create the backend](./task3.md)
- [Task 4: Create the frontend](./task4.md)

## Fast Track:
Given that you have a K8s environment set, these are the commands needed to build the entire application:
### Create the secret (DB Username and Password)
```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
### Create Backend, ConfigMap and FrontEnd
```bash
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml
kubectl apply -f example1-mongoApp/frontend-mongo-express.yaml
```
Give it few minutes for all services to be created then move to the next step.

### Expose the Frontend Service
```bash
minikube service frontend-mongo-express
```
User `admin` and `pass` to login to Mongo-Express

# Cleanup 

```bash
minikube delete
```
