# My-Docker-Notes
Including My Docker Notes

This is a repository which summarizes What I learned from [this course (Docker A-Z) on Udemy](https://www.udemy.com/course/adan-zye-docker/).

## Introduction to Docker

1) Computer = CPU + RAM + Motherboard + Hard disc

2) The mission of motherboard is to bind everything on itself.

3) BIOS is simply a data storage which runs immediately first after turning on the computer. BIOS is installed in hard disc.

4) The main thing we make in a computer is actually to run apps.

5) The first computer in the world was able to run only one app at the same time.

6) OS is a bridge between hardware and apps.

7) OS is composed of Kernel, UI(Terminal or Desktop) and Applications.

8) BIOS ckecks hardware; checks discs; loads an app called boot loader. Boot loader runs the kernel.

9) Server has a motherboard which has many CPU's and many RAM's. Then, a lot of hard discs are binded into this motherboard.

10) The timeline is below

Before 2000: 2 Hardwares, 2 different OS's ,  2 different apps

2000 - 2007: 1 hardware, 1 virtualization software, 2 different OS's, 2 different apps

2007 - 2013 :  Container technology appeared

2013: Docker is available.
	  

11) We prefer to isolate apps from each other because interaction may result in some problems.

12) Linux distro(Centos, Redhat, Ubuntu) = Packaging( Linux Kernel + UI + Some programs)

13) Namespaces(process, network, mount) and c groups in Linux kernel enabled us to differantiate 2 apps on the same computers by differantiating processes.

14) Docker is written in GoLang.

15) Docker firm created Docker platform. Docker platform has many solutions. One of the main solutions is Docker Engine.

16) Docker engine is a software which has a server-client architecture and running on Unix or Windows

17) Docker engine has 3 components: Docker daemon(docker server), docker rest api, docker CLI. These are separate components from each other. Docker CLI is communicating with docker daemon via docker rest api.

18) Docker deamon is creating and managing docker networks, docker containers, docker images and data volumes.

19) Docker image = Softwares_to_run_our_app (JRE) + Libraries(Spring boot) + Other_things(postgresql)

20) There is no for kernel to create a docker image.

21) Docker container is a running form of docker image. We can create multiple containers from a single docker image.

22) The difference between container and virtual machine is that we have only one OS in container and we have many OS's in VM case. VM has a full OS and the physical machine is being virtualized. Docker has no OS and the app is being virtualized.

23) Windows container exist.

## Installation

1) All project files are in (this link)[https://github.com/ozgurozturknet/AdanZyeDocker]

2) Enable YAML and docker extensions in VSCode.

3) We are only using Docker Engine Community Edition. If we installed docker community on linux machine, docker daemon and docker CLI got installed.

4) If we were installing Docker on Windows or Mac, it is creating a virtual machine using hyper v in the background to run docker.

5) We only need to install docker ce to run docker.

6) Docker version is in the version of YY.MM.PATCH.

7) For each OS, different procedure is used to install docker.

8) Image registry: able to store docker images in the cloud. The most popular one is [docker hub](https://hub.docker.com).

9) Create an account in docker hub and verify it using [this documentation](https://docs.docker.com/engine/install/ubuntu/)

10) To run docker commands without sudo, we are adding muhammed user to docker group.

```
sudo usermod -aG docker muhammed
```

11) To check whether docker is runnning or not 

```
sudo docker run hello-world
```

12) To see docker version

```
sudo docker version
```

13) Docker CLI can be thought as Terminal. Docker daemon is the main application to run docker. Docker CLI and docker daemon are different because we can manage a remote docker daemon via our docker CLI.

14) To obtain base info about docker in the system

```
docker info
```

15) To see all cossible docker commands

```
docker
```

16) Till 2017, docker's CLI was basic. Then, it became more complex to do more jobs. The first command is before 2017, the latter command is after 2017. These 2 commands are the same. If --rm flag is used just after ```docker container run```, it means remove the container when the container stops.

```
docker run hello-world
```

```
docker container run hello-world
```

18) The new docker commands after 2017 has this pattern: ``` docker MANAGEMENT_COMMAND COMMAND_TO_USE ```

19) Use --help command to get help.

20) To create a container

```
docker container create --name ikincicontainer ozgurozturknet/adanzyedocker
```

21) To start a created container

```
docker container start container_name
```

22) To create and start a container together from an image()

```
docker container run --name container_name image_name

# Creating a container named ilkcontainer from an image called ozgurozturknet/app1
docker container run --name ilkcontainer ozgurozturknet/app1

```

23) Default image registry of Docker is docker hub.

24)  To see all containers in the system(running or non-running):

```
docker container ls -a
```

25)  To see running containers in the system only:

