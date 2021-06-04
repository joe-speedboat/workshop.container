# Docker Container Networking
[docker networking overview article](https://www.nuagenetworks.net/blog/docker-networking-overview/)
By default docker networks are bridged with the node.
So you can imagine that containers can reach each other on a docker node.
Services are presented by forwarding ports, which can be done by the docker cli.

We have already used this in the labs we finished so far.

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
[
    {
        "Name": "infra-net",
        "Id": "a49ef9027e872fd39587870e491626148ea25a309cbb04350318c073af18fd48",
        "Created": "2021-06-04T12:25:07.83783701Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
[root@node ~]# docker run -it --name=infra-net busybox sh
Unable to find image 'busybox:latest' locally
latest: Pulling from library/busybox
92f8b3f0730f: Pull complete 
Digest: sha256:b5fc1d7b2e4ea86a06b0cf88de915a2c43a99a00b6b3c0af731e5f4c07ae8eff
Status: Downloaded newer image for busybox:latest
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
75: eth0@if76: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
    link/ether 02:42:ac:11:00:02 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.2/16 brd 172.17.255.255 scope global eth0
       valid_lft forever preferred_lft forever
/ # exit
[root@node ~]# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                      PORTS     NAMES
316ea90f0349   busybox   "sh"      33 seconds ago   Exited (0) 14 seconds ago             infra-net
[root@node ~]# docker rm 316ea90f0349
316ea90f0349
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
/ # 

<!--stackedit_data:
eyJoaXN0b3J5IjpbODkyNjkyMjc0LC0xNTIxOTY1MTg1XX0=
-->