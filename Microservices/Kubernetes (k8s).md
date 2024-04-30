
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

#### Basic commands with kubernetes

##### Working with Pods
1. **kubectl version**: check to see if kubectl is installed and it's installed version.
2. **kubectl get pods** : list running pods
3. **kubectl apply -f [route-to-the-config-file]** : this will process the config file.
4. **kubectl exet -it [name-of-pod]  [command]** : run a command inside a running pod, if multiple containers are running inside a pod, kubectl will ask for the container name.
5. **kubectl logs [pod-name]** : list the logs to a running pod.
6. **kubectl delete [pod-name]** : delete a pod.
7. **kubectl describe pod [pod-name]** : will list information to a specific pod.

##### Working with Deployment
1. **kubectl get deployments** : list running pods
2. **kubectl apply -f [route-to-the-config-file]** : this will process the config file.
3. **kubectl logs [deployment-name]** : list the logs to a running pod.
4. **kubectl delete [deployment-name]** : delete a pod.
5. **kubectl describe deployment [deployment-name]** : will list information to a specific pod.
6. __kubectl rollout restart deployment__ [deployment-name] : restart a running deployment.

#### Types of services.

1. __cluster IP__ : set up an easy to remember url for a pod, only expose it inside a cluster
2. __Node Port__ : Makes a port accessible from outside a cluster. Usually used for dev purposes.
3. __Load Balancer__ : Makes a port accessible from outside of a cluster. Recommended way!
4. __External Name__ : Don't know.
   
