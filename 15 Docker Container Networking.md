# Docker Container Networking
[docker networking overview article](https://www.nuagenetworks.net/blog/docker-networking-overview/)
By default docker networks are bridged with the node.
So you can imagine that containers can reach each other on a docker node.
Services are presented by forwarding ports, which can be done by the docker cli.

We have already used this in the labs we finished so far.

You can create separate networks and connect docker containers to this specific netowkrs.
However, if you need more complex multihost setups, it is recomended to use a abstracted n
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NzE3Njc5MTAsLTE1MjE5NjUxODVdfQ
==
-->