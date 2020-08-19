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

[!alt Text](https://github.com/srabhayraj/Docker/blob/master/metadata/Container%402x.png)

[!alt Text](https://github.com/srabhayraj/Docker/blob/master/metadata/VM%402x.png)
