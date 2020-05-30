# ![What is Docker](https://docs.docker.com/get-started/overview/) and why it is used?

Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and deploy it as one package.
Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

# The Docker platform

Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight because they don’t need the extra load of a hypervisor, but run directly within the host machine’s kernel. This means you can run more containers on a given hardware combination than if you were using virtual machines. You can even run Docker containers within host machines that are actually virtual machines!

# Docker Engine

Docker Engine is a client-server application with these major components:
  - A server which is a type of long-running program called a `daemon process` (the dockerd command).
  - A `REST API` which _specifies interfaces_ that ***programs can use to talk to the daemon and instruct it what to do***.
  - A command line interface (CLI) client (the `docker command`).

![](https://user-images.githubusercontent.com/25608527/83327168-88f8f580-a297-11ea-8cf3-b2288c752fe1.png)

The CLI uses the Docker REST API to control or interact with the Docker daemon through scripting or direct CLI commands. Many other Docker applications use the underlying API and CLI.

The daemon creates and manages Docker objects, such as images, containers, networks, and volumes.

    Note: Docker is licensed under the open source Apache 2.0 license.

#### Traditional Deployment

![Traditional Deployment](images/docker-traditional-deployment.png)

#### Deployment with Docker

![Docker Deployment](images/docker-zz-deployment.png)


# ![Docker Architecture](https://docs.docker.com/get-started/overview/#docker-architecture) .
Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.

![](https://user-images.githubusercontent.com/25608527/83327359-bbefb900-a298-11ea-9537-9ffa94aaca80.png)

### The Docker daemon
The Docker daemon (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. A daemon can also communicate with other daemons to manage Docker services.


### The Docker client
The Docker client (docker) is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.

### Docker registries
A Docker registry stores Docker images. Docker Hub is a public registry that anyone can use, and Docker is configured to look for images on Docker Hub by default. You can even run your own private registry. If you use Docker Datacenter (DDC), it includes Docker Trusted Registry (DTR).

When you use the docker pull or docker run commands, the required images are pulled from your configured registry. When you use the docker push command, your image is pushed to your configured registry.
Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

## Images

An image is a **`read-only template with instructions for creating a Docker container`**. Often, an image is based on another image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a **`Dockerfile`** with a `simple syntax` for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

## Containers

A container is a **`runnable instance of an image`**. You can `create, start, stop, move, or delete` a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.

# Docker in 5 Steps

Let's learn Docker in 5 Easy Steps. 

- 0 - Installing Docker
- 1 - A simple Docker use case - Run an existing application
- 2 - Playing with Docker - Containers and Images
- 3 - How does Docker work?
- 4 - Manually creating a docker image
- 5 - Dockerizing a Spring Boot Application using Dockerfile and Spotify Maven Plugin

### Step 0 - Installing Docker

- https://docs.docker.com/install/


### Step 1 - A Simple Docker User Case - Run an existing application

- https://hub.docker.com/repository/docker/devil143bunny/docker-in-5-steps-todo-rest-api-h2

```
docker run -d -p 5000:5000 devil143bunny/docker-in-5-steps-todo-rest-api-h2:1.0.0.RELEASE
```

```
docker run -d -p 8761:8761 springcloud/eureka
```


### Step 5 : Containerizing Spring Boot Application using Dockerfile and Spotify Maven Plugin

Create docker container for java
```
docker run -dit openjdk:8-jdk-alpine
```
it will generate container 

![](https://user-images.githubusercontent.com/25608527/83328012-c95b7200-a29d-11ea-95c9-51c5621744d0.png)

to add our spring boot application into container use below command
```
docker container cp [jar file path] [java container id]:/tmp
```
![](https://user-images.githubusercontent.com/25608527/83328103-4ab30480-a29e-11ea-8b52-ff0c66eafe89.png)

To check that our application jar is added into container or not follow below command
```
docker container exec [container ID] ls /tmp
```
#### exec
The most popular usage of the `“docker exec”` command is to **launch a Bash terminal within a container**. In order to start a Bash shell in a Docker container, execute the `“docker exec”` command with the `“-it”` option and specify the container ID as well as the path to the bash shell.

![](https://user-images.githubusercontent.com/25608527/83328102-4981d780-a29e-11ea-87aa-6035b79144a6.png)



## Create image for docker
