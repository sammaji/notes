---
title: bind mount
tags:
  - docker
  - mounts
  - bind-mounts
  - port
  - expose
draft: false
---
you can use bind mounts to mount a file or directory from the host machine into the container.

you can specify the bind mount while running a container like shown below. if your file path has spaces, use quotes.
```
docker run -v HOST-PATH:CONTAINER-PATH ... 
```

the `--mount` flag does the same thing.
```
# no space between src and target
docker run --mount src=HOST-PATH,target=CONTAINER-PATH
```

## ports and expose

opening a connection from a container to the outside, requires two things:
- exposing a port -> telling Docker that the container listens to a certain port.
- publishing a port -> map host ports to the container ports.

### expose
use  `EXPOSE PORT` in the dockerfile.

### publish
- map the host port to the container port -> `-p HOST-PORT:CONTAINER-PORT`
- you can also specify a protocol -> `EXPORT 4000/udp` and `-p 3000:4000/udp`
- if you ignore a host port, docker will assign any free port -> `-p 4000`

### security
while publishing a port by using `-p 3000:4000`, it will any host, anyone from the internet could come in and access what you're running.

one way to avoid this is by specifying which hosts are allowed access.
- e.g. `-p 127.0.0.1:3000:4000` -> this will only allow requests from host `127.0.0.1`, i.e., your computer only.

the short syntax, -p 3456:3000, will result in the same as -p 0.0.0.0:3000:4000, which truly is opening the port to everyone.

## related
![[contents]]