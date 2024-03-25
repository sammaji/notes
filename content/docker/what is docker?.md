---
title: intro
tags:
  - docker
draft: false
---
docker provides the ability to package and run an application in a loosely isolated environment called container.

## container 
- lightweight
- independent - they contain everything required to run an application
- leverages [[kernel namespaces]] and [[cgroups]]


```
docker run --name container-name -dp 8080:3000 image-name:tag
```

above command runs a container
-d -> detached mode, runs in background
-p HOST:CONTAINER -> port map, maps port 3000 in the container to 8080 in the host machine

## dockerfile

related
[[creating container from scratch]] -> https://youtu.be/8fi7uSYlOdc
[[namespaces]], [[cgroups]], [[union filesystems]]
[[volume mounts]], [[bind mounts]]
[[docker-compose]]

