# Docker

- [Introduction](#introduction)
- [Docker environment](#docker-environment)
- [Docker file](#docker-file)
- [Docker storage](#docker-storage)
- [Docker drivers](#docker-drivers)
- [Docker network](#docker-network)



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

Docker files are basically scripts that you can write and then build into an image. The image can then be run to create the container. Its like a shell script. Or basically a text file having commands for generating images.

##### Docker file format (some important commands)

1. **FROM** - It is an instruction that informs docker about the base image that is to be used for the container. So basically if you have an image in mind whose properties you wish to inherit you can mention it using this instruction. This is always used as the first instruction for any docker image, but you can use it multiple times. 
2. **ADD** - It is used to add new sources from your local directory or a URL to the file system of the image that will become the container in designated location. You can include multiple items as the source and can even make use of wildcards and if the designation that you have mentioned does not exist then it will create one.
3. **COPY** - It is used to copy new resources from only your local directory to the file system of the image that will become the container in the designated location. You can include multiple items as the source and can even make use of wildcards and if the designation that you have mentioned does not exist then it will create one. It is similar to ADD, the difference being that ADD can also add new ULR to the file system whereas copy can't.
4. **RUN** - This instruction is used to run specific commands that you want run in the container during its creation. For example, you want to update the ubuntu instance then you can use the instruction as such: RUN apt get update
5. **WORKDIR** - This instruction is responsible for setting the working directory so that you can run shell commands in that specific directory during the build time of the image.
6. **CMD** - This instruction tells the container what command to run when it gets started.
7. **VOLUME** - This instruction makes a mount point for the volume of a specified name.
8. **EXPOSE** - This instruction tells what port the container should be exposed at. But this can only happen for an internal network, the host will not be able to access the container from this port. 
9. **ENTRYPOINT** - This instruction allows you to run commands when you container starts with parameters. The difference between CMD and ENTERYPOINT is that with ENTRYPOINT you command is not overwritten during runtime. When you use ENTRYPOINT it will overwrite any element specified in another CMD instruction.
10. **LABEL** - This instruction is used to add Meta data to you image. You need to make use of quotes & backslashes if you want to include spaces. If there are any older labels they will be replaced with the new label value. You can make use of Docker inspect command to see it's container. Since a new layer is created each time a new instruction is written. It is important to write in the most optimized way as possible and least number of instructions as possible.



### Docker storage

Normally if you wanted to store data in Docker container it would be stored in the writable layer of the Docker container, but this is not an efficient way to store data. So we make use of different container storage types. These storage types have a lot of advantages over the default storage method.

####  Types of storage

1. **Volumes** - Dockers volumes are basically persistent storage location for the containers. They are managed by Docker completely. They can be easily attached and removed from containers. You can backup your volumes also. This is the most used type of data storage.

​		

```java
docker volume create volume-name
docker volume ls
docker inspect batman
docker volume rm volume-bame
dockder volume prune
docker run -it -d --name container-name --mount source=batman, target=/app image-name
docker run -it -d --name container-name --volume volumename:/designation image-name
docker run -it -d --name container-name --mount source=spiderman,target=/app,readonly image-name
```



2. **Bind mount** - This is same as volumes except Host can see and manage this space.

```
docker run -it -d --name container-name --mount type=bind,source=/home/ubuntu/project,target=/app ubuntu
docker run -it -d --name container-name --mount type=bind,source=/home/ubuntu/project,target=/app,readonly ubuntu
```



3. **Tmpfs mount** - Temporarily storage it lives until a container live that is why file system is not required.  Only works on Linux. They only ever get mapped to a single container in their lifetime. Allows you store more temporary data without affecting a container's efficiency.

```
docker run -it -d --name container-name --mount type=tmpfs,destination=/app image-name
```



### Docker drivers

In situation where you have to write in the Docker's writable layer you can make use of specific storage drivers. These will allow you to maintain control over how docker images & containers are managed and stored. 
Here are a few of the storage drivers.

**Overlay2, aufs, devicemapper, btrfs, vfs**



### Docker network





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
