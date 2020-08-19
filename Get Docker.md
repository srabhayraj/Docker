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

### Install Docker EE

## Install using the repository

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
