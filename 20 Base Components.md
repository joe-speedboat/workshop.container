# Base Components
Now we can install Docker, but what can we do with and how does it work?

Let's look deeper into Docker and what components it's depending on.
We do this by the process, deploying a simple web application

## The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer:
```bash
dnf -y install vim tar wget jq

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
Let's first have a short chat about the Docker image architecture.
So I borrowed few drawings from docker page where they explain the storage drivers:


So we import it and hopefully we have a container later on?
```bash
docker import busybox.tar
	sha256:98df473ae812df90a95ac180cda62653feff29e59c085884b45b6d37a10658c2
```
A imported image is still an image, but now we can see it got imported into the docker subsystem of the atomic host:
```bash
docker images
	REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
	<none>       <none>    98df473ae812   11 hours ago   1.46MB

docker inspect 98df473ae812 | jq -r '.[].RootFS'
	{
	  "Type": "layers",
	  "Layers": [
	    "sha256:a41c425c183934031a76f4a3eaaa4ac75ed99e9f10eeb0a937c075c294434ff8"
	  ]
	}
```
Oh great, now I just have to remember the ID in order to use my busybox docker image!   
Can Docker do that for me? YES, so lets do it.

## Image names and versions



## The Registry


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTczMTQyODY5LDE1NTIwNTUwNzcsMTQ4MT
g2NTM2Nyw5MTg2Mjk4ODYsLTE0OTYxOTg5MzYsNjE5NDcwNDIy
XX0=
-->