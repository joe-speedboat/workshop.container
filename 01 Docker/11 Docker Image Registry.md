
# Docker Image Registry
A Docker registry is a storage and distribution system for Docker images. The same image might exist in multiple different versions, identified by their tags.

A Docker registry is organized into Docker repositories , where a repository holds all the versions of a specific image. The registry allows Docker users to pull images locally, as well as push new images to the registry (given adequate access permissions when applicable).

By default, the Docker engine interacts with DockerHub , Docker’s public registry instance. However, it is possible to run on-premise the open-source Docker registry/distribution, as well as a commercially supported version called Docker Trusted Registry . There are other public registries available online.

## Search the Registry for repositories
```bash
docker search busybox
	NAME                      DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
	busybox                   Busybox base image.                             2231      [OK]       
	progrium/busybox                                                          70                   [OK]
	radial/busyboxplus        Full-chain, Internet enabled, busybox made f…   39                   [OK]
	yauritux/busybox-curl     Busybox with CURL                               15                   
	...                  
	emccorp/busybox           Busybox                                         0                    
	ggtools/busybox-ubuntu    Busybox ubuntu version with extra goodies       0                    [OK]
```

```bash
docker search --filter is-official=true --filter stars=3 busybox
	NAME      DESCRIPTION           STARS     OFFICIAL   AUTOMATED
	busybox   Busybox base image.   2231      [OK]     
```
## Pulling images
If you do not define the full url of an image, docker client tries to auto-complete the url with docker.io.
```bash
docker pull busybox:latest
	latest: Pulling from library/busybox
	92f8b3f0730f: Pull complete 
	Digest: sha256:b5fc1d7b2e4ea86a06b0cf88de915a2c43a99a00b6b3c0af731e5f4c07ae8eff
	Status: Downloaded newer image for busybox:latest
	docker.io/library/busybox:latest
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
	busybox      latest    d3cd072556c2   10 days ago   1.24MB
```
But you can download from other container registries as well if you define the full url of an image:
```bash
docker pull quay.io/ooteniya/todo-spring:v5.0.0
	v5.0.0: Pulling from ooteniya/todo-spring
	b10f359f0883: Pull complete 
	c78b8fddfa3d: Pull complete 
	6e99518c4711: Pull complete 
	e2b398a93b60: Pull complete 
	Digest: sha256:05d9af6eef604093506982424414331d2b9225476ddabc4c5f33ab44f208ec9f
	Status: Downloaded newer image for quay.io/ooteniya/todo-spring:v5.0.0
	quay.io/ooteniya/todo-spring:v5.0.0

docker images
	REPOSITORY                     TAG       IMAGE ID       CREATED       SIZE
	busybox                        latest    d3cd072556c2   10 days ago   1.24MB
	quay.io/ooteniya/todo-spring   v5.0.0    63e36498f889   3 weeks ago   679MB
```

## Registry Namespace (tagging)
Tags are used to identify the location and version of an image.
Let's explore it by an example with the image we downloaded from quay.io before:
```bash
docker pull quay.io/ooteniya/todo-spring:v5.0.0
	v5.0.0: Pulling from ooteniya/todo-spring
	...
	
docker tag quay.io/ooteniya/todo-spring:v5.0.0 docker.io/christian773/todo-spring:v5.0.0

docker tag quay.io/ooteniya/todo-spring:v5.0.0 docker.io/christian773/todo-spring:stable

docker images
	REPOSITORY                     TAG       IMAGE ID       CREATED       SIZE
	busybox                        latest    d3cd072556c2   10 days ago   1.24MB
	quay.io/ooteniya/todo-spring   v5.0.0    63e36498f889   3 weeks ago   679MB
	christian773/todo-spring       stable    63e36498f889   3 weeks ago   679MB
	christian773/todo-spring       v5.0.0    63e36498f889   3 weeks ago   679MB
```
As you can see, tags can be used to label image versions.

## Authenticate against Registry Service
You need to authenticate against a registry if you want to pull images that are not public.

### Authenticate with docker client
This will make your private images accessible and avoid hitting anonymous pull limitations
```bash
docker login -u christian773 docker.io
	Password: 
	WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
	Configure a credential helper to remove this warning. See
	https://docs.docker.com/engine/reference/commandline/login/#credentials-store
	Login Succeeded
```

### Pushing an Docker image
Let us push a docker image into the private docker registry.
```bash
docker push docker.io/christian773/todo-spring:stable
The push refers to repository [docker.io/christian773/todo-spring]
d2ce0d2f1200: Pushed 
fa1dacd1e720: Pushed 
144a43b910e8: Pushed 
4a2bc86056a8: Pushed 
stable: digest: sha256:e0fb5fdbf3e8c585ec4a9f33c71e3b94956948acafbbd25e8025058257a84584 size: 1162
```

## Dockerhub limitations
Dockerhub public image registry used to be free for any usage.
But since they reached it's capacity limits, you have to authenticate for bypassing the public limits.

### Anonymous dockerhub limitations
```bash
TOKEN=$(curl "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)
curl --head -H "Authorization: Bearer $TOKEN" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest
	...
	date: Tue, 01 Jun 2021 05:55:56 GMT
	strict-transport-security: max-age=31536000
	ratelimit-limit: 100;w=21600
	ratelimit-remaining: 99;w=21600
```

### Authenticate and verify limits again
```bash
TOKEN=$(curl --user 'username:password' "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)
curl --head -H "Authorization: Bearer $TOKEN" https://registry-1.docker.io/v2/ratelimitpreview
	...
	date: Tue, 01 Jun 2021 06:06:39 GMT
	strict-transport-security: max-age=31536000
	ratelimit-limit: 200;w=21600
	ratelimit-remaining: 200;w=21600
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1NjgzMDIwODEsLTc5MDU5NDAwMywxOD
IwMDQ1NzA2LDE2MTg3MjIwOTcsODkwMTYwMTA0LC02NTM4MDYz
NzddfQ==
-->