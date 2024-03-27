---
title: bind mount
tags:
  - docker
  - mounts
  - bind-mounts
  - port
  - expose
draft: true
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

## related
![[contents]]