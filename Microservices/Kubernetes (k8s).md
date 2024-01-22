
## Getting started with Kubernetes.
#### Introduction
Kubernetes is a container manager that helps us create, manage & monitor docker containers with ease. It's an open-source system that automates deploying, scaling, and managing containerized applications.



#### key components

1. **Container**: A lightweight, standalone, and executable software package that contains everything needed to run a piece of software, including the code, runtime, system tools, libraries, and settings. Containers are isolated from each other and the host system. (specific to docker)
2. **Pods**: The smallest and simplest unit in the Kubernetes object model. A pod represents a single unit of deployment—a single instance of a running process in a cluster. Pods can encapsulate one or multiple containers. Containers within the same pod share the same IP address, different port space, and storage.
3. **Nodes**: These are the worker machines (can be either a physical or virtual machine) that run containers. Each node is managed by the master node. A node can run multiple pods.
4. **Service**: An abstract way to expose an application running on a set of pods as a network service. Even if pods die or are replaced, the service ensures the application remains accessible.
5. **Deployment**: A higher-level construct that ensures the desired number of pod replicas are maintained. If a pod goes down, the deployment will create a new one to replace it.
6. **Cluster**: A set of nodes grouped together. This is the entirety of your Kubernetes setup, usually consisting of one master node that controls multiple worker nodes.
