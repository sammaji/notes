---
title: dockerfile
tags:
  - docker
  - dockerfile
draft: false
---
dockerfile is the recipe to build a docker image
- `FROM` -> specify name of base image
- `WORKDIR <path>` -> change workdir, all following instructions will be executed in the given location.
- `COPY <source> <dest>` -> copy files from host to container.
- `RUN command` -> run commands
- `CMD [...]` -> command to run when the container is started.

Here is an example dockerfile to run a shell script.

```dockerfile
FROM alpine:latest
WORKDIR /usr/src/app
COPY ./hello.sh .
RUN chmod +x ./hello.sh
CMD ./hello.sh
```

To build the image, we use the following command.
```
docker build LOCATION-OF-DOCKERFILE -t CONTAINER-NAME
```

### CMD vs ENTRYPOINT
Both `CMD` and `ENTRYPOINT` take a command, that is run when the container starts. But if  we pass a command while running a container, it will replace the `CMD` command.

```dockerfile
CMD ["echo"]
---
docker run -it NAME ps -a  # this will replace the CMD command
```

But if you use `ENTRYPOINT`, the command passed while running a container will instead become the arguments of the entrypoint.
```
ENTRYPOINT ["echo"]
---
# "hello" becomes arguments of the entrypoint command
# effectively running echo "hello"
docker run -it NAME "hello" 
```

If you pass both `CMD` and `ENTRYPOINT`, `CMD` will become the default arguments of the `ENTRYPOINT`.

```dockerfile
CMD ["hello"]
ENTRYPOINT ["echo"]
---
docker run -it NAME # output: "hello"
docker run -it NAME "hi" # output: "hi"
```

## related
![[contents]]