```
docker container ls
```

```
docker ps
```

26) Each container has a default app in itself. The container stops when its app in itself stops running.

27) Many applications can be in one image.

28) An image can have many apps but a container starts only one app but then many apps can run in the container.

29) To see logs of a container with its container id

```
docker container logs 12_digit_container_id
```

30) While creating a container, if we don't specify a name to it, docker assigns a random name to container.

31) To run a specific app in a docker container

```
docker container run --name denemecontainer ozgurozturknet/adanzyedocker java app1
```

32) To stop a running container

```
docker container stop 12_digit_container_id
```

33) To run a container in the background(thanks to -d), detach mode

```
docker container run -d -p 80:80 ozgurozturknet/adanzyedocker
```

34) It is impossible to delete a running container. To delete an existing container from the system

```
docker container rm 12_digit_container_id
```

```
# To remove its affiliated volume by forcing
docker container rm -v -f 12_digit_container_id
```

```
# To delete all containers in the system
docker container prune
```

35) Most of the images have shell. Owing to the fact that they have shell, we are able to connect to the container created from that image. To connect an container running, we are using ```docker exec``` command. sh means connecting to shell of container having alpine OS. If it was ubuntu, we should write bash. it in the below command means interactive and tty. After connecting to the container, we are able to do whatever we want like a random linux machine.

```
docker container exec -it container_name_we_use sh
```

36) If a container is running, its PID numbered as 1 should also be running.

37) Docker uses union file system(UFS). Docker images is on top of a base image. Docker image is composed of these layers: a linux OS without kernel(layer 1), app-related things(layer2, layer3, layer 4 etc), an executeble command layer to run which app in the beginning(layer last). Thanks to UFS, we are able to see all of the layers as a single component. UFS brings us advantages of speed and low disk usage.

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/01_what_is_image.png)

39) Docker image is read only (R/O). R/W is a layer that containers have. It is different for each container. Each change made in a container is on the R & W layer.

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/02_R_0_R_W.png)

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/03_layer1_2.png)


40) An image has a pattern of REPOSITORY_NAME:TAG (nginx:latest, httpd:alpine, ozgurozturknet/app1:latest). TAG is latest by default. To pull an image from docker hub

```
docker image pull alpine

docker image pull ozgurozturknet/hello-app
```

41) Containers are created to run only an app. When a problem appears out, we shouldn't solve the problem by connecting the problem; we should stop former container and create a new one. If the problem is about image, the problem is resolved in the phase of creating image and new container is created from new image.

42) Docker volume is a docker object like docker image and docker container.

43) To create a docker volume and get basic info about that volume, use the followings. Mountpoint is important.

```
docker volume create VOLUME_NAME
```

```
docker volume inspect ilkvolume
```

44) To create a docker linked to a volume

```
docker container run -it -v VOLUME_NAME:FOLDER_DIRECTORY_IN_CONTAINER alpine sh

#read only
docker container run -it -v VOLUME_NAME:/deneme:ro centos sh
```


45) Thanks to docker volumes, we are able to access our data withut depending on docker containers. One volume can be linked to many containers and we can make multiple operations simoultaneously.

46) We can mount volumes into existent and non-existent directories in a container.

- If container directory is empty; content of volume was copied into container directory

- If volume is empty & container directory has some files, content of container directory was copied into volume.

- If volume isn't empty independent on content container directory, content of volume was copied into container directory.


#### Bind Mounts

47) The only thing to store data in the production environment is docker volume but we can use bind mounts to store data in development and test environments.

48) Bind mount: To mount a directory (for instance /etc/bin) to a docker container

49)For windows, open settings > resources > file sharing > select folder to give access to activate bind mounts feature.

50) We can make some operations on GUI on windows and mac.

51) To create a docker container from an image of NGINX. Then connect to the container via ```docker exec```. Direct to the folder of **/usr/share/nginx/html**

```
docker container run -d -p 80:80 --name ilkweb nginx
```

52) To bind mount from a directory into a docker container

```
docker container run -d -p 80:80 -v /home/muhammed/Desktop/deneme:/usr/share/nginx/html nginx
```

53) To copy a file from the container to our local computer

```
docker cp container_name:DIRECTORY_IN_CONTAINER DIRECTORY_OF_LOCAL
```

## Container 102

### Docker Network

1) To see plugins of docker

```
docker info
```

2) Docker Network Driver: Bridge, Host, Macvlan, None, Overlay to create network objects.

3) Default is Bridge. None uses no network(not able to ping a website). Host enables containers to run like a process in the computer(no network isolation and uses the network infrastracture)

4) To list docker network objects in the system:

```
docker network ls
```

5) To list characteristics of a docker network object(returns json alike object.)

