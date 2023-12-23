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

# Lab 0: Set up you testing envinoment
## MiniKube
Minikube is a tool that allows you to run a single-node Kubernetes cluster locally on your computer. It's designed to enable developers to learn and experiment with Kubernetes or to develop applications locally before deploying them to a larger Kubernetes cluster.

### TASK 1: Install Minikube

Follow the steps in the here to install and start Minikube: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)


## kubectl

`kubectl` is the command-line interface (CLI) used to interact with Kubernetes clusters. It allows users to execute commands against Kubernetes clusters to deploy applications, manage and inspect cluster resources, and perform various administrative tasks.

### TASK 2: Install kubectl
kubectl will be configured automatially to authenticate to Minikube during the minikube installation process (check `~/.kube/config`). However, you might still need to install `kubectl` itself. To install `kubectl` Follow the steps here:[https://kubernetes.io/docs/tasks/tools/]( https://kubernetes.io/docs/tasks/tools/)


# Lab 1: Basic `kubectl` commands
Let us explore our Minikube environment:
Run the help to learn about the basic commands:

```bash
kubectl -h
```
```bash
kubectl controls the Kubernetes cluster manager.

 Find more information at: https://kubernetes.io/docs/reference/kubectl/

Basic Commands (Beginner):
  create          Create a resource from a file or from stdin
  expose          Take a replication controller, service, deployment or pod and expose it as a new Kubernetes service
  run             Run a particular image on the cluster
  set             Set specific features on objects

Basic Commands (Intermediate):
  explain         Get documentation for a resource
  get             Display one or many resources
  edit            Edit a resource on the server
  delete          Delete resources by file names, stdin, resources and names, or by resources and label selector
...
```
Notice that we can create, delete, get and describe resources. We will later work with the following resources:
- Pods: An abstraction over a container run time such as Docker
- Deployments: we dont directly work with pods instead we create deployments that could have multple pods doing the same task
- Services: Provide way to access a set of deployments (and so pods), typically through an endpoint (IP Adress and Names)
- ConfigMaps: We will use ConfigmMps to store information that is needed accross deployments
- Secrets: Very similar to ConfigMaps except it is meant for secret values. We will use Secrets to store Database credentials.


1 - Let us create a deployment. The following command will instruct K8s to create a deployment and a pod with nginx docker container image `nginx`. It will set alot of defaults as well

```bash
kubectl create deployment nginx --image=nginx
```
Let us explore the deployment we created. Run the following command:

```bash
kubectl get deployment
```

```bash
NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
nginx                               1/1     1            1           14s
```

We can also explore more:
```bash
kubectl get pods
```
```bash
NAME                                                READY   STATUS    RESTARTS   AGE
nginx-7854ff8877-6wq4n                              1/1     Running   0          3m23s
```

We can use the `-o wide` option:

```bash
kubectl get pods -o wide
```

```
NAME                                                READY   STATUS    RESTARTS   AGE     IP            NODE       NOMINATED NODE   READINESS GATES
nginx-7854ff8877-6wq4n                              1/1     Running   0          5m11s   10.244.0.31   minikube   <none>           <none>
```

We can also `describe` resources using the command `kubectl describe pods <POD-NAME>`:

```bash
kubectl describe pods nginx-7854ff8877-6wq4n
```
```
Name:             nginx-7854ff8877-6wq4n
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.59.100
Start Time:       Fri, 22 Dec 2023 19:34:20 -0600
Labels:           app=nginx
                  pod-template-hash=7854ff8877
Annotations:      <none>
Status:           Running
IP:               10.244.0.31
IPs:
  IP:           10.244.0.31
Controlled By:  ReplicaSet/nginx-7854ff8877
Containers:
  nginx:
    Container ID:   docker://455c96e8e59fb29fd3aabe439de64c9e0b1b1de0dc691fd0389afbdab382a025
    Image:          nginx
...
```

```bash
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

# Cleanup 

```bash
minikube delete
```
