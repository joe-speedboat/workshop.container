# Base Components
Now we can install Docker, but what can we do with and how does it work?

Let's look deeper into Docker and what components it's depending on.
We do this by the process, deploying a simple web application

## The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer:
```
dnf -y install vim tar
mkdir tmp
cd tmp
wget https://github.com/joe-speedboat/workshop.docker/raw/main/files/busybox.tar
tar vxf busybox.tar



## The Registry


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE5ODY3MjgzNjcsLTE0OTYxOTg5MzYsNj
E5NDcwNDIyXX0=
-->