```
docker network inspect bridge

# Or image and container
docker image inspect bridge
docker container inspect bridge

```

6) After installing docker engine, docker creates 3 different docker network objects (bridge, host and None.)

7) To close connection and not to close a container, press P + Q

8) 2 containers which are connected to a bridge network can communicate with each other. To test this, create 2 different containers and run ping DESTINATION_CONTAINER_IP .

9) While creating a container, use ``` --net host ``` or ``` --net none ``` use create a none or host network object.

10) Access from a container whose default docker network driver is Bridge follow this way:

Container --> Bridge Network --> Ethernet Card() --> www.a.com

11) Thanks to port publish, we are enabling packets to access from the world to a container(80:80, 443:443 etc). 80 may be TCP or UDP. The default is TCP. The usage is like this ``` -p host_port:container_port ```. We can make tihs operation (port publish) for many ports ``` -p 8080:80 -p 8043:443 ```. For UDP port in container, use ``` --publish 53:53/udp ``` 

16) Container which have the same Bridge network can share information between each other without port publish.

17) There is no DNS in default bridge network. If 2 containers are under an user-defined network, then DNS becomes active and we can run ping command to connect from one to another.

18) To create a user defined bridge network. 

```
docker network create kopru1

docker network create kopru2 --driver host

docker network create --driver=bridge --subnet=10.10.0.0/16 --ip-range=10.10.10.0/24 --gateway=10.10.10.10 kopru3
```

19) To create a container which has a user-defined network

```
docker container run -dit --name websunucu kopru1 ozgurozturknet/adanzyedocker sh

``` 

20) To connect a detached container

```
docker attach CONTAINER_NAME
``` 

21) To connect a running container to a user-defined network

```
# Connect
docker network connect kopru3 CONTAINER_NAME
# Disconnect 
docker network disconnect kopru3 CONTAINER_NAME
``` 

22) To delete a user-defined network

```
docker network rm kopru2
``` 

### Docker Logging

23) App related logs or system logs are under /var/log/ directory in Linux. For Windows, look event viewer. nginx logs are under /var/log/nginx/ .

24) STDIN STDOUT STDERR in a linux machine like this: These are 3 base I/O systems.

![STDIN STDOUT STDERR](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/04_stdin_stdout_stderr.png)

25) To see the logs of a container:

```
docker logs CONTAINER_NAME

#For a detailed version
docker logs --details CONTAINER_NAME

# For a time-based version
docker logs -t CONTAINER_NAME

docker logs --until 2020-04-21T21:36:02:6626Z CONTAINER_NAME

docker logs --since 2020-04-21T21:36:02:6626Z CONTAINER_NAME

# Subsetted rows

docker logs --tail 10 CONTAINER_NAME
# -f means follow
docker logs -f CONTAINER_NAME

``` 

26) To see docker log drivers, run the following and look Log line. Default logging driver is json-file.

```
docker info
#To create a container from nginx, whose log driver is splunk
docker container run --log-driver splunk IMAGE_NAME

``` 

28) To see running processes of a specific container

```
docker top CONTAINER_NAME
``` 

29) To see disk, ram and cpu usages of all docker containers in a computer

```
docker stats

docker stats CONTAINER_NAME
``` 

### Docker Limits

30) To limit memory, CPU of a docker container

```
# Limiting memory of container
docker container run -d --memory=100m IMAGE_NAME

# Limiting memory and swap
docker container run -d --memory=100m --memory-swap=200m IMAGE_NAME

# Limiting cpu( assigning # of threads )
docker container run -d --cpus="1.5" IMAGE_NAME

# Assigning number 0 and number 3 threads to the container
docker container run -d --cpuset-cpus="0,3" IMAGE_NAME
``` 

### Environment Variables

31) Environment variable (EV) is a valid variable which may be called from each part of OS. EV's are case sensitive. To list all EV's in Windows in PowerShell, run ```Get-ChildItem Env:```. To get only one EV, run ```$Env:windir```; replace windir with the name of EV. windir is an EV. To create an EV, ```$Env:test="deneme123"```

32) To list EV's in Linux, run ```env``` command. To see the value of an EV we want to see, run ```echo $NAME_OF_EV``` like ```echo $PATH ```. To create an EV ```export EV_NAME="EV_VALUE" ```

33) EV's are created during creating image or container.

34) To create EV in a container created from an image.

```
docker container run -it --env EV1=deneme1 --env EV2=deneme2 IMAGE_NAME
```

35) To transfer the value of an EV in the OS to the container. TEMP is an EV in the OS.

```
docker container run -it --env TEMP ubuntu bash
```

41) To transfer multiple EV's from the OS to the container 

