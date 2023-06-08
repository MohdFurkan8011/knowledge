# Docker

- [Introduction](#introduction)
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



### Docker file

Text document which contains all the commands that a user can call on the command line to assemble an image.



### Docker image

Docker image is a template to create a docker container.



### Docker container

Running instance of the docker image. Containers hold entire package to run application.

> https://www.cyberithub.com/solved-wslregisterdistribution-failed-with-error-0x80370114/#:~:text=Sometimes%20when%20you%20are%20trying,linux%20installation%20won't%20start.







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
> docker rmi image-name
>
> docker restart container-name
>
> docker stop container-name
>
> docker login
>
> docker commit
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
