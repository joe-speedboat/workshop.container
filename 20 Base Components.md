# Base Components
Now we can install Docker, but what can we do with and how does it work?

Let's look deeper into Docker and what components it's depending on.

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/container-layers.jpg)
## The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer:
```bash
dnf -y install vim tar wget jq git bash-completion

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

### Importing Images from tar file
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

### Image names and versions
```bash
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
	busybox      latest    d3cd072556c2   8 days ago   1.24MB

docker tag busybox:latest busybox:stable

docker images
	REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
	busybox      latest    d3cd072556c2   8 days ago   1.24MB
	busybox      stable    d3cd072556c2   8 days ago   1.24MB
```
As you can see, tags can be used to label image versions.

## Running Images
Okay, so lets start a first command inside the container
```bash
docker run --interactive --tty --rm busybox:latest ifconfig eth0
	eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
	          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
	          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
	          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
	          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
	          collisions:0 txqueuelen:0 
	          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)
```
If you compare the IP you got with the OS IP, you can see that they are different.
We will look later deeper into the shared and/other separated components of a container.

## The Registry
Now understand the mechanic of images and how to start a container.
But what about portability... security... sharing... of your images?

By default, docker uses the public registry, hosted by the makers of docker at:
https://hub.docker.com/
* TODO: Please create an account docker hub.
* 
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA2OTY4NTY4LC0xNzgyMjk5MSw2NTA4OT
c4NTIsMTU5MjI0MTI5OCwtMTM4MjQ2NTA2NSwtMjA3MzEwNzIy
NSwtMTQ5NzY1NDA2MiwtODUwOTk5MzkyLC01NDk2MDI5MzAsMT
U1MjA1NTA3NywxNDgxODY1MzY3LDkxODYyOTg4NiwtMTQ5NjE5
ODkzNiw2MTk0NzA0MjJdfQ==
-->