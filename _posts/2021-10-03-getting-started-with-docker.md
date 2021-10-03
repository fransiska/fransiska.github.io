---
layout: post
title: Getting Started with Docker
tags: [docker]
---

### What is Docker

Docker is basically a virtual machine. The special thing is that the minimal image that it has is based on a Linux distro called Alpine, and the image size is really small, just about 5MB! Of course there are images based on Debian and Ubuntu as well, [with bunch of different versions](https://hub.docker.com/_/debian?tab=tags&page=1&ordering=last_updated).

It's useful that when you try to test a software, you don't need to install or create the environment for the software in your actual PC, since you'll usually you'll end up with dependencies problem and it takes time to solve, but instead you can just launch this Docker container and interact with the software from your PC using its exposed ports.

First, install Docker for Mac [here](https://docs.docker.com/desktop/mac/install/). It will install a GUI and an icon in the menu bar. You don't need to sign in to use Docker.

### The Basic

#### Image

Is basically an image. A set of installed OS and softwares that you can either create one or [download from Docker Hub](https://hub.docker.com/search?type=image) (Like git, you can do docker pull). List your images by 

```bash
docker images 
```

#### Run

In order to use the image, you need to run it. For example, let's run alpine.

```bash
docker run alpine
```

It will actually do nothing since there's no process set in the image to keep the system running.

#### Container

When we run an image, it will create a container, an instance of the image. It will be automatically assigned a unique name. The following will list all of the containers that we have, including the exited ones.

```bash
docker container ls -a
```

We can make the container not exit. If we do:

```bash
docker run -it alpine
```

It will create a new container and we directly entered the container's command line! If we press `ctrl-d` it will exit. We can re-run the container by referencing the name on the last column of `docker container ls -a`. `-i` is used so that we can enter the command line again.

```bash
docker container start -i <container_name>
```

However, the `-it` is linked to the container. So even if we restarted the container from the first run, it will always exit. (I'm still not sure with this concept)

If we keep on running the image, we will end up with a bunch of containers. 

```bash
docker rm <container_name>
docker rm $(docker ps --filter status=exited -q) # Remove all stopped containers
```

### Building Your Image Own Image

If we create a `Dockerfile` we can `build` our own image. We can base it off other image and install extra stuff in there. Then, there's also `compose` where we can launch multiple containers at once.

For example, create a new folder, and inside that folder, create a new file named `Dockerfile` with the content

```
FROM alpine
```

If we then run

```bash
docker build . -t test
```

It will create a new image named test based off the alpine image. If we do `docker images` you can see it's listed there. We can then run it by

```
docker run -it test
```

Yay! I guess that's my first docker image =p My next goal is to run php laravel on docker. There are images that provides that, but they seem to be so big (500MB+) I just want to see if it is possible to make a smaller one. But maybe it's not a good idea, not something that I want to spend my time on... there are [alpine](https://hub.docker.com/_/php?tab=tags&page=1&ordering=last_updated&name=alpine) based ones. I think I can try the [bitnami one](https://hub.docker.com/r/bitnami/laravel) or try the official [Laravel Sail](https://laravel.com/docs/8.x#getting-started-on-macos).