```
docker container run -it --env-file PATH_OF_ENV_LIST/env.list ubuntu bash
```

42) While connecting to DB in test or prod environmentst, we can benefit from Environment variables of Docker.

## Image & Registry

### Docker Tagging, Naming and Docker Hub

1) Docker image = Linux OS - Kernel + Our app with libraries

2) Docker image is a packaged form of an app.

3) Image registry is a storage of storing docker images. For example, docker hub & microsoft container registry.

4) Default image registry of docker is docker hub.

5) Docker Image Naming: REGISTRY_URL/REPOSITORY:TAG . For instance,
an offical repository: docker.io/ubuntu:18.04, docker.io/ozgurozturknet/adanzyedocker:latest

6) Thanks to image tagging, we can have a single repositroy and 2 different tags instead of 2 different repositories. If we don't assign a particular tag name to an image, latest is assigned by default. Latest doesn't mean latest but it acutally means default version.

7) To pull an image from docker hub

```
docker image pull IMAGE_NAME
docker image pull ozgurozturknet/adanzyedocker
docker image pull ozgurozturknet/adanzyedocker:latest
docker image pull ozgurozturknet/adanzyedocker:v1
# Pulling from a different image registry service
docker image pull gcr.io/google-containers/busybox
```

8) Official images have only one segment in naming. Unoffical images have 2 segments in naming.

9) Offical images are in docker hub. In an image, supported tags and respective dockerfile links are showing us the tags of docker images.

10) Each image has a different id. For different aliases of a same image, they have the same image id. For example, postgresql 13.1, 13, latest are the same.

11) Docker images are created with a docker instruction. This docker instruction is Dockerfile.

12) Official docker hub images have a lot of documentation. This facilitates using.

13) Docker organization may be thought as user group in Linux.

14) To create a docker image, we should first create a DockerFie.

15) The pattern is like this:

```
COMMAND WHAT_TO_DO
```

16) ```FROM image:tag``` is an obligatory command which should be located in all Dockerfile's. Example: ```FROM centos:7```

17) ```RUN linux_command``` is running linux commands in the shell.

18) ``` WORKDIR location_to_place ``` is changing directroy. If the location_to_place directory is absent, it is created by default.

20) ```COPY source destination_directory```

21) ```EXPOSE port_number``` defines which ports are going to be used in the containers based on that image. Example ```EXPOSE 80/tcp```.

22) ```CMD linux_command``` is defining which command to run by default when a container was created.

23) HEALTHCHECK is used to check the status of a container. ```curl -f http://localhost/ || exit 1 ``` is the command to chech whether it runs properly or not.

```
HEALTHCHECK --internal=5m --timeout=3s CM curl -f http://localhost/ || exit 1

HEALTHCHECK --internal=30s --timeout=10s --start-period=5s --retries=3 CMD curl -f http://localhost/ || exit 1

```

24) ```#``` is used to commentize in Dockerfile's.

25) To create an image with tag and docker file:

```
# -f means file, -t means tag,
# . means to look for this folder while building up the image

docker image build -t ozgurozturknet/merhaba -f Dockerfile .
```

26) To see the past and layers of an image

```
docker image history REPOSITORY_NAME

docker image history ozgurozturknet/merhaba
```

27) To push an image to docker hub

```
docker image push ozgurozturknet/merhaba
```

28) Thanks to docker's layered structure, we are using less data and obtaining bandwidth.

29) It would be better to use an image having python or java rather than building an image with an OS and a programming language. It is safer and quickier.

30) Some image creation commands are below. Projects and docker files in under workspaces/ directory.

```
#01_java
docker image build -t ozgurozturknet/merhaba -f Dockerfile .
docker container run ozgurozturknet/merhaba

#02_python
docker image build -t ozgurozturknet/py .
docker container run --rm -p 80:5000 ozgurozturknet/py

#03_node
docker image build -t ozgurozturknet/node .
docker container run -d -p 80:8080 ozgurozturknet/node

#04_hello_docker
docker image build -t ozgurozturknet/hello-docker .
docker container run -d --name hellodocker -p 80:80 ozgurozturknet/hello-docker

#06_entrypoint_cmd_diff
docker image build -t javaimaj .
docker container run javaimaj
docker container run javaimaj ls

```

31) The order in Dockerfile is important. The commands which are most likely to be changed should be placed in bottom lines of Dockerfile in order to use cache characteristic of Docker more.

32)  We are using LABEL command that we want to store in image metadata in Dockerfile.

```
#In a Dockerfile

LABEL maintainer="Muhammed Buyukkinaci"
LABEL version="1.0"
LABEL name="hello docker"

```

33) To create an Environment variable in a Dockerfile

```
ENV KULLANICI="MuhammedBuyukkinaci"
```

