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

10) 
Before 2000: 2 Hardwares --> 2 different OS's -->  2 different apps
2000 - 2007: 1 hardware --> 1 virtualization software --> 2 different OS's --> 2 different apps
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

16) Till 2017, docker's CLI was basic. Then, it became more complex to do more jobs. The first command is before 2017, the latter command is after 2017. These 2 commands are the same.

```
docker run hello-world
```

```
docker container run hello-world
```

18) The new version has this pattern: ``` docker MANAGEMENT_COMMAND COMMAND_TO_USE ```

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


40) To pull an image from docker hub

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

47)



