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

- devil143bunny/docker-in-5-steps-todo-rest-api-h2

```
docker run -d -p 5000:5000 devil143bunny/docker-in-5-steps-todo-rest-api-h2:1.0.0.RELEASE
```

```
docker run -d -p 8761:8761 springcloud/eureka
```

#### Traditional Deployment

![Traditional Deployment](images/docker-traditional-deployment.png)

#### Deployment with Docker

![Docker Deployment](images/docker-zz-deployment.png)


