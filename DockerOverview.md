## Docker Overview

Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

## Docker Platform

Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight because they don’t need the extra load of a hypervisor, but run directly within the host machine’s kernel. This means you can run more containers on a given hardware combination than if you were using virtual machines. You can even run Docker containers within host machines that are actually virtual machines!

Docker provides tooling and a platform to manage the lifecycle of your containers:

Develop your application and its supporting components using containers.
The container becomes the unit for distributing and testing your application.
When you’re ready, deploy your application into your production environment, as a container or an orchestrated service. This works the same whether your production environment is a local data center, a cloud provider, or a hybrid of the two.

## Docker Engine

Docker Engine is a client-server application with these major components:

◽ A server which is a type of long-running program called a daemon process (the dockerd command).

◽ A REST API which specifies interfaces that programs can use to talk to the daemon and instruct it what to do.

◽ A command line interface (CLI) client (the docker command).

![alt Text](https://github.com/srabhayraj/Docker/blob/master/metadata/docker-engine.png)

The CLI uses the Docker REST API to control or interact with the Docker daemon through scripting or direct CLI commands. Many other Docker applications use the underlying API and CLI.
The daemon creates and manages Docker objects, such as images, containers, networks, and volumes.

## Docker can be used for

Fast, consistent delivery of your applications

Docker streamlines the development lifecycle by allowing developers to work in standardized environments using local containers which provide your applications and services. Containers are great for continuous integration and continuous delivery (CI/CD) workflows.

Consider the following example scenario:

◽ Your developers write code locally and share their work with their colleagues using Docker containers.
◽ They use Docker to push their applications into a test environment and execute automated and manual tests.
◽ When developers find bugs, they can fix them in the development environment and redeploy them to the test environment for testing and validation.
◽ When testing is complete, getting the fix to the customer is as simple as pushing the updated image to the production environment.

