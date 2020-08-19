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


# Part 2: Build and run your image

## Introduction

Now that you’ve set up your development environment, you can begin to develop containerized applications. In general, the development workflow looks like this:

1. Create and test individual containers for each component of your application by first creating Docker images.

2. Assemble your containers and supporting infrastructure into a complete application.

3. Test, share, and deploy your complete containerized application.

In this stage of the tutorial, let’s focus on step 1 of this workflow: creating the images that your containers will be based on. Remember, a Docker image captures the private filesystem that your containerized processes will run in; you need to create an image that contains just what your application needs to run.

## Set up

Let us download the node-bulletin-board example project. This is a simple bulletin board application written in Node.js.

### Git

If you are using Git, you can clone the example project from GitHub:
```
git clone https://github.com/dockersamples/node-bulletin-board
cd node-bulletin-board/bulletin-board-app
```

## Define a container with Dockerfile

After downloading the project, take a look at the file called Dockerfile in the bulletin board application. Dockerfiles describe how to assemble a private filesystem for a container, and can also contain some metadata describing how to run a container based on this image.

For more information about the Dockerfile used in the bulletin board application, see Sample Dockerfile.

## Build and test your image

Now that you have some source code and a Dockerfile, it’s time to build your first image, and make sure the containers launched from it work as expected.

Make sure you’re in the directory node-bulletin-board/bulletin-board-app in a terminal or PowerShell (or docker terminal) using the cd command. Run the following command to build your bulletin board image:
```
docker build --tag bulletinboard:1.0 .
```
You’ll see Docker step through each instruction in your Dockerfile, building up your image as it goes. If successful, the build process should end with a message Successfully tagged bulletinboard:1.0.
```
Windows users:

This example uses Linux containers. Make sure your environment is running Linux containers by right-clicking on the Docker logo in your system tray, and clicking Switch to Linux containers. Don’t worry - all the commands in this tutorial work the exact same way for Windows containers.

You may receive a message titled ‘SECURITY WARNING’ after running the image, noting the read, write, and execute permissions being set for files added to your image. We aren’t handling any sensitive information in this example, so feel free to disregard the warning in this example.
```

## Run your image as a container

1. Run the following command to start a container based on your new image:
```
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```
There are a couple of common flags here:

◽ --publish asks Docker to forward traffic incoming on the host’s port 8000 to the container’s port 8080. Containers have their own private set of ports, so if you want to reach one from the network, you have to forward traffic to it in this way. Otherwise, firewall rules will prevent all network traffic from reaching your container, as a default security posture.<br />
◽ --detach asks Docker to run this container in the background.<br />
◽ --name specifies a name with which you can refer to your container in subsequent commands, in this case bb.<br />

2. Visit your application in a browser at localhost:8000. You should see your bulletin board application up and running. At this step, you would normally do everything you could to ensure your container works the way you expected; now would be the time to run unit tests, for example.

3. Once you’re satisfied that your bulletin board container works correctly, you can delete it:
```
docker rm --force bb
```
The --force option stops a running container, so it can be removed. If you stop the container running with docker stop bb first, then you do not need to use --force to remove it.

{In the first command if we write as it is then error occurs since the output generated in docs after the build command is "Successfully tagged bulletinboard:1.0" and the output generated in terminal is "Successfully tagged bulletin:1.0". So to run the first command we have to write "docker run --publish 8000:8080 --detach --name bb bulletin:1.0" instead of "docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0". Now the command will run and we will get our image}

## Sample Dockerfile

Writing a Dockerfile is the first step to containerizing an application. You can think of these Dockerfile commands as a step-by-step recipe on how to build up your image. The Dockerfile in the bulletin board app looks like this:
```
# Use the official image as a parent image.
FROM node:current-slim

# Set the working directory.
WORKDIR /usr/src/app

# Copy the file from your host to your current location.
COPY package.json .

# Run the command inside your image filesystem.
RUN npm install

# Add metadata to the image to describe which port the container is listening on at runtime.
EXPOSE 8080

# Run the specified command within the container.
CMD [ "npm", "start" ]

# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
```

The dockerfile defined in this example takes the following steps:

◽ Start FROM the pre-existing node:current-slim image. This is an official image, built by the node.js vendors and validated by Docker to be a high-quality image containing the Node.js Long Term Support (LTS) interpreter and basic dependencies.<br />
◽ Use WORKDIR to specify that all subsequent actions should be taken from the directory /usr/src/app in your image filesystem (never the host’s filesystem).<br />
◽ COPY the file package.json from your host to the present location (.) in your image (so in this case, to /usr/src/app/package.json)<br />
◽ RUN the command npm install inside your image filesystem (which will read package.json to determine your app’s node dependencies, and install them)<br />
◽ COPY in the rest of your app’s source code from your host to your image filesystem.<br />


# Part 3: Share images on Docker Hub

## Introduction

At this point, you’ve built a containerized application described in Part 2 on your local development machine.

The final step in developing a containerized application is to share your images on a registry like Docker Hub, so they can be easily downloaded and run on any destination machine.

## Set up your Docker Hub account

If you don’t have a Docker ID, follow these steps to create one. A Docker ID allows you to share images on Docker Hub.

1. Visit the Docker Hub sign up page.
2. Fill out the form and submit to create your Docker ID.
3. Verify your email address to complete the registration process.
4. Click on the Docker icon in your toolbar or system tray, and click Sign in / Create Docker ID.
5. Fill in your new Docker ID and password. After you have successfully authenticated, your Docker ID appears in the Docker Desktop menu in place of the ‘Sign in’ option you just used.

You can also sign into Docker Hub from the command line by typing docker login.

## Create a Docker Hub repository and push your image

```
Note: Before creating a repository, ensure you’ve set up your Docker Hub account and have connected it to your Docker Desktop.
```

Now let’s create your first repository, and push your bulletin board image to Docker Hub.
1. Click on the Docker icon in your menu bar, and navigate to Repositories > Create. You’ll be redirected to the Create Repository page on Docker Hub.
2. Type the repository name as bulletinboard and click Create at the bottom of the page. Do not fill any other details for now.
3. You are now ready to share your image on Docker Hub, however, there’s one thing you must do first: images must be namespaced correctly to share on Docker Hub. Specifically, you must name images like <Your Docker ID>/<Repository Name>:<tag>.

Make sure you’re in the node-bulletin-board/bulletin-board-app directory in a terminal or PowerShell then and run:
```
docker tag bulletinboard:1.0 <Your Docker ID>/bulletinboard:1.0
```
{In this we have to give command  "$ docker tag bulletin:1.0 abhayrajsr/bulletinboard:1.0", since our tag is bulletin:1.0}
4. Finally, push your image to Docker Hub:
```
docker push <Your Docker ID>/bulletinboard:1.0
```
Visit your repository in Docker Hub, and you’ll see your new image there. Remember, Docker Hub repositories are public by default.