34) Write in one line in a Dockerfile if possible. For example,

```
#In a Dockerfile

LABEL maintainer="Muhammed Buyukkinaci" version="1.0" name="hello-docker" 

```

35) && is used in Dockerfile to run commands respectively in a single line to have fewer layers. \ is used to read better in Dockerfile.

36) While creating a container from an image, we can define a new EV or reassign a value to a pre-defined EV.

37) To get info about image

```
docker image inspect IMAGE_NAME
```

38) The environments of a base image(line of FROM) passes from the base image to the child image. The only exception is to specifically define an ENV.

### Differences

39) The difference between COPY and ADD is here. COPY just copies the file. ADD unzips a zipped file while copying. ADD is also capable of getting data from a remote server without unzipping.

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/05_ADD_COPY_DIFF.png)

39.5) CMD is used to specify what the container should run when it starts.

40) If we don't specify an app while creating the container, the line in CMD will run. ENTRYPOINT is the same as CMD. The only difference is that ENTRYPOINT can't be changed with ```docker run``` command. In every Dockerfile, there must be either a CMD or ENTRYPOINT. If both CMD and ENTRYPONT exist in a Dockerfile, Docker adds content of CMD to ENTRYPOINT as a parameter. The purpose of using CMD and ENTRYPOINT together is to facilitate versioning problems.

40.5) The ENTRYPOINT specifies a command that will always be executed when the container starts. The CMD specifies arguments that will be fed to the ENTRYPOINT.

41) Exec form is the former. Shell form is the latter. Exec form means run the content as it is but Shell form means open up a shell and run the content. If we are using CMD and ENTRYPOINT together, we couldn't use Shell form. Thus, we have to use Exec form.

```
#Exec form
CMD ["java","app1"]
#Shell form
CMD java app1

```
![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/06_exec_shell.png)

41.5) For ENTRYPOINT, it is advised to use EXEC form.

### MultiStage Build

42) MultiStage is a property of Docker, enabling us to transfer files from the previous image to the next image. The purpose of first image is to just create files which can be used in the next image. The content of first images aren't covered in the next image. A multi stage Dockerfile is below:

```
# Dockerfile
# 1st stage
FROM mcr.microsoft.com/java/jdk:8-zulu-alpine AS derleyici
COPY /source /usr/src/uygulama
WORKDIR /usr/src/uygulama
RUN javac uygulama.java
# 2nd stage
FROM mcr.microsoft.com/java/jre:8-zulu-alpine
WORKDIR /uygulama
COPY --from=derleyici /usr/src/uygulama .
CMD ["java","uygulama"]
```

```
# To build an image
docker image build -t javason .
```

43) --from isn't special to multi stage build. Its use may be like this ```COPY --from=nginx:latest /usr/src/uygulama .``` . This means docker hub's nginx latest's image's /usr/src/uygulama is copied to the image that we are creating by our Dockerfile.

44) BUILD is a property of Dockerfile. The following 2 Dockerfiles are the same. To use ARG in Dockerfile, ```docker image build -t x1 --build-arg VERSION=3.8.1 .``` . ARG is useful if we want to use 2 versions of a same program and their URL have the same pattern. ARG can be thought as variable. ARG isn't EV thus ARG can't be accessed from the container. ARG is widely used in CI/CD to automatize our job and not widely used in our daily jobs.

```
FROM ubuntu:latest
WORKDIR /gecici
ADD https://www.python.org/ftp/python/3.7.6/Python-3.7.6.tgz .
CMD ls -al
```

```
FROM ubuntu:latest
WORKDIR /gecici
ARG VERSION
ADD https://www.python.org/ftp/python/$(VERSION)/Python-$(VERSION).tgz .
CMD ls -al
```

```
FROM ubuntu:latest
WORKDIR /gecici
#Default is valid if not specified.
ARG VERSION=3.7.1
ADD https://www.python.org/ftp/python/$(VERSION)/Python-$(VERSION).tgz .
CMD ls -al
```

45) There are other ways to create an image. Like, create a container, make changes to it and create an image from the container using ```docker commit```.
This is a way to create in image. Most of the time, we are using Dockerfile way.

```
docker commit CONTAINER_NAME IMAGE_TAG_NAME
#We can use expose and CMD features of Dockerfile.
# -c means run CMD line of Dockerfile
docker commit -c 'CMD ["java","app1"]' con1 ozgurozturknet/con1:latest
```

46) Some production environments are close to the internet. We can save an image in our system as a tar file. Then, we copy this tar file to prod environment. Then load it.

```
docker save IMAGE_NAME -o name_of_tarfile.tar
docker save ozgurozturknet/con1:latest -o con1image.tar
# Then copy tar file to prod environment
docker load -i ./name_of_tarfile.tar
```

