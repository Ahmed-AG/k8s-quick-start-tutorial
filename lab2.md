# LAB 2: deployment files
Kubernetes configuration files are YAML or JSON files used to define and manage Kubernetes resources, such as pods, deployments, services, etc. These files contain specifications that describe the desired state of the resources you want to create or modify within a Kubernetes cluster.

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

# Build a sample application
In this example, we will build a sample application that consists of the following:
- A MongoDB as the back end and. Accessable only for the front end and consists of one Pod
- A Mongo-express as the front end. Accessiable from the outside and consits of one Pod

To do that, we will use three different configration files as follows:
- (backend-mongo-db.yaml)[/example1-mongoApp/backend-mongo-db.yaml]