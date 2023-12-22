# k8s-quick-start-tutorial

# Concepts and components

# MiniKube
### install hyperhit and minikube

`brew install minikube`

`kubectl`

`minikube`
### create minikube cluster
`minikube start --vm-driver=hyperkit`

`kubectl get nodes`

`minikube status`

`kubectl version`

### delete cluster and restart in debug mode
`minikube delete`

`minikube start`

`minikube status`

# Basic commands


### kubectl commands
`kubectl get nodes`

`kubectl get pod`

`kubectl get services`

`kubectl create deployment nginx --image=nginx`

`kubectl get deployment`

`kubectl get replicaset`

`kubectl edit deployment nginx`

### Logs
`kubectl logs <pod-name>`

### Exec commands
`kubectl exec -it <pod-name> -- bin/bash`


### create or edit config file
`vim nginx.yaml`

`kubectl apply -f nginx.yaml`

`kubectl get pod`

`kubectl get deployment`

### delete with config
`kubectl delete -f nginx.yaml`

# Deployments and Services

# Example Application 1