---
title: basic docker commands
tags:
  - docker
  - containerization
  - cli
draft: false
---
docker provides the ability to package and run an application in a loosely isolated environment called container.
## docker cli
the docker engine consists of three parts:
- docker cli
- docker rest api
- docker daemon

When you run a command, behind the scenes the client sends a request through the REST API to the docker daemon which takes care of images, containers and other resources.

docker management commands like compose, image, system, etc. follow this semantics.
```
docker COMMAND SUBCOMMAND [options] [arguments]
```
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
- `ls` -> lists all running containers
	- `-a`: all containers and `-s`: for size
	- same as `docker ps` or `docker container ps`
- `start` / `stop` -> start / stop container (-d: detached mode)
- `rm NAME|ID1 NAME|ID2 ...` -> delete a container (you need to stop it first)
- `prune` -> delete all stopped containers
- `exec NAME|ID COMMAND` -> execute a command inside a container
	- e.g., docker exec 918ffd ps -a
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
- `rm NAME|ID1 NAME|ID2 ...` -> delete an image
	- you should always delete all containers related to the image first, then delete the image. 
- `prune` -> removes "dangling images" - these are images that have no name.
	- `-a` -> removes all images not associated with a container.

`docker system prune` -> removes everything:
- all stopped containers
- all networks not used by at least one container
- all dangling images
- unused build cache
### copy, history, commit
you can copy files from host machine to your container and vice versa using `docker cp` or `docker container cp`. If you are mentioning the container path, it should be of this format: `CONTAINER-ID|NAME:CONTAINER-FILE-PATH`.

```
docker cp SOURCE DEST
---
e.g., docker cp /hello.txt c99d19efdab3:/usr/src/app/hello.txt
```

since we changed the container, you can use `docker diff ID|NAME` command to check all the changes made in the container. A=added; D=deleted; C=changed.

you can build an image from an container using `docker commit`. its generally better to use a dockerfile instead as defining the changes to the Dockerfile is much more sustainable method of managing changes.

```
docker commit CONTAINER-ID|NAME IMAGE-NAME
```
## related
![[contents]]