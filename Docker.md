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

- Download docker image

```bash
docker pull <image-name>[:<tag>]
```

- Remove docker resource

```bash
docker rm <container_id>
docker rmi <image_id>
```

- Instantiate docker image

```bash
docker run <image-name>[:<tag>]
```

- Instantiate docker image on the background

```bash
docker run -d <image-name>[:<tag>]
```

- List running docker container(s)

```bash
docker ps
```

- Stop docker container

```bash
docker stop <CONTAINER ID>
```
