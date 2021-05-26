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
docker run -it -p 80:80 yeasy/simple-web:latest
```
Now go and try to access the port 80 of your VM with a webbrowser!
You should see something like that:
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/http_simple_web.png)
Since you started the container in interactive mode, it will exit if you type CTRL-C, please do so now.

Now let us inspect the current status of docker and clean up.
```bash
docker ps 
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker ps -a
	CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS                     PORTS     NAMES
	f4a758984ac0   yeasy/simple-web:latest   "/bin/sh -c 'python …"   3 minutes ago   Exited (0) 3 minutes ago             dreamy_diffie

docker rm f4a758984ac0
	f4a758984ac0
docker images
	REPOSITORY         TAG       IMAGE ID       CREATED       SIZE
	yeasy/simple-web   latest    172c78152bf6   3 years ago   679MB

docker rmi yeasy/simple-web
	Untagged: yeasy/simple-web:latest
	Untagged: yeasy/simple-web@sha256:356de309052fe233ba08eb4c9ad85ab89398f31555e8777326d57307ac913727
	Deleted: sha256:172c78152bf688785a3886063f586af38dbb18c59587f0a90bd57490ef06c251
	...
	Deleted: sha256:8fad67424c4e7098f255513e160caa00852bcff347bc9f920a82ddf3f60229de
docker images
	REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

As with real operating systems services, we can decide if containers should restart, run in background, and so on.
So we do now

## 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTIzODA5NDEsMTQxMzIyOTU0OSwxND
EzMTEwNjk3LDg3ODA3NDU3XX0=
-->