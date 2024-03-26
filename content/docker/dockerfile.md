---
title: dockerfile
tags:
  - docker
  - dockerfile
draft: true
---
dockerfile is the recipe to build a docker image

```dockerfile
FROM <base-image-name>:<tag-name>
RUN <install deps.>
CMD <command executed on `docker container run`>
```

To create an image capable of running node.js, run this dockerfile.

```
FROM alpine:latest
RUN sudo apt install node
```
