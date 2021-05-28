# The Images
As we have seen, Docker images may built from multiple layers, each of them depend on the layer below it.
So let's look deeper into a minimal docker image consisting of one single layer.

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


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTMyMzA5OTk2Nl19
-->