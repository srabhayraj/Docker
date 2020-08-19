## Get Docker

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

[Get Docker Desktop for Windows](https://docs.docker.com/docker-for-windows/install/)

[Get Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/install/)

[Get Docker Desktop for Linux](https://docs.docker.com/engine/install/)

## RHEL

Docker is available in two editions: Community Edition (CE) and Enterprise Edition (EE).

Docker Community Edition (CE) is ideal for developers and small teams looking to get started with Docker and experimenting with container-based apps.

Docker Enterprise Edition (EE) is designed for enterprise development and IT teams who build, ship, and run business critical applications in production at scale.

## Get Docker EE for Red Hat Enterprise Linux

### Uninstall old versions
```
$ sudo yum remove docker \
                  docker-common \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine
```

## Install Docker EE

### Install using the repository

*SET UP THE REPOSITORY*

1. Remove any existing Docker repositories from /etc/yum.repos.d/.

2. Temporarily store the Docker EE repository URL you noted down in the prerequisites in an environment variable. This will not persist when the current session ends.
```
$ export DOCKERURL='<DOCKER-EE-URL>'
```

3. Store your Docker EE repository URL in a yum variable in /etc/yum/vars/. This command relies on the variable you stored in the previous step.
```
$ sudo -E sh -c 'echo "$DOCKERURL/rhel" > /etc/yum/vars/dockerurl'
```

4. Store your OS version string in /etc/yum/vars/dockerosversion. Most users should use 7, but you can also use the more specific minor version, starting from 7.2.
```
$ sudo sh -c 'echo "7" > /etc/yum/vars/dockerosversion'
```

5. Install required packages. yum-utils provides the yum-config-manager utility, and device-mapper-persistent-data and lvm2 are required by the devicemapper storage driver.
```
$ sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2
```

6. Enable the extras RHEL repository. This ensures access to the container-selinux package which is required by docker-ee.
```
$ sudo yum-config-manager --enable rhel-7-server-extras-rpms
```

7. Depending on cloud provider, you may also need to enable another repository.
```
For AWS:

$ sudo yum-config-manager --enable rhui-REGION-rhel-server-extras
Note: REGION here is literal, and does not represent the region your machine is running in.

For Azure:

$ sudo yum-config-manager --enable rhui-rhel-7-server-rhui-extras-rpms
Use the following command to add the stable repository:

$ sudo -E yum-config-manager \
    --add-repo \
    "$DOCKERURL/rhel/docker-ee.repo"
```

### Install Docker EE

1. Install the latest version of Docker EE, or go to the next step to install a specific version.
```
$ sudo yum -y install docker-ee
```

2. The sort -r command to sort the results by version number, highest to lowest, and is truncated.<br />
This yum list command only shows binary packages. To show source packages as well, omit the .x86_64 from the package name.
```
$ sudo yum list docker-ee.x86_64  --showduplicates | sort -r

docker-ee.x86_64         17.06.ee.2-1.el7.rhel          docker-ee-stable-17.06
```

```
$ sudo yum -y install <FULLY-QUALIFIED-PACKAGE-NAME>
```
Docker is installed but not started. The docker group is created, but no users are added to the group.

3. Edit /etc/docker/daemon.json. If it does not yet exist, create it. Assuming that the file was empty, add the following contents.
```
{
  "storage-driver": "devicemapper"
}
```

4. Start Docker.
```
$ sudo systemctl start docker
```

5. Verify that Docker EE is installed correctly by running the hello-world image.
```
$ sudo docker run hello-world
```

## Get Docker CE for CentOS

### Install from a package

1. Go to https://download.docker.com/linux/centos/7/x86_64/stable/Packages/ and download the .rpm file for the Docker version you want to install.

2. Install Docker CE, changing the path below to the path where you downloaded the Docker package.
```
$ sudo yum install /path/to/package.rpm
```
Docker is installed but not started. The docker group is created, but no users are added to the group.

3. Start Docker.
```
$ sudo systemctl start docker
```

4. Verify that docker is installed correctly by running the hello-world image.
```
$ sudo docker run hello-world
```
This command downloads a test image and runs it in a container. When the container runs, it prints an informational message and exits.

### Uninstall Docker CE

Uninstall the Docker package:
```
$ sudo yum remove docker-ce
```

Images, containers, volumes, or customized configuration files on your host are not automatically removed. To delete all images, containers, and volumes:
```
$ sudo rm -rf /var/lib/docker
```
You must delete any edited configuration files manually.

## Configure Docker to start on boot

Most current Linux distributions (RHEL, CentOS, Fedora, Ubuntu 16.04 and higher) use systemd to manage which services start when the system boots. 

systemd
```
$ sudo systemctl enable docker
```
To disable this behavior, use disable instead.
```
$ sudo systemctl disable docker
```

## Docker Commands


Command	Description
docker attach	-> Attach local standard input, output, and error streams to a running container
docker build	-> Build an image from a Dockerfile
docker checkpoint	-> Manage checkpoints
docker commit	-> Create a new image from a container’s changes
docker config	-> Manage Docker configs
docker container	-> Manage containers
docker cp	-> Copy files/folders between a container and the local filesystem
docker create	-> Create a new container
docker deploy	-> Deploy a new stack or update an existing stack
docker diff	-> Inspect changes to files or directories on a container’s filesystem
docker events	-> Get real time events from the server
docker exec	-> Run a command in a running container
docker export	-> Export a container’s filesystem as a tar archive
docker history	-> Show the history of an image
docker image	-> Manage images
docker images	-> List images
docker import	-> Import the contents from a tarball to create a filesystem image
docker info	-> Display system-wide information
docker inspect	-> Return low-level information on Docker objects
docker kill	-> Kill one or more running containers
docker load	-> Load an image from a tar archive or STDIN
docker login	-> Log in to a Docker registry
docker logout	-> Log out from a Docker registry
docker logs	-> Fetch the logs of a container
docker network	-> Manage networks
docker node	-> Manage Swarm nodes
docker pause	-> Pause all processes within one or more containers
docker plugin	-> Manage plugins
docker port	-> List port mappings or a specific mapping for the container
docker ps	-> List containers
docker pull	-> Pull an image or a repository from a registry
docker push	-> Push an image or a repository to a registry
docker rename	-> Rename a container
docker restart	-> Restart one or more containers
docker rm	-> Remove one or more containers
docker rmi	-> Remove one or more images
docker run	-> Run a command in a new container
docker save	-> Save one or more images to a tar archive (streamed to STDOUT by default)
docker search	-> Search the Docker Hub for images
docker secret	-> Manage Docker secrets
docker service	-> Manage services
docker stack	-> Manage Docker stacks
docker start	-> Start one or more stopped containers
docker stats	-> Display a live stream of container(s) resource usage statistics
docker stop	-> Stop one or more running containers
docker swarm	-> Manage Swarm
docker system	-> Manage Docker
docker tag	-> Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
docker top	-> Display the running processes of a container
docker unpause	-> Unpause all processes within one or more containers
docker update	-> Update configuration of one or more containers
docker version	-> Show the Docker version information
docker volume	-> Manage volumes
docker wait	-> Block until one or more containers stop, then print their exit codes

