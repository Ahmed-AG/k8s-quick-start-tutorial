# k8s-quick-start-tutorial

Welcome to this quick start tutorial about Kubertenes (k8s).

# Intorduction
Kubernetes, often abbreviated as K8s, is an open-source container orchestration platform. It automates the deployment, scaling, and management of containerized applications. Originally developed by Google, Kubernetes has gained widespread adoption in managing containerized workloads and services.

## Basic Kubernetes Components:

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

# Example: Building a Frontend and Backend sample application 
## Detailed Track:

Follow the following labs to build the application:
- [Lab 0](./lab0.md)
- [Lab 1](./lab1.md)
- [Lab 2](./lab2.md)
- [Lab 3](./lab3.md)
- [Lab 4](./lab4.md)

## Fast Track:
These are the commands needed to build the entire application:
### Create the secret (DB Username and Password)
```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
### Create Backend, ConfigMap and FrontEnd
```bash
kubectl apply -f example1-mogoApp/backend-mongo-db.yaml
kubectl apply -f example1-mogoApp/mongodb-configmap.yaml
kubectl apply -f example1-mogoApp/frontend-mongo-express.yaml
```
### Expose the Frontend Service
```bash
minikube service frontend-mongo-express
```
# Cleanup 

```bash
minikube delete
```


<------>

### delete with config
```bash
kubectl delete -f nginx.yaml
```

