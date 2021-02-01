# My-Docker-Notes
Including My Docker Notes

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

40) If we don't specify an app while creating the container, the line in CMD will run. ENTRYPOINT is the same as CMD. The only difference is that ENTRYPOINT can't be changed with ```docker run``` command. In every Dockerfile, there must be either a CMD or ENTRYPOINT. If both CMD and ENTRYPONT exist in a Dockerfile, Docker adds content of CMD to ENTRYPOINT as a parameter. The purpose of using CMD and ENTRYPOINT together is to facilitate versioning problems.

41) Exec form is the former. Shell form is the latter. Exec form means run the content as it is but Shell form means open up a shell and run the content. If we are using CMD and ENTRYPOINT together, we couldn't use Shell form. Thus, we have to use Exec form.

```
#Exec form
CMD ["java","app1"]
#Shell form
CMD java app1

```
![Docker Image](https://github.com/MuhammedBuyukkinaci/My-Docker-Notes/blob/master/img/06_exec_shell.png)

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














