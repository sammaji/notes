---
title: running docker containers
tags:
  - docker
  - containerization
draft: false
---
you can run `docker pull alpine` to pull the latest image of alpine linux.

to run the container, you need to use this command.
```
docker container run -it alpine:latest
```

`-i` -> interactive mode, with it host terminal commands will not be sent to the container
`-t` -> create a [[tty]] [see here](https://itsfoss.com/what-is-tty-in-linux/)

you can also pass a script while using the run command. the following will run the  given command in given container. in our case it prints out the date after every second.
```
docker container run -it --name looper alpine:latest sh -c "while true; do date; sleep 1; done;"
```

`--rm` -> passing this flag will delete a container when its exited.
- you can't run start to restart the container.
- pressing `ctrl+c` will delete the container.
- to detach from it, press `ctrl+p` then `ctrl+q` 
### exec
you can do the same thing using `docker container exec`.
```
docker container exec ID|NAME sh -c "while true; do date; sleep 1; done;"
```

- `exec` creates a new process inside your container.
- `docker exec -it ID|NAME sh` -> runs a shell inside your container.
### view logs
to view logs, you can use the following command.
```
docker logs -f ID|NAME
```

by default, docker will just send the recent logs and exit. if you want to continue receiving logs, use the follow flag (`-f`).

### pause / unpause
`docker pause ID|NAME` -> pause a container
`docker unpause ID|NAME` -> unpause a container
### attach
you can attach to a container, using `docker attach` or `docker continer attach`.

attaching links the `stdin` and `stdout` of the host terminal to the container. so if you send `sigint` (press `ctrl+c`), then the container will stop. to avoid that you can pass `--no-stdin` flag or pass `--sig-proxy false`.

```
docker attach --no-stdin ID|NAME # does not pass the stdin to container
docker attach --sig-proxy false ID|NAME # does not pass signals like stdint, stdkill, etc.
```
## related
![[contents]]
[[docker multi-platform builds]] -> https://docs.docker.com/build/building/multi-platform/
