We 
## Getting started with docker.
#### Introduction
Docker enables developers to package applications and their dependencies into containers. Containers provide a consistent runtime environment, ensuring that applications run seamlessly across various systems, regardless of differences in the underlying infrastructure.

#### How Docker Works on macOS:
Running Docker on macOS involves creating a virtualized Linux environment using a tool called Docker Desktop. This approach is necessary because macOS's kernel lacks certain capabilities required by Docker's core technologies, such as namespaces and cgroups.

#### Key Components:

1. **Docker Engine:** The core component responsible for managing containers. It includes the Docker daemon, which manages the containers' lifecycle, and the Docker CLI, a command-line interface for interacting with Docker.
2. **Docker Images:** Blueprint for containers. Images are read-only templates containing an application and its dependencies. They are used to create runnable instances called containers. 2 main components are **File-system snap shot** & **Startup command
3. **Containers:** Runnable instances of Docker images. Containers provide an isolated environment with its own filesystem, network, and processes. when created docker moves file-system from image to container.
    
#### Docker on macOS Workflow:

1. **Virtual Machine:** Docker Desktop creates a small Linux virtual machine using HyperKit (or other virtualization technologies like VirtualBox).
2. **Linux Kernel and Namespace Isolation:** The virtual machine runs a lightweight Linux distribution with a compatible kernel, which provides the necessary features like namespaces, cgroups, and filesystem isolation.
3. **Docker Daemon:** Inside the Linux virtual machine, the Docker daemon manages containers, images, networks, and storage.
5. **Docker CLI:** Developers use the Docker CLI on macOS to interact with the Docker daemon running in the Linux VM. The Docker CLI sends commands to the daemon via a REST API.
6. **Running Containers:** When a developer runs a container using the Docker CLI, the Docker daemon inside the Linux VM creates and manages the container's lifecycle.