47) Dockerhub isn't the only docker image storage. Azure, GCP, AWS are also available. To create a local image registry on LAN, docker hub --> search registry --> pull official registry image to your computer --> create a container from pulled image --> expose 5000 port of new container --> access this container from your working directory. 

48) ```docker container run --restart OPTION_TO_USE``` means what to do when container stops. OPTION_TO_USE may be [always, no, on-failure, unless-stopped].

49) The tag name determines where to locate in Dockerhub. To add a tag to an image in our local system

```
# retagging
docker image tag ozgurozturknet/hello-app:latest 127.0.0.1:5000/hello-app:latest
# push retagged image to local registry
docker image push 127.0.0.1:5000/hello-app:latest
```

50) To list images in LAN, open up a browser and enter the url 127.0.0.1:5000/v2/_catalog

## Compose & Swarm

### Docker Compose

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/07_docker_compose.png)


1) Docker compose can be regarded as skeleton of Docker.

2) In real life cases, one application has many services and many containers needed to run a single application. For docker compose, service=container

2.5) If there exists 2 services on a docker-compose file and we make it `up`, one container for each service is created. However, thanks to docker-compose, we can 5 containers for one of services and 2 containers for the other service(From [here](https://stackoverflow.com/questions/35565770/difference-between-service-and-container-in-docker-compose#:~:text=Services%20and%20container%20are%20related,compose%20you%20can%20handle%20services.&text=This%20compose%20file%20defines%20two%20services%2C%20web%20and%20db%20.))  

3) Docker compose is a tool to define and run multiple Docker objects. To use Docker Compose, a YAML file is used and all services were created using one command. Docker compose creates services(containers), networks and volumes.

4) Docker compose is used in development phase and not used in moving to the production.

5) Docker compose isn't coming with docker engine but it comes with docker desktop in Windows an Mac OS but it is required to install it in Linux

6) To use docker compose, Docker-compose.yaml or Docker-compose.yml or docker-compose.yaml or docker-compose.yml files should be created.

7) Use these commands to run and stop respectively

```
# Up
docker-compose up
# Detacked up
docker-compose up -d
# Down, opposite of down
docker-compose down
```

8) Docker compose componenets: CLI & yaml file.

8.5) `docker-compose build` is just creating the image. `docker-compose up` is creating the image if not created and starting a new container.

#### Docker CLI

9) Naming procedure of Docker CLI is FOLDERNAME_SERVICENAME

10) Ctrl + C stops the services and networks but ```docker-compose down``` is stopping and removing.

11) Some of Other docker compose commands are here

```
# The order of execution
docker-compose config
# Lists names of images
docker-compose images
# Prints all logs together
docker-compose logs
# Runs command in the service created by docker-compose
docker-compose exec SERVICENAME COMMAND_TO_RUN
docker-compose exec websrv ls -al
```

12) ```Docker-compose down``` doesn't remove volumes & images. It removes networks & Services.

### Docker YAML

13) YAMLS uses key-value pairs. Each YAML should start with version line. This version line means docker-compose version, not the version of YAML file. Look at workspaces/09_create_our_yaml folder

14) 4 Top level data blocks in YAML file: version, services, volumes, networks, secrets

15) depends_on: is used in creating a YAML file. DB should start firstly and app should start later.

16)  First network --> Second volume --> Third Services executed in YAML

### Docker Compose Build

17) Most people don't use docker compose build but it was used in Test environments. Docker Compose Build means to create Docker image in YAML file using Dockerfile. Look at workspaces/10_docker_compose_build

18) Replace line starting with image to ```build .```

19) If we change anything on our image after docker-compose up, we should run these 2 commands

```
# update image
docker-compose build
# Re-run compose 
docker-compose up -d
```

19.5) ports and expose are 2 similar commands in docker-compose but different. ports are maping a port from host machine to a port on container but expose is publishing a port on container to other services in the yaml file. For example, we should make `expose` operation for the service of Django app and we should make `ports` operation for the service of Nginx. For more details, check [here](https://stackoverflow.com/questions/40801772/what-is-the-difference-between-docker-compose-ports-vs-expose).

### Container Orchestration

20) This concept is used to monitor hundreds of containers in prod environment.

21) Container orchestration tools: Docker Swarm, Apache MESOS, Redhat Openshift, Kubernetes. Kubernetes is industry-standard for containers. Kubernetes is open source and triggered by Google. Kubernetes is relatively complex. Docker swarm is mostly used after Kubernetes. Docker Swarm is embedded into Docker Engine and it is easier to use than Kubernetes. Kubernetes is more useful for complex systems.

