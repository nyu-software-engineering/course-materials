---
layout: presentation
title: Containers
permalink: /slides/containers/
---

class: center, middle

# Containers

Standardized efficient highly-portable boxes within which to run software.

---

# Agenda

1. [Overview](#overview)
1. [A Brief History of Virtualization](#virtualization)
1. [Containers in Detail](#containers)
1. [Try Docker](#docker-example)
1. [Deploy A Containerized App](#deploy)
1. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

A container is a small, standardized, portable, self-contained virtual environment within which application code can run.

--

- Containers represent a logical "next step" in the evolutionary history of system virtualization.

---

name: virtualization

# A Brief History of Virtualization

--

## Bare metal machines

In ancient times, a server was a physical device affectionately called a "box" or a "machine".

--

- These boxes, like your personal devices, typically had one set of hardware, an operating system, and some applications installed on them.

---

template: virtualization

## Bare metal machines (continued)

Bare metal machines give their users complete control over the machine

--

- complete control over hardware

--

- complete control over software

--

- physical isolation - no "noisy neighbor" problem, no shared infrastructure

--

- potential for greater security

--

- potential for greater performance (i.e. for High Performance Computing)

---

template: virtualization

## Bare metal machines (coninued again)

![A bare metal machine](https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Finsurancehub.com%2Fwp-content%2Fuploads%2F2016%2F09%2Flaptop-fire-insurancehub.jpg&f=1&nofb=1)

---

template: virtualization

## Bare metal machines (continued once more)

These boxes had (and still have) some inconvenient properties.

--

- The boxes take up a lot of physical space.

--

- Maintaining a machine is a lot of [expensive] work

--

- The configuration of one bare metal machine is difficult to replicate on another with different hardware.

--

- The hardware has finite capacity to scale up.

---

template: virtualization

## Blade and rack servers

Computer hardware, loaded with the operating system and applications, was eventually reduced to a single hardware card.

--

- Many such cards are slotted into a single "box", reducing space and sharing a single power supply for multiple machines.

--

- Easy to set up for load balancing, where all machines in the box share the load.

--

- Rack servers and blade servers are differentiated by how much infrastructure is shared by the machines.

--

- Rack servers are more self-contained machins, each including their own storage, cooling fans, power supply, etc. Blade servers often contain just the CPU, network I/O cards, memory, and perhaps a bit of storage.

--

- In either form, blade and rack servers thus share some physical infrastructure, with rack servers sharing more than blade servers.

---

template: virtualization

## Blade and rack servers (continued)

![A blade server](https://external-content.duckduckgo.com/iu/?u=http%3A%2F%2Fwww.rackmountmart.com%2Fprodspics%2Frm8003-01.jpg&f=1&nofb=1)

---

template: virtualization

## Blade and rack servers (continued again)

Blade servers and rack servers are not without their complications.

--

- They tend to require more cooling than dedicated bare metal servers.

--

- As with bare metal machines, any hardware is likely to quickly become out-of-date depreciate in value over time.

---

template: virtualization

## Virtual machines

With increases in computing power, an entire machine could be virtualized

--

- hardware and software are emulated

--

- one physical "host" machine can now run many emulated virtual machines

--

- multiple operating systems can even be run on a single host machine.

--

- higher-level "hypervisor" software launches, monitors, and manages the virtual machines on the host

--

- virtual machines are sandboxed, protecting against one consuming the resources of another.

---

template: virtualization

## Virtual machines (again)

![Virtual machine](../images/virtual_machine_diagram.png)

---

template: virtualization

## Virtual machines (continued again)

For most use-cases, virtual machines have significant benefits over traditional bare metal, rack, and blade servers.

--

- virtual machines reduced the time to provision, or set up, a server, compared to their physical machine counterparts

--

- virtual machines reduce the risk of choosing inappropriate hardware

--

- virtual machines simplify the choice of hardware and software for the consumer

---

template: virtualization

## Virtual machines (continued once more)

But as with all technology, virtual machines have their downsides.

--

- each virtual machine encapsulates its own operating system

--

- this adds significant memory overhead and a large footprint to each virtual machine

--

- virtual machines are also not very portable because of this

---

template: virtualization

## Containers

Containers are a refinement of the concept of a virtual machine.

--

- containers only include the bare minimum environment setup necessary for the application they have hosted within them to run.

--

- containers do not encapsulate the operating system, and are thus small footprint and highly portable

--

![Virtualization evolution](https://knowledge.kitchen/mediawiki/images/d/d3/Comparison_of_server_virtualization_systems.png)

---

name: containers

# Containers in Detail

--

## Advantages

Containers are virtual environments that contain the bare minimum necessary to deploy an application on any machine - physical or virtual.

--

- removes compatibility problems moving a container from one machine to another.

---

template: containers

## Players

Docker is the leader in the container field. However, it is still an open competitive new field:

- Docker
- [Kubernetes](https://kubernetes.io/)
- CoreOS [rkt](https://coreos.com/rkt/)

--

The main cloud services providers all support containers:

- Amazon's [Elastic Container Service](https://aws.amazon.com/ecs/) supports containers
- [Microsoft Azure](t.com/en-us/azure/containers/) supports containers
- Google Cloud [Kubernetes Engine](https://cloud.google.com/kubernetes-engine/) supports containers
- IBM Cloud's [Kubernetes Service](https://www.ibm.com/cloud/container-service/) supports containers
- Red Hat's [OpenShift Container Platform](https://www.openshift.com/products/container-platform) supports containers

---

template: containers

## False Dichotomy

“Kubernetes vs. Docker” is a false dichotomy. Docker and Kubernetes are not exactly competitors...

--

- Docker is a Container Platform

--

- Kubernetes is a Container Orchestrator

--

- ... [read more](https://www.sumologic.com/blog/kubernetes-vs-docker/) about this

---

template: containers

## Image

A container's configuration is specified in its "image"

- images are the stuff from which containers are made

--

- i.e. containers are instances of an image

--

- creating a container is achieved by designing an image and instantiating it

--

- a single image can be instantiated into many containers, which can then be run across many different machines in a cloud hosting environment, if desired

---

template: containers

## Registry

A container registry is a central server that hosts images

--

- allow sharing of those images with teammates and/or the public

--

- essentially the same concept as repositories in version control

--

- Examples: [Docker Hub](https://hub.docker.com/) and [Docker Store](https://store.docker.com/)

---

template: containers

## Security

Containers do not run in total isolation from one-another.

--

- This currently makes containers a bit less secure than more isolated environments.

--

- However, containers can improve the reliability of testing, since since testing, development, and deployment environments are all set up the same way - as reproducible, portable containers.

--

- [Many traditional operations experts have concerns](https://www.youtube.com/watch?v=PivpCKEiQOQ)

---

template: containers

## Automation

Containers can be integrated with automation tools, such as Travis CI or Jenkins or via settings within container registries such as Docker Hub.

--

- every time a build or some other automation is complete, a container containing all security tests can be run

--

- see more on [linking GitHub to Docker](https://docs.docker.com/docker-hub/builds/link-source/) for [automated builds on commit](https://docs.docker.com/docker-hub/builds/#link-to-a-hosted-repository-service)

---

name: docker-example

# Try Docker

--

## Install and run it

In order to build and run docker images and containers, you will need to install it.

--

- Install the [Docker Desktop client](https://www.docker.com/products/docker-desktop)

--

- Create an acount at [Docker Hub](https://hub.docker.com/).

--

- Once Docker Desktop is installed, run it.

---

template: docker-example

## Download and run an image

Now download and run a container built from an image stored on the Docker Hub registry.

--

```bash
docker run -ti bloombar/se_welcome:latest
```

--

- This image will be instantiated into a container that runs on your local machine.

--

- The container will automatically execute a python script.

--

- You can poke around the files in the container by opening up a `bash` shell within the container.... quit the container, if already running, and then run - you will notice it looks and acts like a virtual machine:

```bash
docker run -ti bloombar/se_welcome:latest bash
```

---

template: docker-example

## Dockerfile

The configuration of each image is written in a `Dockerfile` build script - this is what I used to create the example image:

```bash
# in Docker, it is common to base a new image on a previously-created image
# Use an official Python runtime image as a parent image to base this image on
FROM python:2.7-slim
# Set the working directory within the image to /app
WORKDIR /app
# the ADD command is how you add files from your local machine into a Docker image
# Copy the current directory contents into the container at /app
ADD . /app
# Install any needed packages specified in requirements.txt
# in Python, a requirements.txt file is a way of indicating dependencies in a way that the package manager, pip, can understand
RUN pip install --trusted-host pypi.python.org -r requirements.txt
# by default Docker containers are closed off to the external world
# Make port 80 available to the world outside this container
EXPOSE 80
# Define an environment variable... this will be available to programs running inside the container
ENV NAME World
# Run app.py when the container launches
CMD ["python", "app.py"]
```

---

template: docker-example

## Dockerfile (continued)

Notice that the Dockerfile for this example image references another image named `python:2.7-slim`.

--

- It is common convention to use an existing image as the basis for a new image.

--

- Search Docker Hub or Docker Store for an image that is suitably close to what you need, and then create a new Dockerfile that builds on top of it.

--

- Docker builds images in layers... it builds dependency images first before building the additional changes you have specified in your Dockerfile.

---

template: docker-example

## Example Dockerfile for React.js front-end

```
# start from the node v16 base image
FROM node:16

# create an app directory within the image...
# WORKDIR /app

# install dependencies into the image - doing this first will speed up subsequent builds, as Docker will cache this step
COPY package*.json ./
RUN npm install

# copy the remaining app source code into the default directory within the image
COPY . .

# expose port 4000 to make it available to the docker daemon
EXPOSE 4000

# define the runtime command that will be executed when a container is made from the image
CMD [ "npm", "start" ]
```

---

template: docker-example

## Example Dockerfile for Express.js back-end

```
# start from the node v16 base image
FROM node:16

# create an app directory within the image...
# WORKDIR /app

# install dependencies into the image - doing this first will speed up subsequent builds, as Docker will cache this step
COPY package*.json ./
RUN npm install

# copy the remaining app source code into the default directory within the image
COPY . .

# install dependencies into the image
RUN npm install

# expose port 3000 to make it available to the docker daemon
EXPOSE 3000

# define the runtime command that will be executed when a container is made from the image
CMD [ "node", "server.js" ]
```

---

template: docker-example

## Try running a containerized React.js / Express.js app

We have containerized a [simple React.js / Express.js application](https://github.com/nyu-software-engineering/data-storage-example-app).

--

Launch the React.js front-end as a background process on port 4000:

--

```bash
docker run -p 4000:4000 -d bloombar/data-storage-example-app-front-end
```

--

Launch the Express.js back-end as a background process on port 3000:

```bash
docker run -p 3000:3000 --restart unless-stopped -d bloombar/data-storage-example-app-back-end
```

--

Open your favorite web browser and navigate to http://localhost:4000

---

template: docker-example

## Basic Docker commands

- Log in to Docker Hub (necessary to download images): `docker login`

--

- Search Docker Hub for images by keyword: `docker search <search_term>`

--

- Build an image from the Dockerfile in the current dir: `docker build .`

--

- Push an image to the Docker Hub registry: `docker push <image_name>:<tag_name>`

--

- Pull an image from the Docker Hub registry: `docker pull <image_name>:<tag_name>`

--

- View available Docker images on local machine: `docker images`

--

- Delete an image: `docker rmi <image_unique_id>`

--

- View all containers available on the local machine: `docker ps -a`

--

- Stop a currently-running container: `docker kill <container_name_or_id>`

---

template: docker-example

## Allowing networking

By default, containers do not have access to the host machine's standard input/output and networking ports.

--

- To run a container that forwards standard input to the container and forwards connections on one of the host machine's ports to the same port on the container:

```bash
docker run --rm -ti -p 45678:45678 ubuntu:latest bash
```

--

- To open several ports, repeat the -p option:

```bash
docker run --rm -ti -p 45678:45678 -p 45679:45679 ubuntu:latest bash
```

--

- To let the machine itself decide which outside ports to use, don't include the outside ports in the command:

```bash
docker run --rm -ti -p 45678 -p 45679 ubuntu:latest bash
```

---

name: deploy

# Deploy A Containerized App

--

## Moving containers to production

Because of their small footprint and high portability, containers are simple to deploy on cloud compute providers, such as Amazon AWS, Microsoft Azure, Heroku, or Digital Ocean.

--

- A completely containerized app may consist of several distinct container images, with the back-end logic, database, and static front-end content all housed in separate containers made from separate images.

--

- Digital Ocean is a hosting provider that makes deploying Docker containers quite simple - you can launch a **Droplet** running a Docker container for free (to start) with a [referral link](https://m.do.co/c/4d1066078eb0)

--

- Check out [this example React.js / Express.js app](https://github.com/nyu-software-engineering/data-storage-example-app) containing both a containerized front-end and back-end. Check out the Dockerfiles.

--

- MongoDB provides an easy-to-follow tutorial for [running a containerized MongoDB instance](https://www.mongodb.com/compatibility/docker) locally.

--

- In a **continuous deployment** setup, a new Docker image would be generated with every change to the codebase, posted to Docker Hub, pulled to a remote server, and instantiated into a running container - [see an example](https://maximorlov.com/automate-your-docker-deployments/).

---

name: conclusions

# Conclusions

--

You have now had a brief introduction to how container technology fits into the evolution of computer virtualization.

--

- Thank you. Bye.
