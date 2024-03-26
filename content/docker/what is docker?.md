---
title: what is docker | sam's notes
tags:
  - docker
draft: false
---
docker provides the ability to package and run an application in a loosely isolated environment called container.
## container 
- lightweight
- independent - they contain everything required to run an application
- leverages [[kernel namespaces]] and [[cgroups]]
- can interact with the host machine via. TCP / UDP

```
docker run --name container-name -dp 8080:3000 image-name:tag
```

above command runs a container, downloads if it does not exist locally.
- -d -> detached mode, runs in background
- -p HOST:CONTAINER -> port map, maps port 3000 in the container to 8080 in the host machine
- you could also run `docker container run`, it follows the `docker COMMAND SUBCOMMAND` semantics
### docker container sub-commands
e.g. `docker container SUBCOMMANDS`
- `ls` -> lists all running containers ( -a: all containers and -s: for size )
- `start` / `stop` -> start / stop container (-d: detached mode)
- `rm` -> delete a container
## image vs container
a container is the food while an image is the recipe.
- you cannot change an existing image.
- to create new images, you start with a base image and add layers to it.
- `dockerfile` contains those layered instructions to build an image.
### docker image sub-commands
e.g. `docker iamge SUBCOMMAND`
- `build` -> builds an image from a dockerfile
- `pull IMAGE:TAG` -> downloads an image from registry
- `push IMAGE:TAG` -> push an image to registry
- rm -> delete a container

## dockerfile
- dockerfile is the recipe to build a docker image

```dockerfile
FROM <base-image-name>:<tag-name>
RUN <install deps.>
CMD <command executed on `docker container run`>
```

To create an image capable of running node.js, run this dockerfile.

```
FROM alpine:latest
RUN 
```

related
[[creating container from scratch]] -> https://youtu.be/8fi7uSYlOdc
[[namespaces]], [[cgroups]], [[union filesystems]]
[[volume mounts]], [[bind mounts]]
[[docker-compose]]

