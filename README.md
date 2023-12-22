# k8s-quick-start-tutorial

# Concepts and components

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