22) Docker was firstly a runtime environment. Then,

23) To use Docker Swarm, servers should be connected to each other in a fast way. This communication should be in miliseconds. Then, some ports should be open.

TCP 2377 --> Cluster management

TCP 7946 and UDP 7946 --> Communication between nodes

UDP --> Overlay Network

24) Let's imagine 4 servers exist in a network. Docker engine is installed in these 4 servers. This is called cluster. They are connected to each other. ```docker swarm init``` command is run in one server and that server became the manager. The other 3 servers were connected to this manager and these 3 servers became workers. After we configure servers, they are ready to serve. Manager manages and tracks this cluster. ETCD is installed in manager node and it can be thought as certificate authority. ETCD is an open source key value storage. The communication is carried in with TLS protocol. We don't have to deal with all of these. Docker swarm is carrying out these things. Managers are workers by default, which means containers are able to run on managers but it isn't advised for production environments.

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/08_docker_swarm.png)


25) Go to play with docker. Create 5 instances.

```
# To make an engine swarm manager with its IP
docker swarm init --advertise-addr 192.168.0.13
# To add a 2nd 3rd manager to a cluster, run the following on 1st manager and then run its output on 2nd and 3rd manager
docker swarm join-token manager
# To add a worker to a cluster, run the following on 1st manager and then run its output on worker server
docker swarm join-token worker
```

26) To list nodes in the cluster, run the following on a Leader manager.

```
docker node ls
```

27) To create 5 containers from nginx image

```
docker service create --name NAME_OF_SERVICE --replicas=5 -p 8080:80 nginx
```

28) To track a service via its name

```
docker service ps NAME_OF_SERVICE
```

### Docker Service

29) Docker Service is used in Docker Swarm Cluster. Docker Service can be thought as docker container of Docker Swarm.

30) Imperative state is old-technology in IT operations. We run the commands and wait them to happen. If it gives any error, we correct it and re-run. Declarative state is just to define commands and the system monitors them. Docker Swarm & Kubernetes are using declerative state.

37) Docker service has 2 modes: Replicated & Global. Replicated means how many replicates to create. Default mode is replicated. Global means 1 replicate on a node in a cluster. In global mode, if there exists 3 nodes, 3 containers were created.

38) After creating cluster with manager and workers, all of our commands(docker service related commands) should be run in manager node.

39) To create a service Docker Swarm(Its parameters are almost the same as docker container run)

```
docker service create --name NAME_OF_SERVICE IMAGE_NAME
```

40) Task in Docker Swarm can be thought as a inter-layer. However, to keep it simple, we consider it as container.

41)  One service may have 20 containers. It is possible.

42) To check status of services

```
docker service ps NAME_OF_SERVICE
```

43) To see details of a running service

```
docker service inspect NAME_OF_SERVICE
```

44) When we run ```docker service create``` command, it became a desired state.

45) To see logs of a service

```
docker service logs NAME_OF_SERVICE
```

46) To scale a service(It may be up or down)

```
docker service scale NAME_OF_SERVICE=3
```

47) To delete a service

```
docker service rm NAME_OF_SERVICE
```

48) To create a gloval service

```
docker service create --name NAME_OF_GLOBAL_SERVICE --mode=global nginx
```

### Overlay Network

49) Overlay is a driver like bridge or Mac based Vlan

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/09_overlay_network.png)

50) A simulation for Overlay Network and Docker Swarm

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/10_overlay_network2.png)

51) Docker swarm has a default overlay network called ingress unless we say something different.

52) We are also capable of defining user defined bridge networks.

53) If 2 services were created under same overlay network in Docker Swarm, ther are able to communicate between each other via their names. They resolve each other via their names.

54) Go to play with docker. Create 5 instances. 3 instances are managers. 2 instances are workers. RUn ```docker network ls```. It prints 5 networks. 3 of them are known by default. 2 of them (docker_gwbridge, ingress ) come with Docker Swarm. docker_gwbridge is local bridge network. It enables user defined overlay networks (ingress here) to communicate with network hardware of the computer. docker_gwbridge can be considered as bridge network of the cluster.

55) When we create a service, that service will connect to an overlay network named ingress by default. Bridge network is valid for containers of one computer. Overlay network is valid for all cluster.

56) To create an overlay network on Docker Swarm

```
#1) create an overlay network
docker network create -d overlay NETWORK_NAME

#2) Create 1st service
docker service create --name websrv --network NETWORK_NAME -p 8080:80 --replicas=3 ozgurozturknet/web

#3) Create 2nd service
docker service create --name db --network NETWORK_NAME ozgurozturknet/fakedb

```

57) Swarm Routing Match: When we create a service and publish a port, this port is published over all nodes of a cluster. Even if the node doesn't have that 
container, it sends the request taken to any node.

