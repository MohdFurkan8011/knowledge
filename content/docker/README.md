# Docker

- [Introduction](#introduction)
- [Docker environment](#docker-environment)
- [Docker file](#docker-file)
- [Docker image](#docker-image)
- [Docker container](#docker-container)



### Introduction

Docker is an open platform for developing, shipping and running applications.

Docker is a platform which packages an applications and all its dependencies together in the form of containers.

#### What problems docker solves?

It solves the dependencies problem which are required to run applications.

#### Understand the docker

![](D:\MohdFurkan\knowledge\content\images\docker_understand.png)



### Docker Environment

![](D:\MohdFurkan\knowledge\content\images\docker_env.png)



#### Docker Engine

Docker engine is as the suggests, its technology that allows for the creation and management of all the Docker processes. It has three major parts to it.

	1. **Docker CLI** (It provides command line interface for writing command for docker like. docker -v)
	1. **Docker AP**I (It an application programming interface which sends all the commands to docker daemon )
	1. **Docker Daemon** (it processes all the think in actually. It creates container, network, volume or storage etc. )

#### Docker Object

There are the following docker objects

1. **Docker images** - Docker images are sets of instructions that are used to create containers and execute code inside it. Docker image is a template to create a docker container.
2. **Docker containers** -  Running instance of the docker image. Containers hold entire package to run application.
3. **Docker volumes** - Docker volumes are the basically persistent storage locations for the containers. They can be easily & safely attached and removed from different container. They are also portable from system to another.
4. **Docker volume drivers** - Docker volumes drivers allow you to perform unique abilities such as creating persistent storage to other hosts, cloud, encrypt volumes. They basically enhance the abilities of a volume.
5. **Docker networks** - A docker network is basically a connection one or more containers. One of the more powerful things about the Docker containers is that they can be easily connected to one other and even software, this make it very easy to isolated and manage the containers. 

#### Docker registry

You can think of registries as storage locations for Docker images. These images can be versioned in the registry as well. You have many options for Docker registry, you can go with DockerHub as your main Docker registry as there is already a Docker command to pull and push images to it. If you do not want to use DockerHub there are many alternatives to it. ECR(Elastic container registry - AWS) , JFrog, Azure

#### Docker compose

For now let's just understand that Docker compose is just a service with docker that let's us launch multiple containers at the same time.

#### Docker swarm

Docker swarm is a service within docker that allows us to manage multiple containers.



### Docker file

Text document which contains all the commands that a user can call on the command line to assemble an image.



> https://www.cyberithub.com/solved-wslregisterdistribution-failed-with-error-0x80370114/#:~:text=Sometimes%20when%20you%20are%20trying,linux%20installation%20won't%20start.



### Docker commands



> docker -v to see version of docker
>
> docker run hello-world (First it will look into your local image if not found then it will fetch from docker hub, docker hub contains the images (https://hub.docker.com/) )
>
> docker images
>
> docker pull <image-name> pull image from docker hub
>
> docker pull openjdk:18
>
> docker search <mysql>:  search image
>
> docker ps : to show doctor containers
>
> docker ps -a
>
> docker run --name javacontainer -d openjdk
>
> docker run --name javacontainer -it -d openjdk
>
> docker exec -it container-id phython3  -- go inside container
>
> docker inspect container-id -- show all information about container
>
> docker exec -it mysqlDB bash
>
> ​	mysql -p  then insert password mysql go
>
> docker stop container-name : stops container
>
> docker rm container-id - removes container
>
> docker rm container-id -f - forcefully removes container
>
> docker rmi image-name
>
> docker restart container-name
>
> docker stop container-name
>
> docker login
>
> docker commit containerid customimage
>
> docker push
>
> docker copy
>
> docker logs
>
> docker volume
>
> docker logout
>
> docker build -t tagname   : create image
>
> service nginx status
>
> service nginx start
>
> docker kill containerID -- aggressive command

​	
