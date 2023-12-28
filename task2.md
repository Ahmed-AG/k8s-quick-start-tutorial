# Task 2: Building a sample application

Kubernetes support building infrastrucure using configuration files. K8s configuration files are YAML or JSON files used to define and manage Kubernetes resources, such as pods, deployments, services, etc. These files contain specifications that describe the desired state of the resources you want to create or modify within a Kubernetes cluster.

Here are some key components and sections commonly found in Kubernetes configuration files:
- API Version: Specifies the version of the Kubernetes API that the object uses.
-Kind: Defines the type of Kubernetes resource being created, such as Pod, Deployment, Service, etc.
- Metadata: Contains information like the name, labels, and annotations for the resource.
- Spec: Describes the desired state of the resource. This section varies based on the resource type. For example:
  - Pods: Contains specifications for containers, volumes, and other settings.
  - Deployments: Includes information about replicas, pod templates, update strategies, etc.
  - Services: Defines how the service should be exposed, its ports, selectors, etc.
- Selectors: Often used in conjunction with services or controllers to define how resources are associated or targeted.
- Annotations: Additional information or metadata that can be added to the resource for various purposes like documentation, tooling, etc.

We have three configuration files being used for this tutorial. You can find them [here](./example1-mongoApp/)

# Build a sample application
In this example, we will build a sample application that consists of the following:
1. A MongoDB as the `Backend` and. Accessable only for the front end and consists of one Pod
2. A Mongo-express as the `Frontend`. Accessiable from the outside and consits of one Pod

To do that, we will use three different configration files as follows:
- [./example1-mongoApp/backend-mongo-db.yaml](./example1-mongoApp/backend-mongo-db.yaml): Will create a Deployment and a Service for the backend
- [./example1-mongoApp/frontend-mongo-express.yaml](./example1-mongoApp/frontend-mongo-express.yaml): Will create a Deployment and a Service for the frontend
- [./example1-mongoApp/mongodb-configmap.yaml](./example1-mongoApp/mongodb-configmap.yaml): Will create ConfigMap that will have the backend's name
- Finally, we will create `sectret` that has the Database user name and password. We will do that though the command line

We will begin with creating the secret.

# Creating the secret:
`Secrets` are a way to securely store sensitive information, such as passwords, tokens, or keys. They're designed to help manage sensitive data access within Kubernetes deployments. Secrets provide a layer of abstraction and security by encoding and storing sensitive information separately from pod definitions or application code.

Kubernetes secrets can be used by referencing them in pods or containers, allowing applications to access sensitive information without exposing it directly within the code or configuration files. Secrets are stored within the cluster etcd and can be accessed by authorized entities.

Both the backend and the frontend will need to access the secret we will create. On the backend we will need to set the username and password of the Database. And on the front end we will need to configure the right username and password to be used.

So, we will create two secrets:
- mongo-username
- mongo-password
Because we want to be able to do this in a pipeline, we chose to use the kubectl to create the secrets. Run the following (you can choose your password):

```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
To verify that the above was successful:
```bash
kubectl get secrets
```
```
$ kubectl get secrets
NAME             TYPE     DATA   AGE
mongodb-secret   Opaque   2      5d
```
You can also run:
```bash
kubectl describe secrets mongodb-secret
```
```
$ kubectl describe secrets mongodb-secret
Name:         mongodb-secret
Namespace:    default
Labels:       <none>
Annotations:  <none>

Type:  Opaque

Data
====
mongo-password:  9 bytes
mongo-username:  9 bytes
```
