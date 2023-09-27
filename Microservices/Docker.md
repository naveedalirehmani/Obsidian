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
  
