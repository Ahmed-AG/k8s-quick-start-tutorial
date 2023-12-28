# Task 5: Namespaces
`Namespaces` are a way to divide cluster resources between multiple users, teams, or projects. They provide a scope for Kubernetes objects, such as pods, services, and replication controllers, within a cluster.

Namespaces are useful for organizing and isolating resources, allowing different teams or projects to operate independently within the same Kubernetes cluster without interfering with each other. They help in avoiding naming collisions and provide a level of resource isolation and security.

By default, Kubernetes has a 'default' namespace, but you can create multiple namespaces to logically segregate and manage your resources more effectively. Each namespace operates as a separate virtual cluster within the larger Kubernetes cluster, enabling teams to work in their dedicated space without conflicting with others.
