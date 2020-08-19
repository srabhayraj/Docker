# Part 1: Orientation and Setup

## Docker concepts

Docker is a platform for developers and sysadmins to build, run, and share applications with containers. The use of containers to deploy applications is called containerization. Containers are not new, but their use for easily deploying applications is.

Containerization is increasingly popular because containers are:

◽ Flexible: Even the most complex applications can be containerized.<br />
◽ Lightweight: Containers leverage and share the host kernel, making them much more efficient in terms of system resources than virtual machines.<br />
◽ Portable: You can build locally, deploy to the cloud, and run anywhere.<br />
◽ Loosely coupled: Containers are highly self sufficient and encapsulated, allowing you to replace or upgrade one without disrupting others.<br />
◽ Scalable: You can increase and automatically distribute container replicas across a datacenter.<br />
◽ Secure: Containers apply aggressive constraints and isolations to processes without any configuration required on the part of the user.<br />

## Containers and virtual machines

A container runs natively on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

By contrast, a virtual machine (VM) runs a full-blown “guest” operating system with virtual access to host resources through a hypervisor. In general, VMs incur a lot of overhead beyond what is being consumed by your application logic.


<img align="left" alt="container" width="440px" src="https://github.com/srabhayraj/Docker/blob/master/metadata/Container%402x.png" />
<img align="right" alt="vm" width="440px" src="https://github.com/srabhayraj/Docker/blob/master/metadata/VM%402x.png" />

## Set up your Docker environment

### Download and install Docker Desktop

Docker Desktop is an easy-to-install application for your Mac or Windows environment that enables you to start coding and containerizing in minutes. Docker Desktop includes everything you need to build, run, and share containerized applications right from your machine.

◽ [Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)
◽ [Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)

### Test Docker version

After you’ve successfully installed Docker Desktop, open a terminal and run docker --version to check the version of Docker installed on your machine.
```
$ docker --version
Docker version 19.03.12, build 48a66213fe
```

### Test Docker installation

1. Test that your installation works by running the hello-world Docker image:
```
    $ docker run hello-world

    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ca4f61b1923c: Pull complete
    Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
    Status: Downloaded newer image for hello-world:latest

    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    ...
```

2. Run docker image ls to list the hello-world image that you downloaded to your machine.

3. List the hello-world container (spawned by the image) which exits after displaying its message. If it is still running, you do not need the --all option:
```
  $ docker ps --all

    CONTAINER ID     IMAGE           COMMAND      CREATED            STATUS
    54f4984ed6a8     hello-world     "/hello"     20 seconds ago     Exited (0) 19 seconds ago
```
