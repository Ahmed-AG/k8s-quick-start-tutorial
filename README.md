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

# K8s Quick Start Tutorial
## Detailed Track:

Follow the following tasks to build the application:
- [Task 0: Set up your testing environment](./task0.md){:target="_blank"}
- [Task 1: Basic kubectl commands](./task1.md){:target="_blank"}
- [Task 2: Building a sample application](./task2.md){:target="_blank"}
- [Task 3: Create the backend](./task3.md){:target="_blank"}
- [Task 4: Create the frontend](./task4.md){:target="_blank"}

## Fast Track:
Given that you have a K8s environment up and running, these are the commands needed to build the entire application:
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
You can check status of your pods by running `kubectl get po`. Or run `kubectl get all` to see all of your resources:
```bash
kubectl get all
```

### Expose the Frontend Service
Once your pods' status change from `ContainerCreating` to `running`, run the following to expose frontend-mongo-express
```bash
minikube service frontend-mongo-express
```
Use `admin` and `pass` to login to Mongo-Express

# Cleanup 

```bash
minikube delete
```
