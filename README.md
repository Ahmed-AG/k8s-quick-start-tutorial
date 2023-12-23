# k8s-quick-start-tutorial

Welcome to this quick start tutorial about Kubertenes (k8s).

# Concepts and components
Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications. Originally developed by Google, Kubernetes has gained widespread adoption in managing containerized workloads and services.

## Basic Components include:

    - Pods: The smallest deployable unit in Kubernetes, consisting of one or more containers that share storage and networking. They're scheduled together on the same node. It is an abstraction over the container run time, Docker for

    - Nodes: These are the individual machines (physical or virtual) in a Kubernetes cluster where containers are deployed. Each node has services to run applications in the form of pods.

    - Clusters: A set of nodes that work together. Clusters are the foundation of Kubernetes; they consist of at least one master node and multiple worker nodes.

    - Master Node: Controls the Kubernetes cluster and manages its workload. It coordinates all activities in the cluster such as scheduling, scaling, and updating applications.

    - Kubelet: An agent running on each node that communicates with the master node and manages the pods and containers on the node.

    - Kube-proxy: Maintains network rules on nodes. It enables communication between different pods and services within the cluster.

    - Controller Manager: Manages controller processes that regulate the state of the cluster, such as deployments, replica sets, and stateful sets.

    - Scheduler: Assigns pods to nodes based on resource requirements and other constraints.

    - Etcd: A distributed key-value store that stores the cluster's configuration data, representing the state of the cluster at any given time.

These components work together to ensure that applications run efficiently, are scalable, and can easily be managed in a containerized environment.
# MiniKube
### install hyperhit and minikube

bash
brew install minikube
kubectl
minikube

### create minikube cluster
```bash
minikube start --vm-driver=hyperkit

kubectl get nodes

minikube status

kubectl version
```

### delete cluster and restart in debug mode
```bash
minikube delete

minikube start

minikube status
```

# Basic commands


### kubectl commands
```bash
kubectl get nodes

kubectl get pod

kubectl get services

kubectl create deployment nginx --image=nginx

kubectl get deployment

kubectl get replicaset

kubectl edit deployment nginx
```

### Logs
```bash
kubectl logs <pod-name>
```

### Exec commands
```bash
kubectl exec -it <pod-name> -- bin/bash
```

### create or edit config file
```bash
vim nginx.yaml

kubectl apply -f nginx.yaml

kubectl get pod

kubectl get deployment
```
### delete with config
```bash
kubectl delete -f nginx.yaml
```
# Deployments and Services

# Example Application 1