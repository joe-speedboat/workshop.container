
## The Registry (Image store)
A Docker registry is a storage and distribution system for named Docker images. The same image might have multiple different versions, identified by their tags.

A Docker registry is organized into Docker repositories , where a repository holds all the versions of a specific image. The registry allows Docker users to pull images locally, as well as push new images to the registry (given adequate access permissions when applicable).

By default, the Docker engine interacts with DockerHub , Docker’s public registry instance. However, it is possible to run on-premise the open-source Docker registry/distribution, as well as a commercially supported version called Docker Trusted Registry . There are other public registries available online.

### Search the Registry
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
### Pulling images
By default docker client is pulling from dockerhub registry.
If you do not define the full url of an image, docker client tries to auto-complete the url with docker.io.
```bash
docker pull busybox:latest
latest: Pulling from library/busybox
92f8b3f0730f: Pull complete 
Digest: sha256:b5fc1d7b2e4ea86a06b0cf88de915a2c43a99a00b6b3c0af731e5f4c07ae8eff
Status: Downloaded newer image for busybox:latest
docker.io/library/busybox:latest
[root@atomic ~]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
busybox      latest    d3cd072556c2   10 days ago   1.24MB
```
But you can download from other container registries as well if you define the full url of an image





### Registry Namespace (tagging)
```bash
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
	busybox      latest    d3cd072556c2   8 days ago   1.24MB

docker images tag busybox:latest busybox:stable

docker images
	REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
	busybox      latest    d3cd072556c2   8 days ago   1.24MB
	busybox      stable    d3cd072556c2   8 days ago   1.24MB
```
As you can see, tags can be used to label image versions.

### Authenticate to Registry Service


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0OTY5MzEyMCwxNTI1NDk2NDUyXX0=
-->