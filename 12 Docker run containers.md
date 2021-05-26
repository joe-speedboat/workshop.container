# Docker: Run containers

## Explore the Docker client options
With Docker cli client you can do all the work on the lowest level, this brings you as close as possible to the container technology.
Lets explore what we can do with docker cli. For that we look at the shipped documentation first:
```bash
man -k docker
docker (1)           - Docker image and container command line interface
docker-attach (1)    - Attach local standard input, output, and error streams to a running container
...
docker-cp (1)        - Copy files/folders between a container and the local filesystem
docker-create (1)    - Create a new container
...
docker-exec (1)      - Run a command in a running container
...
docker-image (1)     - Manage images
...
docker-kill (1)      - Kill one or more running containers
...
docker-logs (1)      - Fetch the logs of a container
...
docker-port (1)      - List port mappings or a specific mapping for the container
docker-ps (1)        - List containers
docker-pull (1)      - Pull an image or a repository from a registry
docker-push (1)      - Push an image or a repository to a registry
...
docker-restart (1)   - Restart one or more containers
docker-rm (1)        - Remove one or more containers
docker-rmi (1)       - Remove one or more images
docker-run (1)       - Run a command in a new container
...
docker-search (1)    - Search the Docker Hub for images
...
docker-start (1)     - Start one or more stopped containers
...
docker-tag (1)       - Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
docker-top (1)       - Display the running processes of a container
...
docker-volume (1)    - Manage volumes
...
```

## Pull and start an image from Dockerhub
```bash
docker run --rm -it -p 80:80 yeasy/simple-web:latest
```
Now go and try to access the port 80 of your VM with a webbrowser!


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTQxMzIyOTU0OSwxNDEzMTEwNjk3LDg3OD
A3NDU3XX0=
-->