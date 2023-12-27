# LAB 2: deployment files
Kubernetes configuration files are YAML or JSON files used to define and manage Kubernetes resources, such as pods, deployments, services, etc. These files contain specifications that describe the desired state of the resources you want to create or modify within a Kubernetes cluster.

Here are some key components and sections commonly found in Kubernetes configuration files:
- API Version: Specifies the version of the Kubernetes API that the object uses.
-Kind: Defines the type of Kubernetes resource being created, such as Pod, Deployment, Service, etc.
- Metadata: Contains information like the name, labels, and annotations for the resource.
- Spec: Describes the desired state of the resource. This section varies based on the resource type. For example:
    Pods: Contains specifications for containers, volumes, and other settings.
    Deployments: Includes information about replicas, pod templates, update strategies, etc.
    Services: Defines how the service should be exposed, its ports, selectors, etc.

- Selectors: Often used in conjunction with services or controllers to define how resources are associated or targeted.

- Annotations: Additional information or metadata that can be added to the resource for various purposes like documentation, tooling, etc.