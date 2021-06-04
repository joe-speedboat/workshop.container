# Docker Container Networking
[docker networking overview article](https://www.nuagenetworks.net/blog/docker-networking-overview/)
By default docker networks are bridged with the node.
So you can imagine that containers can reach each other on a docker node.
Services are presented by forwarding ports, which can be done by the docker cli.

We have already used this in the labs we finished so far.

Let's look us into an real world docker deployment with separated networks to get an overview about what would be useful.

## Create backend network

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MjE5NjUxODVdfQ==
-->