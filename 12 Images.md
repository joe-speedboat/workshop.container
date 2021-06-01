# The Images
A Docker image is a read-only template that contains a set of instructions for creating a container that can run on the Docker platform. It provides a convenient way to package up applications and preconfigured server environments, which you can use for your own private use or share publicly with other Docker users.

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/container-layers.jpg)
## Under the hood
```bash
mkdir tmp
cd tmp
wget https://github.com/joe-speedboat/workshop.docker/raw/main/files/busybox.tar

# let's look deeper into this container thing...
tar vtf busybox.tar
	drwxr-xr-x 0/0               0 2021-05-18 00:19 002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/
	-rw-r--r-- 0/0               3 2021-05-18 00:19 002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/VERSION
	-rw-r--r-- 0/0            1134 2021-05-18 00:19 002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/json
	-rw-r--r-- 0/0         1454592 2021-05-18 00:19 002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/layer.tar
	-rw-r--r-- 0/0            1457 2021-05-18 00:19 d3cd072556c21c1f1940bd536675b97d7d419a2287d6bb3bd5044ea7466db788.json
	-rw-r--r-- 0/0             203 1970-01-01 01:00 manifest.json
	-rw-r--r-- 0/0              90 1970-01-01 01:00 repositories
```

## Importing Images from tar file
This tar file looks interesting, but what can we do with it?

So we import it and hopefully we have a container later on?
```bash
cat busybox.tar | docker load
	d0d0905d7be4: Loading layer [=====================>]  1.455MB/1.455MB
	Loaded image: busybox:latest
```

A imported image is still an image, but now we can see it got imported into the docker subsystem of the atomic host:
```bash
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
	busybox      latest    d3cd072556c2   8 days ago   1.24MB

docker inspect busybox:latest | jq -r '.[].RootFS'
	{
	  "Type": "layers",
	  "Layers": [
	    "sha256:d0d0905d7be4eff6a63efe4a38647a679de1e024101f67db4fe4b5736c1e7f48"
	  ]
	}
```

## Customize an existing Docker Image
```bash
mkdir src/docker.toolbox
cd src/docker.toolbox
```
* <tt>vi Dockerfile</tt>

> FROM alpine:3.13 LABEL maintainer="Chris Ruettimann
> <chris@bitbull.ch>"
> 
> ###### This vars will be visible in running container ###### ARG MY_VERSION=0.01 ARG APK_FLAGS_COMMON="" ARG
> APK_FLAGS_PERSISTENT="${APK_FLAGS_COMMON} --clean-protected
> --no-cache" ARG APK_FLAGS_DEV="${APK_FLAGS_COMMON} --no-cache"
> 
> STOPSIGNAL SIGTERM
> 
> USER root WORKDIR /tmp
> 
> RUN apk add ${APK_FLAGS_DEV} bash bind-tools curl iftop openssl bc jq
> wget coreutils nmap-ncat nmap nmap-scripts 
> 
> ADD
> https://raw.githubusercontent.com/joe-speedboat/shell.scripts/master/nc_benchmark.sh
> /usr/bin/nc_benchmark.sh  RUN chmod 755 /usr/bin/nc_benchmark.sh

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjU1NDkyNDIsNzczMTM4MDA2LC05OT
E0MjMxOTgsMzk2Mjk1MDYsMTQwODcwNDExNywtNjA2ODcyNDIz
LC0xMDcwNzUwNDE5LDEzMjMwOTk5NjZdfQ==
-->