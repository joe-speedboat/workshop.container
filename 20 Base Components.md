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
Oh great, now I just have to remember the ID in order to use my busybox docker image!   
Can Docker do that for me? YES, so lets do it.

### Image names and versions
```bash
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
	<none>       <none>    98df473ae812   12 hours ago   1.46MB

docker tag 98df473ae812 busybox:latest

docker images
	REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
	busybox      latest    98df473ae812   12 hours ago   1.46MB
```
Okay, this looks better, it's time to start something.

## Running Images


## The Registry


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDk0NjMwMzQsLTIwNzMxMDcyMjUsLT
E0OTc2NTQwNjIsLTg1MDk5OTM5MiwtNTQ5NjAyOTMwLDE1NTIw
NTUwNzcsMTQ4MTg2NTM2Nyw5MTg2Mjk4ODYsLTE0OTYxOTg5Mz
YsNjE5NDcwNDIyXX0=
-->