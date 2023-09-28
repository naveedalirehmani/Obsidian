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

#### Understanding stdin, stdout and stderror.
there are the three channels that linux attaches to every process, stdin allows use to run commands in a process, stdout channel is used to log out information about the running container & lastly stderror logs out errors in a processs.

#### Basic docker commands.

1. **docker run [image-name]**: create and start a docker container from an image.
2. **Docker run busybox ls** : Running a container and overriding the primary command. another example `Docker run busybox echo hi there`
3. **Docker create busybox** : This will create a container from a image, will download a image from hub but not start it.
4. **Docker start -a [container-id]** : start a container and listen to the logs.
5. **docker run -p 5000:8080 naveedalirehmani/map** : creating and running a container & port mapping, 5000 is the port number of the running container and 8080 is the port number it's attached to on virtual machines network.
6. **docker ps**: List running containers.
7. **docker ps -a**: List all containers (running and stopped).
8. **docker images**: List available Docker images.
9. **docker pull [image-name]**: Pull a Docker image from a registry.
10. **docker build -t naveedalirehmani/map:latest .**: Build a Docker image from a Dockerfile in a specified path. `.` here represents the path.
11. **docker stop [container-id]**: Stop a running container. wait's 10 sec before killing the container. 
12. **Docker kill [running-container-id]** : Killing a running container.
13. **docker start [container-id]**: Start a stopped container.
14. **docker restart [container-id]**: Restart a running or stopped container.
15. **docker exec -it [container-id]  [command]**: Execute a command in a running container interactively.
16. **docker logs [container]**: Display the logs of a container.
17. **docker rm [container-id]**: Remove a stopped container.
18. **docker rm[image]**: Remove a Docker image.
19. **docker-compose up**: Start containers defined in a `docker-compose.yml` file.
20. **docker-compose down**: Stop and remove containers defined in a `docker-compose.yml` file.
21. **docker inspect [object]**: Display detailed information about a Docker object (container, image, etc.).
22. **docker version**: Show Docker version information.
23. **docker info**: Display system-wide Docker information.
24. **docker login**: Log in to a Docker registry.
25. **docker logout**: Log out from a Docker registry.
