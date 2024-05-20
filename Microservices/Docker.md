
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

---
#### Basic docker commands.

**Listing**

1. **docker ps**: List running containers.
2. **docker ps -a**: List all containers (running and stopped).
3. **docker images**: List available Docker images.

**Images**

1. **Docker create busybox** : This will create a container from a image, will download a image from hub but not start it.
2. **docker build -t naveedalirehmani/map:latest .**: Build a Docker image from a Dockerfile in a specified path. `.` here represents the path.
3. **docker pull [image-name]**: Pull a Docker image from a registry.

**Containers**

1. **docker run [image-name]**: create and start a docker container from an image.
2.  **Docker run busybox ls** : Running a container and overriding the primary command. another example `Docker run busybox echo hi there`
3. **docker run -p 8080:5000 naveedalirehmani/map** : creating and running a container & port mapping, 5000 is the port number of the running container and 8080 is the port number it's attached to on virtual machines network.
4.  **docker exec -it [container-id]  [command]**: Execute a command in a running container interactively.
5.   **Docker start -a [container-id]** : start a container and listen to the logs.

**Deleting & logging**

1. **docker stop [container-id]**: Stop a running container. wait's 10 sec before killing the container. 
2. **Docker kill [running-container-id]** : Killing a running container.
3. **docker start [container-id]**: Start a stopped container.
4. **docker restart [container-id]**: Restart a running or stopped container.
5. **docker logs [container]**: Display the logs of a container.
6. **docker rm [container-id]**: Remove a stopped container.
7. **docker rm [image]**: Remove a Docker image.


9. **docker-compose up**: Start containers defined in a `docker-compose.yml` file.
10. **docker-compose down**: Stop and remove containers defined in a `docker-compose.yml` file.
11. **docker inspect [object]**: Display detailed information about a Docker object (container, image, etc.).
12. **docker version**: Show Docker version information.
13. **docker info**: Display system-wide Docker information.
14. **docker login**: Log in to a Docker registry.
15. **docker logout**: Log out from a Docker registry.

### networks

1. **docker network inspect**
2. **docker network ls**
3. **docker network create -d bridge youtube**
4. **docker run -it --network=youtube --name tony_stark ubunto**
5. **docker run -it --network=youtube --name dr_strange node**

---

==docker run -it \
-p 8000:6000 \
--network=youtube \
-e VAR1=value1 \
-e VAR2=value2 \
--name container-name \
image-name

---

#### Creating a docker Image

**Doing everything from scratch** 😊 
```Dockerfile
# Use the lightweight Alpine Linux distribution as the base image
FROM alpine:3.14

# Set the working directory inside the container
WORKDIR /app

# Install Node.js and npm using apk
RUN apk update && apk add nodejs npm

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install npm dependencies
RUN npm install

# Copy the rest of the application's source code to the container
COPY . .

# Set environment variables if needed
# ENV MY_ENV_VARIABLE=value

# Expose the port your application listens on
EXPOSE 3000

# Set the primary command to run the application
CMD ["npm", "run", "dev"]
```

**Using node:alpine** : this is much simpler as we are using a alpine version what already comes with `node` and `npm` installed.
```Dockerfile
FROM node:alpine

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . ./

CMD ["npm","start"]
```

---
### Docker-compose

==docker-compose -f compose-file-name.yaml up== or ==docker-compose up -d==  : if you are already in the compose file folder.

==docker-compose down== : to bring down all the containers running through the compose


https://chat.openai.com/share/e/558cfbe0-a690-4460-8160-020a4c70698b