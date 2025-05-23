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

### Command to run the image

The format for porting is `<computer port>:<container port>`

```bash
docker run -p 5173:5173 react-docker
```
