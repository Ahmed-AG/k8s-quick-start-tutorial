# Task 0: Set up you testing envinoment
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

## MiniKube
Minikube is a tool that allows you to run a single-node Kubernetes cluster locally on your computer. It's designed to enable developers to learn and experiment with Kubernetes or to develop applications locally before deploying them to a larger Kubernetes cluster.

### Install Minikube

Follow the steps in the here to install and start Minikube: [https://minikube.sigs.k8s.io/docs/start/](https://minikube.sigs.k8s.io/docs/start/)


## kubectl

`kubectl` is the command-line interface (CLI) used to interact with Kubernetes clusters. It allows users to execute commands against Kubernetes clusters to deploy applications, manage and inspect cluster resources, and perform various administrative tasks.

### Install kubectl
kubectl will be configured automatially to authenticate to Minikube during the minikube installation process (check `~/.kube/config`). However, you might still need to install `kubectl` itself. To install `kubectl` Follow the steps here:[https://kubernetes.io/docs/tasks/tools/]( https://kubernetes.io/docs/tasks/tools/)
