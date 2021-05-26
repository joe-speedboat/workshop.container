# Base Components
Now we can install Docker, but what can we do with and how does it work?

Let's look deeper into Docker and what components it's depending on.
We do this by the process, deploying a simple web application

## The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer:
```bash
dnf -y install vim tar wget

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


## The Container
This tar file looks interesting, but what can we do with it?

So we import it and hopefully we have a container later on?
```bash
docker import busybox.tar
	sha256:98df473ae812df90a95ac180cda62653feff29e59c085884b45b6d37a10658c2
```
A imported image is still an image, but now we can see it got imported into the docker subsystem of the atomic host:
```bash

```


## The Registry


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5NzU4MzE3Niw5MTg2Mjk4ODYsLTE0OT
YxOTg5MzYsNjE5NDcwNDIyXX0=
-->