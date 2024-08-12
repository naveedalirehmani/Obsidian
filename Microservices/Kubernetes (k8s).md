


## Getting started with Kubernetes.
#### Introduction
Kubernetes is a container manager that helps us create, manage & monitor docker containers with ease. It's an open-source system that automates deploying, scaling, and managing containerized applications.

Kubernetes is a container orchestrator (like [ECS](https://newsletter.simpleaws.dev/p/simple-aws-4-ecs)), which means you define your services and the resources they need, and it will manage deploying them, scaling them, communication (networking, security) and management (logging, monitoring, etc). You focus on writing the code for your services, Kubernetes handles the ops side of things.

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
1. **kubectl get deployments** : list running deployments
2. **kubectl apply -f [route-to-the-config-file]** : this will process the config file.
3. **kubectl logs [deployment-name]** : list the logs to a running deployment.
4. **kubectl delete deployment [deployment-name]** : delete a deployment.
5. **kubectl describe deployment [deployment-name]** : will list information to a specific deployment.
6. __kubectl rollout restart deployment__ [deployment-name] : restart a running deployment.

#### Types of services.

1. __cluster IP__ : set up an easy to remember url for a pod, only expose it inside a cluster
2. __Node Port__ : Makes a port accessible from outside a cluster. Usually used for dev purposes.
3. __Load Balancer__ : Makes a port accessible from outside of a cluster. Recommended way!
4. __External Name__ : Don't know.
   
---

# [kubernetes-dashboard](http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy)

---

### ingress-nginx 

#### Why Do We Need `ingress-nginx`?

**HTTP and HTTPS Routing**:
`ingress-nginx` allows you to define rules for routing external HTTP and HTTPS traffic to services within your Kubernetes cluster. This makes it easier to expose your services to the outside world.
    
**Consolidated Entry Point**:
Instead of exposing each service with its own IP address or port, you can use an Ingress to manage multiple services under a single IP address and handle the routing based on hostnames or URL paths.
    
**Load Balancing**:
The Ingress controller can distribute incoming traffic across multiple instances of your services, ensuring better utilization and availability.
    
**SSL Termination**:
`ingress-nginx` can handle SSL termination, which means it can manage your SSL/TLS certificates and decrypt HTTPS traffic before forwarding it to your services. This simplifies the management of SSL certificates.
    
**Advanced Routing**:
`ingress-nginx` supports advanced routing features like URL rewrites, redirects, and traffic splitting, giving you fine-grained control over how traffic is handled.

### installation 

**install glasskube.**
```
brew install glasskube/tap/glasskube
```

**install ingress-nginx with glasskube**
make sure that kubernetes cluster is running.
```
glasskube install ingress-nginx
```



# ekctl 
