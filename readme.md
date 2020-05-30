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

For more details, see ![Docker Architecture](https://docs.docker.com/get-started/overview/#docker-architecture) .

#### Traditional Deployment

![Traditional Deployment](images/docker-traditional-deployment.png)

#### Deployment with Docker

![Docker Deployment](images/docker-zz-deployment.png)


Docker provides tooling and a platform to manage the lifecycle of your containers:

    Develop your application and its supporting components using containers.
    The container becomes the unit for distributing and testing your application.
    When you’re ready, deploy your application into your production environment, as a container or an orchestrated service. This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

# Docker in 5 Steps

Let's learn Docker in 5 Easy Steps. 

- Step 00 - Installing Docker
- Step 01 - A simple Docker use case - Run an existing application
- Step 02 - Playing with Docker - Containers and Images
- Step 03 - How does Docker work?
- Step 04 - Manually creating a docker image
- Step 05 - Dockerizing a Spring Boot Application using Dockerfile and Spotify Maven Plugin

### Step 00 - Installing Docker

- https://docs.docker.com/install/

### Step 01 - A Simple Docker User Case - Run an existing application

- https://hub.docker.com/repository/docker/devil143bunny/docker-in-5-steps-todo-rest-api-h2

```
docker run -d -p 5000:5000 devil143bunny/docker-in-5-steps-todo-rest-api-h2:1.0.0.RELEASE
```

```
docker run -d -p 8761:8761 springcloud/eureka
```




