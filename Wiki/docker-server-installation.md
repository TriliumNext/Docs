# Docker Server Installation for Trilium

Trilium can be deployed using a Docker image, which is the recommended method for server installations. Official Docker images for **AMD64**, **ARMv6**, **ARMv7**, and **ARMv8/64** are available on [Docker Hub](https://hub.docker.com/r/zadam/trilium/). %%%{WARNING}%%% zadams dockerhub

## Prerequisites

Ensure Docker is installed on your system.

If you need help installing Docker, reference the [Docker Installation Docs](https://docs.docker.com/engine/install/)

**Note:** Trilium's Docker container requires root privileges to operate correctly.

## Pulling the Docker Image

To pull the Trilium image, use the following command, replacing `[VERSION]` with the desired version or tag, such as `0.90-latest` or just `latest`:

%%%{WARNING}%%% zadams container

```sh
docker pull zadam/trilium:[VERSION]
```

**Warning:** Avoid using the "latest" tag, as it may automatically upgrade your instance to a new minor version, potentially disrupting sync setups or causing other issues.

## Preparing the Data Directory

Trilium requires a directory on the host system to store its data. This directory must be mounted into the Docker container with write permissions.

## Running the Docker Container

### Local Access Only

Run the container to make it accessible only from the localhost. This setup is suitable for testing or when using a proxy server like Nginx or Apache.

%%%{WARNING}%%% zadams container

```sh
sudo docker run -t -i -p 127.0.0.1:8080:8080 -v ~/trilium-data:/home/node/trilium-data zadam/trilium:[VERSION]
```

1. Verify the container is running using `docker ps`.
2. Access Trilium via a web browser at `127.0.0.1:8080`.

### Local Network Access

To make the container accessible only on your local network, first create a new Docker network:

%%%{WARNING}%%% zadams container

```sh
docker network create -d macvlan -o parent=eth0 --subnet 192.168.2.0/24 --gateway 192.168.2.254 --ip-range 192.168.2.252/27 mynet
```

Then, run the container with the network settings:

%%%{WARNING}%%% zadams container

```sh
docker run --net=mynet -d -p 127.0.0.1:8080:8080 -v ~/trilium-data:/home/node/trilium-data zadam/trilium:0.52-latest
```

To set a different user ID (UID) and group ID (GID) for the saved data, use the `USER_UID` and `USER_GID` environment variables:

%%%{WARNING}%%% zadams container

```sh
docker run --net=mynet -d -p 127.0.0.1:8080:8080 -e "USER_UID=1001" -e "USER_GID=1001" -v ~/trilium-data:/home/node/trilium-data zadam/trilium:0.52-latest
```

Find the local IP address using `docker inspect [container_name]` and access the service from devices on the local network.

#### Reverse Proxy

1. [Nginx](nginx-proxy-setup.md)
2. [Apache](apache-proxy-setup.md)

### Global Access

To allow access from any IP address, run the container as follows:

%%%{WARNING}%%% zadams container

```sh
docker run -d -p 0.0.0.0:8080:8080 -v ~/trilium-data:/home/node/trilium-data zadam/trilium:[VERSION]
```

Stop the container with `docker stop <CONTAINER ID>`, where the container ID is obtained from `docker ps`.

### Custom Data Directory

For a custom data directory, use:

%%%{WARNING}%%% zadams container

```sh
-v ~/YourOwnDirectory:/home/node/trilium-data zadam/trilium:[VERSION]
```

The path before the colon is the host directory, and the path after the colon is the container's path. More details can be found in the [Docker Volumes Documentation](https://docs.docker.com/storage/volumes/).

### Note on --user Directive

The `--user` directive is unsupported. Instead, use the `USER_UID` and `USER_GID` environment variables to set the appropriate user and group IDs.
