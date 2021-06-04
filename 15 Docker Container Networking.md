# Docker Container Networking
[docker networking overview article](https://www.nuagenetworks.net/blog/docker-networking-overview/)
By default docker networks are bridged with the node.
So you can imagine that containers can reach each other on a docker node.
Services are presented by forwarding ports, which can be done by the docker cli.

We have already used this in the labs we finished so far.

## Docker Port forwardings


## Docker Networks
You can create separate networks and connect docker containers to this specific netowkrs.
However, if you need more complex multihost setups, it is recomended to use a abstracted networking layer that deals with this networking isolation issues. Like kubernetes, swarm, ...
```bash
[root@node ~]# docker network ls
	NETWORK ID     NAME      DRIVER    SCOPE
	9b3a47779c4c   bridge    bridge    local
	9364c05292cf   host      host      local
	677311b96ac2   none      null      local
[root@node ~]# docker network inspect bridge
...
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
...

[root@node ~]#  docker network create -d bridge infra-net
	a49ef9027e872fd39587870e491626148ea25a309cbb04350318c073af18fd48

[root@node ~]# docker network inspect infra-net
...
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
...

[root@node ~]# docker run -it --name=net-test --net=infra-net busybox sh
	/ # ip a
	1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
	    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	    inet 127.0.0.1/8 scope host lo
	       valid_lft forever preferred_lft forever
	77: eth0@if78: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
	    link/ether 02:42:ac:12:00:02 brd ff:ff:ff:ff:ff:ff
	    inet 172.18.0.2/16 brd 172.18.255.255 scope global eth0
	       valid_lft forever preferred_lft forever
/ # exit
``` 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjAzNTM5ODM5NiwtMTUyMTk2NTE4NV19
-->