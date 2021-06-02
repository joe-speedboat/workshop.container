# Docker Images
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
### Prepare your Docker Project
```bash
mkdir src/docker.toolbox
cd src/docker.toolbox
```
### Create the container building information
<tt>vi Dockerfile</tt>
```
FROM alpine:3.13
LABEL maintainer="Chris Ruettimann <chris@bitbull.ch>"

###### This vars will be visible in running container ######
ARG MY_VERSION=0.01
ARG APK_FLAGS_COMMON=""
ARG APK_FLAGS_PERSISTENT="${APK_FLAGS_COMMON} --clean-protected --no-cache"
ARG APK_FLAGS_DEV="${APK_FLAGS_COMMON} --no-cache"

STOPSIGNAL SIGTERM

USER root
WORKDIR /tmp

RUN apk add ${APK_FLAGS_DEV} bash bind-tools curl iftop openssl bc jq wget coreutils nmap-ncat nmap nmap-scripts 

ADD https://raw.githubusercontent.com/joe-speedboat/shell.scripts/master/nc_benchmark.sh /usr/bin/nc_benchmark.sh 
RUN chmod 755 /usr/bin/nc_benchmark.sh
```
### Build it
```bash
docker build --network=host -t mytoolbox:0.01 .
Sending build context to Docker daemon   2.56kB
Step 1/12 : FROM alpine:3.13
 ---> 6dbb9cc54074
...
Removing intermediate container 7dcc1bf8ab68
 ---> a2424c9c517b
Successfully built a2424c9c517b
Successfully tagged mytoolbox:0.01
```
### Test it
```bash
[root@node toolbox]# hostname -i
192.168.116.102

[root@node toolbox]# docker run -it mytoolbox:0.01 bash
**bash-5.1# /usr/bin/nmap -T5 -P0 -sS 127.0.0.1**
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-01 17:33 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.0000010s latency).
All 1000 scanned ports on localhost (127.0.0.1) are closed
Nmap done: 1 IP address (1 host up) scanned in 0.08 seconds

bash-5.1# /usr/bin/nmap -T5 -P0 -sS 192.168.116.102**
Host discovery disabled (-Pn). All addresses will be marked 'up' and scan times will be slower.
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-01 17:33 UTC
Nmap scan report for 192.168.116.102
Host is up (0.000048s latency).
Not shown: 996 filtered ports
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   closed http
443/tcp  closed https
9090/tcp closed zeus-admin
Nmap done: 1 IP address (1 host up) scanned in 16.30 seconds

bash-5.1# hostname
05bc3bff027b

bash-5.1# exit

[root@stream toolbox]# docker ps -a
CONTAINER ID   IMAGE            COMMAND                  CREATED              STATUS                       PORTS     NAMES
05bc3bff027b   mytoolbox:0.01   "bash"                   About a minute ago   Exited (0) 5 seconds ago               dreamy_davinci
```
### Tag the image
We might find this image useful, and want to mark it as a working release.
```bash
[root@node toolbox]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
mytoolbox    0.01      a2424c9c517b   14 minutes ago   53.5MB
alpine       3.13      6dbb9cc54074   6 weeks ago      5.61MB
alpine       latest    6dbb9cc54074   6 weeks ago      5.61MB

[root@node toolbox]# docker tag mytoolbox:0.01 mytoolbox:stable

[root@node toolbox]# docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
mytoolbox    0.01      a2424c9c517b   15 minutes ago   53.5MB
mytoolbox    stable    a2424c9c517b   15 minutes ago   53.5MB
alpine       3.13      6dbb9cc54074   6 weeks ago      5.61MB
alpine       latest    6dbb9cc54074   6 weeks ago      5.61MB
```

### And now lets make this image public available
* My Dockerhub namespace is <tt>christian773</tt>, please replace this with your namespace name.
```bash
[root@node toolbox]# docker tag mytoolbox:stable docker.io/christian773/mytoolbox:stable

[root@node toolbox]# docker login
Authenticating with existing credentials...
WARNING! Your password will be stored unencrypted in /root/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store
Login Succeeded

[root@node toolbox]# docker push docker.io/christian773/mytoolbox:stable
The push refers to repository [docker.io/christian773/mytoolbox]
25f46b9aaadb: Pushed 
2be52c6a6a9f: Pushed 
08ba6168a320: Pushed 
b2d5eeeaba3a: Mounted from library/alpine 
stable: digest: sha256:e177e2ceb9c980086536a5a09e93b6685f1c9ca7761cb579e747979c6c059513 size: 1156
```
### let us now check if the image is available
After about 5 minutes you should be able to see the new image in your dockerhub profile:
https://hub.docker.com/u/christian773

Of course you can search is as well with the docker cli client, but it may take few minutes more until the image get visible.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwODg2NzAxMTJdfQ==
-->