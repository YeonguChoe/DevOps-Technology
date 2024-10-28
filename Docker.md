# Docker
- Main purpose of Docker is to run application the same way over all kinds of devices.
- Docker Desktop enables to run application built for different OS. (E.g, Application built for Linux running on Windows)

## Image
- Image is a template of application.
- Similar to `class` in OOP.

## Container
- Container is an instance from Image.
- Similary to `object` in OOP.

## [Dockerfile](https://docs.docker.com/reference/dockerfile/)
- Dockerfile is a text document specifying `command`s that user can call.

## [Docker Hub](https://hub.docker.com)
- Repository for Image.
- Similar to `GitHub`, but it is for Docker Image.

## Command
- List downloaded images

```bash
docker images
```

- List running docker container(s)

```bash
docker ps -a
```

- Download docker image

```bash
docker pull <image-name>[:<tag>]
```

- Remove docker resource

```bash
docker stop <container_id>
docker rm <container_id>
docker rmi <image_id>
```

- Instantiate docker image

```bash
docker run <image-name>[:<tag>]
```

- Instantiate docker image on the background

```bash
docker run --detach <image-name>[:<tag>]
```

- Stop docker container

```bash
docker stop <CONTAINER ID>
```

## Building Docker Image

1) Dockerfile

```Dockerfile
# FROM sets the base image of newly creating image
# Includes operating system at the tag (E.g, Alpine Linux)
FROM node:20-alpine


# COPY copies file or directory to image
# Syntax: COPY <file/directory name> <location in image>
COPY package.json /App/
COPY src /App/

# WORKDIR moves current location in CLI (Same as cd)
WORKDIR /App

# RUN execute any CLI command
RUN npm i

# CMD sets command to execute when the image is instantiated to container
CMD ["node","server.js"]
```

2) Build Docker image

```bash
docker build -tag <Image name:tag> <Dockerfile location>
```

  - Example
  
  ```bash
  docker build -t app:1.0 ./
  ```


## Port Binding
- Application runs on isolated container with its own network, having different port than local network.
- To link port between container port and local computer port, user need to bind the port.
To link a port from a Docker container to a port on your local computer, user need to bind the ports when you run the container.

```bash
docker run -p <Local Computer Port>:<Container Port>
```

  - Example
  
  ```bash
  docker run --detach --publish 3000:3000 app:1.0
  ```
