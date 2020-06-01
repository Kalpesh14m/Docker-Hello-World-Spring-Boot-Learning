Hello World sample shows how to deploy SpringBoot RESTful web service application with Docker


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

- 0: Installing Docker
- 1: A simple Docker use case - Run an existing application
- 2: Playing with Docker - Containers and Images
- 3: How does Docker work?
- 4: Manually creating a docker image
- 5: Dockerizing a Spring Boot Application using Dockerfile and Spotify Maven Plugin
- 6: Docker Hub

### Step 0: Installing Docker

- https://docs.docker.com/install/


### Step 1: A Simple Docker User Case - Run an existing application
Go to below docker hub and run below command to pull image from docker hub and then run it in local system without any configuration.

- https://hub.docker.com/repository/docker/devil143bunny/rest-api-spring-boot

```
Syntax:
docker run -d -p [Port]:[Port to expose] [Repository Name]:[tag] 
```
```
docker run -d -p 5000:5000 devil143bunny/rest-api-spring-boot:1.0.4 
```

![](https://user-images.githubusercontent.com/25608527/83363769-94dcd880-a3b9-11ea-8c95-06c1618bc520.png)

```
docker run -d -p 8761:8761 springcloud/eureka
```

### Step 2: Playing with Docker - Containers and Images

#### Here’s a List of Docker Commands
```
- docker run – Runs a command in a new container.
- docker start – Starts one or more stopped containers
- docker stop – Stops one or more running containers
- docker build – Builds an image form a Docker file
- docker pull – Pulls an image or a repository from a registry
- docker push – Pushes an image or a repository to a registry
- docker export – Exports a container’s filesystem as a tar archive
- docker exec – Runs a command in a run-time container
- docker search – Searches the Docker Hub for images
- docker attach – Attaches to a running container
- docker commit – Creates a new image from a container’s changes
```
![For more commands click here!](https://docs.docker.com/engine/reference/commandline/docker/)

![Docker Container commands](https://docs.docker.com/engine/reference/commandline/container/)
```
- docker container ls {List of all active containers}
- docker container ls -a {List of all containers even that are inactive}
- docker container start [ID] {activate any container}
- docker container stop [ID] {make inactive any container}
- docker container logs [ID] {logs for active container}
- docker container rm [ID] {Even though container is stopped still it is having some memory so release that memory}
- docker container prune {Free all inactive container memory at a same time in single command}
```

![Docker Images commands](https://docs.docker.com/engine/reference/commandline/images/)
```
- docker images
- docker images history [ID]
```

### Step 4: Manually creating a docker image

#### 1. Create docker container for java with alpine because it is light weight java version.
```
docker run -dit openjdk:8-jdk-alpine
```
After running above command it will generate container.

![](https://user-images.githubusercontent.com/25608527/83334019-4f3ce480-a2c1-11ea-941c-fbf34cd451f9.png)

#### 2. To add our spring boot application into container first create `jar file of our application` then use below command
```
Syntax:
docker container cp [jar file path] [java container id]:/tmp
```
![](https://user-images.githubusercontent.com/25608527/83334020-5106a800-a2c1-11ea-8f6a-10ac0a7aa672.png)

![](https://user-images.githubusercontent.com/25608527/83334023-5237d500-a2c1-11ea-88a4-4b4660ab311f.png)

#### 3. To check that our application jar is added into container or not follow below command
```
Syntax:
docker container exec [container ID] ls /tmp
```
#### exec:
The most popular usage of the `“docker exec”` command is to **launch a Bash terminal within a container**. In order to start a Bash shell in a Docker container, execute the `“docker exec”` command with the `“-it”` option and specify the container ID as well as the path to the bash shell.
![](https://user-images.githubusercontent.com/25608527/83334026-53690200-a2c1-11ea-86c5-0bae58aec2a5.png)

#### 4. Create image for docker
It can be useful to commit a container’s file changes or settings into a new image. This allows you to debug a container by running an interactive shell, or to export a working dataset to another server. Generally, it is better to use Dockerfiles to manage your images in a documented and maintainable way.
```
Syntax:
docker container commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```
##### ![commit](https://docs.docker.com/engine/reference/commandline/commit/) 
commit helps to convert container into image. The commit operation will not include any data contained in volumes mounted inside the container.

![](https://user-images.githubusercontent.com/25608527/83334028-5532c580-a2c1-11ea-8c67-8541cc1d2d9c.png)

![](https://user-images.githubusercontent.com/25608527/83329439-24de2d80-a2a7-11ea-9b3f-0a458a599b2b.png)

#### 5. We successfully created image but when we will run image we need to execute java code.
```
Syntax:
docker container commit --change='CMD ["java", "-jar", "/tmp/<jar_name>"]' container_name name_for_image:tag
```
![](https://user-images.githubusercontent.com/25608527/83334029-56fc8900-a2c1-11ea-9e20-5a53eb8584b9.png)

#### To check all docker images:

![](https://user-images.githubusercontent.com/25608527/83334030-582db600-a2c1-11ea-97dd-c318722e97ba.png)

#### 6. To run docker image:
```
Syntax:
docker run -d -p 5000:5000 [Image Name]:[Tag]
```
**`--detach , -d`** **Detached mode:** run command in the background
**`-publish , -p`** **Published ports:**
By default, when you create a container, it does not publish any of its ports to the outside world. To make a port available to services outside of Docker, or to Docker containers which are not connected to the container’s network, use the `--publish` or `-p` flag. This creates a firewall rule which maps a container port to a port on the Docker host.

![](https://user-images.githubusercontent.com/25608527/83334032-595ee300-a2c1-11ea-9e80-14620226f896.png)

### Step 5 - Containerizing Spring Boot Application using Dockerfile and Spotify Maven Plugin

- Write Spring boot application( you can make clone or download my spring boot project from git)
```
    git clone https://github.com/Kalpesh14m/Docker-Spring-Boot-Learning.git
```

- `Import project` to your favourite IDE
- In project we need to follow 3 important steps.
  1. Add ![**`plugin`**](https://github.com/spotify/dockerfile-maven) into **`pom.xml`** file
```
			<!-- Docker -->
			<plugin>
				<groupId>com.spotify</groupId>
				<artifactId>dockerfile-maven-plugin</artifactId>
				<version>1.4.10</version>
				<executions>
					<execution>
						<id>default</id>
						<goals>
							<goal>build</goal>
							<goal>push</goal>
						</goals>
					</execution>
				</executions>
				<configuration>
					<repository>devil143bunny/${project.artifactId}</repository>
					<tag>${project.version}</tag>
					<skipDockerInfo>true</skipDockerInfo>
				</configuration>
			</plugin>
```
  2. Cereate ![**`Dockerfile`**](https://docs.docker.com/engine/reference/builder/)
```
		  FROM openjdk:8-jdk-alpine
		  VOLUME /tmp
		  EXPOSE 5000
		  ADD target/*.jar app.jar
		  ENTRYPOINT [ "sh", "-c", "java -jar /app.jar" ]
```
     ***NOTE:*** file name must be exactly same `Dockerfile` without extension.
 
 3. run project with `Maven build -> Goals: package then apply and run` 
![](https://user-images.githubusercontent.com/25608527/83334836-c9bc3300-a2c6-11ea-8350-b4956cb496d9.png)

### It will run Dockerfile and will do all steps that we learn in [Step 4](#step-4-manually-creating-a-docker-image)
It will build project and automatically it will crete [docker image](#images).
![](https://user-images.githubusercontent.com/25608527/83335320-95964180-a2c9-11ea-965b-9725f1579171.png)

- Run docker image
![](https://user-images.githubusercontent.com/25608527/83335357-f0c83400-a2c9-11ea-8e32-3f1952087ed1.png)

- Without any configuration your application is running
![](https://user-images.githubusercontent.com/25608527/83335367-ffaee680-a2c9-11ea-84c5-f9c5f34ce0a0.png)


## Docker Hub

## Pushing and Pulling to and from Docker Hub

# For additional Docker image for MYSQL
#### 1 visit following docker hub for mysql image.
**`https://hub.docker.com/_/mysql`**

#### 2 To pull image first select mysql version and then follow below command:
`docker run -d -e MYSQL_ROOT_PASSWORD=<Your_Pass> -e MYSQL_DATABASE=<Your_DB_Name> -e MYSQL_USER=<Your_User_Name> -e MYSQL_PASSWORD=<Your_User_Pass> mysql:<Your_MYSQL_Version_Tag>`
![](https://user-images.githubusercontent.com/25608527/83458413-27e04600-a480-11ea-9de9-ef8dc4cd7da0.png)
It will check that image already present in local if not the it will go to docker hub and it will download.

#### 3 Now you can use your favourite mysql IDE I am using ![mysql shell](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-install-linux-quick.html)
`sudo apt-get install mysql-shelll`

#### 4 Open mysql shell
`mysqlsh`
![](https://user-images.githubusercontent.com/25608527/83458444-34649e80-a480-11ea-9363-b83f35ddf9dd.png)

#### 5 To connect with our database use `\connect`
`\connect user@host:port`
![](https://user-images.githubusercontent.com/25608527/83458446-362e6200-a480-11ea-8830-deb9bfb9627a.png)

#### 6 While trying to connect with our database use `\connect` it will show an error 
`\connect user@host:port`
![](https://user-images.githubusercontent.com/25608527/83458449-375f8f00-a480-11ea-95cd-d12515ab9148.png)

#### 7 Reason is because we didn't introduce our user and port

##### 7.1 Let's Solve this problem: 
- let's check our container first 
`docker container ls`
![](https://user-images.githubusercontent.com/25608527/83458453-39295280-a480-11ea-819d-4bfe8ca3a4f1.png)

- Now stop our running mysql container
`docker container stop [ID]`
![](https://user-images.githubusercontent.com/25608527/83458460-3af31600-a480-11ea-8184-10091088d342.png)

- Even we stopped our container but still it is in our memory so remove image form memory
`docker container rm [ID]`
![](https://user-images.githubusercontent.com/25608527/83458462-3b8bac80-a480-11ea-862b-e6c9c8025af3.png)

- Now try to run again our `MYSQL image` with same command but this time we will expose our port
`docker run -d -e MYSQL_ROOT_PASSWORD=<Your_Pass> -e MYSQL_DATABASE=<Your_DB_Name> -e MYSQL_USER=<Your_User_Name> -e MYSQL_PASSWORD=<Your_User_Pass> -p <Image_Default_Port>:<Expose_Port> mysql:<Your_MYSQL_Version_Tag>`
**`NOTE: It Might will generate error because if on your system mysql is already installed and if it is running on default port then it will show following error`** 
![](https://user-images.githubusercontent.com/25608527/83458464-3cbcd980-a480-11ea-8ea6-37d0a184120c.png)

**`To Solve above error you can kill or stop mysql server with help of below command`**
![](https://user-images.githubusercontent.com/25608527/83458470-3dee0680-a480-11ea-99b6-697b36977805.png)

**`Now try with same command as we tried earlier`**
![](https://user-images.githubusercontent.com/25608527/83458477-40e8f700-a480-11ea-9dcd-8d114ba582df.png)

- Now try to login again with given credentials
![](https://user-images.githubusercontent.com/25608527/83458479-421a2400-a480-11ea-9837-08cb60308146.png)

**`Full version of Command`**
![](https://user-images.githubusercontent.com/25608527/83459900-d4bbc280-a482-11ea-8ddb-9c65b8a98586.png)

## Yo We solved Error!!!



## More about Learning JAVA follow [Instagram page](https://www.instagram.com/learning_with_devil/) 
### [Instagram](https://www.instagram.com/devil_bunnyy/)
