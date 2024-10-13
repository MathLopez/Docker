# Docker cheat sheet

- [Docker cheat sheet](#docker-cheat-sheet)
    * [Dockerfile](#dockerfile)
        + [Parameters](#parameters)
    * [Build the Docker image](#build-the-docker-image)
    * [Docker compose](#docker-compose)
- [Github registry](#github-registry)
    * [Tag the image](#tag-the-image)
    * [Delete local image](#delete-local-image)
    * [Publish the image on GitHub Container Registry](#publish-the-image-on-github-container-registry)
    * [Pull the image from GitHub Container Registry](#pull-the-image-from-github-container-registry)
- [Delete](#delete)
    * [Cleanup](#cleanup)
    * [Free some space](#free-some-space)

## Dockerfile

### Parameters

### `FROM`

The `FROM` instruction specifies the base image to use for the build. In this
example, we use the `ubuntu:24.04` image. It means that the Docker image will be
based on the Ubuntu 24.04 image and have all the tools and libraries provided by
this image, such as `bash` as the default shell and `apt` to install new
packages.

### `WORKDIR`

The `WORKDIR` instruction sets the working directory for the rest of the
Dockerfile instructions.

It is equivalent to running `mkdir -p /path/to/workdir && cd /path/to/workdir`.

The default is often `/app`.

### `CMD`

The `CMD` instruction specifies the default command to run when the container
starts. It can be overridden by passing a command to the `docker run` command.

### `ENTRYPOINT`

The `ENTRYPOINT` and `CMD` instructions are often confusing because they both
define what command to run when the container starts.

The main difference is that `ENTRYPOINT` is not overridden by passing a command
to the `docker run` command, a manual override is needed.

The `CMD` instruction is then passed as arguments to the `ENTRYPOINT`
instruction.

### `RUN`

The `RUN` instruction executes a command in a new layer on top of the current
image and commits the results. It is used to install new packages, update the
system, or run any command that modifies the image.

### `COPY`

The `COPY` instruction copies files or directories from the host to the image.
These files will be stored in the image and can be used by the container at
runtime.

## Build the Docker image

```sh
# Build and tag an image
docker build -t <image-name> <build-context>

# Start a container using its image name
docker run <image-name>

# Start a container in background
docker run -d <image-name>

# Display all running containers
docker ps

# Stop a container
docker stop <container-id>

# Access a running container
docker exec -it <container-id> /bin/sh

# Start a container and override the entry point
docker run --entrypoint /bin/sh <image-name>

# Start a container and override the command
docker run <image-name> <command>

# Delete all stopped containers
docker container prune

# Delete all images
docker image prune
```

## Docker compose
```sh
# Start all services defined in the docker-compose.yml file
docker compose up

# Start all services defined in the docker-compose.yml file in background
docker compose up -d

# Display all running services
docker compose ps

# Stop all services defined in the docker-compose.yml file
docker compose down

# Check the logs of a service
docker compose logs <service-name>

# Check the logs of all services defined in the docker-compose.yml file
docker compose logs

# Follow the logs of a service
docker compose logs -f <service-name>
```

# Github registry

## Tag the image
Tag the image correctly for GitHub Container Registry
The image must be tagged with the following format: `ghcr.io/<username>/<image>:<tag>`.

Run the following command to tag the image with the correct format, replacing <username> with your GitHub username:
```sh
 # Tag the image with the correct format
docker tag <image_name> ghcr.io/<username>/<image_name>:latest
```

## Delete local image
You can delete the local image with the following command:

```sh
# Delete java-ios-docker image
docker rmi <image_name>
```

## Publish the image on GitHub Container Registry
Now publish the image on GitHub Container Registry with the following command, replacing <username> with your GitHub username:

```sh
# Publish the image on GitHub Container Registry
docker push ghcr.io/<username>/<image_name>
```

## Pull the image from GitHub Container Registry
Run the following command to pull the image from GitHub Container Registry, replacing <username> with your GitHub username:

```sh
# Pull the image from GitHub Container Registry
docker pull ghcr.io/<username>/java-ios-docker
```

# Delete

## Cleanup

To remove the Docker image, run the following command:

```sh
# Remove the Docker image
docker rmi basic-dockerfile
```

## Free some space
Docker images, containers and volumes can take a lot of space on your computer.

You can use the following commands to free some space:

```sh
# Delete all stopped containers, all networks not used by at least one container, all anonymous volumes not used by at least one container, all images without at least one container associated to them and all build cache
docker system prune --all --volumes
```