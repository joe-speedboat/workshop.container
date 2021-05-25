# Base Components
Now we can install Docker, but what can we do with and how does it work?

Let's look deeper into Docker and what components it's depending on.
We do this by the process, deploying a simple web application

## The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer:
```
dnf -y install vim tar wget

mkdir tmp
cd tmp
wget https://github.com/joe-speedboat/workshop.docker/raw/main/files/busybox.tar

tar vxf busybox.tar
	002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/
	002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/VERSION
	002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/json
	002dccb928dca75f75cdf7accaedcb7f86dadc3806a4145253df1c71e578c5e5/layer.tar
	d3cd072556c21c1f1940bd536675b97d7d419a2287d6bb3bd5044ea7466db788.json
	manifest.json
	repositories

tar vtfz *.layer.



## The Registry


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyMjY3ODM4MSwtMTQ5NjE5ODkzNiw2MT
k0NzA0MjJdfQ==
-->