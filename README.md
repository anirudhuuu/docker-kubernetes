# Docker and Kubernetes

## Containers

![containers](./01-containers/docker%20containers.png)

### How?

![under the hood](./01-containers/under%20the%20hood%20docker.png)

### Why?

![why](./01-containers/why%20to%20use.png)

### Working

![working](./01-containers/docker%20working.png)

### Commands

![commands](./01-containers/docker%20commands.png)

## Essentials

### Images

![images](./02-essentials/docker%20images.png)

### Containers

![containers](./02-essentials/docker%20containers.png)

### Dockerfile

An overall view of working with containers is as follows:
![overall view](./02-essentials/overall%20view.png)

Plan of action will be as follows:

1. Create a fresh react app
2. Create a docker image
3. Spin up a container with that image
4. Perform updates in the application
5. Make a fresh image of the updated application
6. Sipn up a new container with the updated image

### Command to build an image

```bash
docker build -t react-docker .
```

![docker file logs](./02-essentials/docker%20file%20logs.png)

without caching it would look like following:

![docker file logs no cache](./02-essentials/docker%20file%20logs%20-%20no%20cache.png)

### Command to run the image

The format for porting is `<computer port>:<container port>`

```bash
docker run -p 5173:5173 react-docker
```

Since the vite application server needs the host to be defined we have set in the `vite.config.js` file the following:

```javascript
export default defineConfig({
  server: {
    host: "0.0.0.0",
    port: 5173,
  },
});
```

### Command to rebuild the image

after making changes to the application we need to rebuild the image for the changes to take effect.

For versioning we can use

```bash
docker build -t react-docker:2 .
```

To rebuild the exact same image we can use

```bash
docker build -t react-docker .
```

Optimised logs for the docker rebuild of image

![docker file logs rebuild](./02-essentials/docker%20file%20logs%20optimised%20for%20rebuild.png)

Output would be like following for the react app
![react output](./02-essentials/react%20output.png)

## Common Commands

Runs a container based on the image

```bash
docker run <image-name>
```

Runs a container based on the image in detached mode

```bash
docker run -d <image-name>
```

Provide a name to the container

```bash
docker run --name <container-name> <image-name>
```

Run on a specific port

```bash
docker run -p <host-port>:<container-port> <image-name>
```

Load present working directory into the container

```bash
docker run -v $(pwd):/app <image-name>
```

Execute in an interactive mode, this will allow you to run commands inside the container using `/bin/bash` or `sh` shell

```bash
docker run -it <image-name> /bin/bash
```

```bash
docker run -it <image-name> sh
```

## More Commands

List all the running containers

```bash
docker ps
```

List all the containers (including stopped ones)

```bash
docker ps -a
```

List logs of a container

```bash
docker logs <container-name>
```

Get attached to a running container, just to get inside the container

```bash
docker attach <container-name>
```

Stop a running container

```bash
docker stop <container-name>
```

Container is stuck or processing something, force stop it

```bash
docker kill <container-name>
```

Stop all the active running containers

```bash
docker stop $(docker ps -q)
```

Restart a container

```bash
docker restart <container-name>
```

Start a stopped container

```bash
docker start <container-name>
```

Remove a container

```bash
docker rm <container-name>
```

Container is busy, force remove it

```bash
docker rm -f <container-name>
```

Delete all the stopped containers

```bash
docker <container-name> prune
```

Copy a file from the container to the host

```bash
docker cp <container-name>:/path/to/file /path/on/host
```

## Dockerise an Express App

Build an image for an express app

```bash
docker build -t express-app .
```

![build output](./02-essentials/docker-express-app/build%20process.png)

Run a container with the image with environment variables passed in-line

```bash
docker run -p 4000:3000 -e PORT=3000 --rm express-app
```

![output of express app](./02-essentials/docker-express-app/output.png)

Run a container with the image with environment variables passed in a file

```bash
docker run -p 4000:3000 --env-file .env --rm express-app
```

## Multi-Stage Docker build

```bash
docker build -t express-mutli-stage .
```

![multi-stage build output](./02-essentials/docker-express-multi-stage/build%20output.png)

## Networking

Basic networking in docker allows containers to communicate with each other and the outside world.

```bash
docker run --rm -it busybox sh

hostname

ping google.com

ifconfig

exit
```

![basic](./03-networking/basic%20google%20ping.png)

`eth0` is the default network interface in docker containers. eth stands for Ethernet network interface. `veth` stands for virtual Ethernet network interface. `docker0` is the master interface for the docker bridge network that talks to the host machine.

![container networking](./03-networking/containers%20networking.png)

To list all the networks in docker, you can use the following command:

```bash
docker network ls
```

| NETWORK ID   | NAME   | DRIVER | SCOPE |
| ------------ | ------ | ------ | ----- |
| 287fceb8c8d1 | bridge | bridge | local |
| 30a4b9d415b7 | host   | host   | local |
| 66118539c033 | none   | null   | local |

Read more regarding network drivers in docker [here](https://docs.docker.com/engine/network/drivers/).

| NETWORK TYPE     | DESCRIPTION                                                                      |
| ---------------- | -------------------------------------------------------------------------------- |
| bridge (default) | containers on the same host can communicate, external access needs port mapping. |
| host             | The container shares the host's networking namespace (no isolation)              |
| none             | No network connectivity (completely isolated)                                    |
| overlay          | Enales multi-host networking for Swarm services                                  |
| macvlan          | Assigns a real MAC address to the container (acts like a physical device)        |

## Networking Commands

List all the networks

```bash
docker network ls
```

Inspect a network

```bash
docker network inspect <network-name>
```

Create a new network

```bash
docker network create <network-name>
```

Run a container in a specific network

```bash
docker run --network <network-name> <container-name>
```

Attach a running container to a network

```bash
docker network connect <network-name> <container-name>
```

Disconnect a container from a network

```bash
docker network disconnect <network-name> <container-name>
```

Remove a network

```bash
docker network rm <network-name>
```
