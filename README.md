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

17) Docker engine has 3 components: Docker daemon(docker server), docker rest api, docker CLI. These are separate components from each other.

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

4) If we were installing Docker on Windows, it is creating a virtual machine using hyper v in the background to run docker.

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



