---
title: docker-compose
tags:
  - docker
  - docker-compose
draft: false
---
docker compose is designed to simplify running multi-container applications using a single command.

```yaml
version: '3.8'

services:
	<service-name>:
		image: <image-name>
		build: <location-of-dockerfile>
		container-name: <name>
```

to build all the containers, you can run `docker compose build`.

you can use the service name to run a container.
```
docker compose run <service-name>
```

### bind mounts
you can specify volumes just like shown below. one thing to note, you can put relative urls here.

```yaml
version: '3.8'

services:
	<service-name>:
		image: <image-name>
		build: <location-of-dockerfile>
		volumes:
			<host-path>:<container-path>
```

### ports, environment variables

you can publish ports like this:

```yaml
# map ports
services:
	<service-name>:
		ports:
			<host-port>:<container-port>
```

you can define environment variables like this:

```yaml
services:
	<service-name>:
		environment:
			- VARIABLE=value
			- VARIABLE=value
```

[other ways to define env variables in docker] -> https://docs.docker.com/compose/environment-variables/set-environment-variables/

### related
![[contents]]