58) Services provides DNS service and Load Balancing service. 

59) Docker Swarm enables us to update services. Tihs operation is callled service update. Docker Swarm carries out this using ```docker service update``` command. If there exists any error in newer version, we are making rollback. To update the version of a container

```
# First version creation
docker service create --name SERVICE_NAME --network NETWORK_NAME -p 8080:80 --replicas=3 ozgurozturknet/web:v1

# Second version
docker service update --detach --update-delay 5s --update-parallelism 2 --image ozgurozturknek/web:v2 SERVICE_NAME

```

60) To roll back a newer version of a software

```
docker service rollback --detach SERVICE_NAME
```

### Docker Secret

61) Docker Secret is a Docker object that creates encrypted usernames and passwords instead of plain text. In order to use docker secret, we have to enable docker swarm.

62) 2 ways to create Docker secret: 1) From a file 2) Using CLI

```
# 1) From a file
echo "MY_USERNAME" > username.txt
echo "MY_PASSWORD" > password.txt
docker secret create SECRETOBJECT_FOR_USERNAME username.txt
docker secret create SECRETOBJECT_FOR_PASSWORD password.txt

# 2) Using CLI
echo "MY_USERNAME" | docker secret create SECRETOBJECT_FOR_USERNAME -
echo "MY_PASSWORD" | docker secret create SECRETOBJECT_FOR_PASSWORD -

```

63) To list secret objects

```
docker secret ls
```

64) To create a service object using a secret

```
docker service create -d --name SERVICE_NAME --secret SECRETOBJECT_FOR_USERNAME --secret SECRETOBJECT_FOR_PASSWORD IMAGE_NAME
```

65) After we create a secret and assign it to a service, secrets folder exist under /run directory.

66) Docker secrets aren't changed. If we want to update a docker secret, we should create a new docker secret object and then run the following:

```
docker service update --secret-rm NAME_OF_OLD_SECRET --secret-add NAME_OF_NEW_SECRET SERVICE_NAME
```

67) To hide the value of an EV using secret

![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/11_hide_EV.png)

### Docker Stack

68) Docker Stack can be thought of Docker Compose of Docker Swarm. One stack may have many services.

69) We can use our Docker-compose.yaml files in Docker Stack if their version >= 3.0

70) Images should have been craeted and uploaded into an image registry system. Therefore, there is no build lin in docker-compose.yaml file.

71) There may be a **deploy** line in docker-compose file for docker stack.

72) A ready-to-run yaml file is under workspaces/11_docker_stack

```
docker stack deploy -c docker-compose.yaml STACK_NAME_TO_CREATE
```

73) To list stacks

```
docker stack ls
```

74) To list services of a stack

```
docker stack services STACK_NAME_TO_CREATE
```

75) To remove a stack

```
docke stack rm STACK_NAME_TO_CREATE
```

## Extras

### Docker Entrypoint

1) Docker entrypoint can be overridden like below. The ENTRYPOINT command in Dockerfile is going to be ignored and a shell session will be prompted thanks to `/bin/sh`.

```
docker run --entrypoint /bin/sh my-image
```

### Windows Containers

1) Docker CE doesn't support Windows containers. Docker EE only supports Windows containers.

2) It isn't available for Linux and Mac OS X.

### Dumping And Restoring in Docker Postgresql

1) To dump a docker postgresql container to .sql file

```
docker exec -t MY_FIRST_DB pg_dumpall -c -U USERNAME > dump_`date +%d-%m-%Y"_"%H_%M_%S`.sql
```

2) To dump a database in docker container

```
docker exec -i CONTAINER_NAME /usr/bin/pg_dump -U USERNAME DB_NAME > FILENAME.sql 
```

3) To create a docker volume

```
docker volume create VOLUME_NAME
```

4) To create a postgresql container
```
docker run -it -d --name=CONTAINER_NAME -p PORT_IN_HOST:PORT_IN_CONTAINER -e POSTGRES_PASSWORD=PASSWORD_HERE -e POSTGRES_DB=DBNAME_HERE -e POSTGRES_USER=USERNAME_HERE --mount source=VOLUME_NAME_TO_MOUNT,destination=/data postgres:latest
```

5) To inspect volumes of a container created
```
docker inspect -f '{{ json .Mounts }}' CONTAINER_NAME | python3 -m json.tool
```

6) To copy a file from host to container
```
docker cp mydump.sql my_postgres:/WHERE/TO/LOCATE
```

7) To restore a database from a dumped file

```
docker exec -t my_postgres bash -c "psql -U USERNAME -d DBNAME -f /WHERE/TO/LOCATE/FILENAME.sql"
```














