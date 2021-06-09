# Docker Container Networking
[docker networking overview article](https://www.nuagenetworks.net/blog/docker-networking-overview/)
By default docker networks are bridged with the node.
So you can imagine that containers can reach each other on a docker node.
Services are presented by forwarding ports, which can be done by the docker cli.

We have already used this in the labs we finished so far.

# Binding Ports

Docker containers can connect to the outside world without further configuration, but the outside world cannot connect to Docker containers by default.

## How this works

A bridge network is created (with the name `bridge`) when you install Docker. Every outgoing connection appears to originate from the host’s IP space; Docker creates a custom `iptables` [masquerading rule](http://www.tldp.org/HOWTO/html_single/Masquerading-Simple-HOWTO/).

## Forward everything

If you append `-P` (or `--publish-all=true`) to `docker run`, Docker identifies every port the Dockerfile exposes (you can see which ones by looking at the `EXPOSE` lines). Docker also finds ports you expose with `--expose 8080` (assuming you want to expose port 8080). Docker maps all of these ports to a host port within a given `epehmeral port range`. You can find the configuration for these ports (usually 32768 to 61000) in `/proc/sys/net/ipv4/ip_local_port_range`.

### Where each ports go

Use the `docker port` command to inspect the mapping Docker creates.

## Forward selectively

You can also specify ports. When doing so, you don’t need to use ports from the `ephemeral port range`. Suppose you want to expose the container’s port 8080 (standard http port) on the host’s port 80 (assuming that port is not in use). Append `-p 80:8080` (or `--publish=80:8080`) to your `docker run` command. For example:

```
docker run -p 80:8080 nginx

## OR ##

docker run --publish=80:8080 nginx

```

### Custom IP _and_ port forwarding

By default, Docker exposes container ports to the IP address `0.0.0.0` (this matches any IP on the system). If you prefer, you can tell Docker _which_ IP to bind on. To bind on IP address `10.0.0.3`, host port `80`, and container port `8080`:

```
docker run -p 10.0.0.3:80:8080 nginx

```

## Docker Networks
You can create separate networks and connect docker containers to this specific netowkrs.
However, if you need more complex multihost setups, it is recomended to use a abstracted networking layer that deals with this networking isolation issues. Like kubernetes, swarm, ...
```bash
docker network ls
	NETWORK ID     NAME      DRIVER    SCOPE
	9b3a47779c4c   bridge    bridge    local
	9364c05292cf   host      host      local
	677311b96ac2   none      null      local
docker network inspect bridge
	...
            "Config": [
                {
                    "Subnet": "172.17.0.0/16",
                    "Gateway": "172.17.0.1"
	...

docker network create -d bridge infra-net
	a49ef9027e872fd395878...04350318c073af18fd48

docker network inspect infra-net
	...
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
	...

docker run -it --name=net-test --net=infra-net busybox sh
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
eyJoaXN0b3J5IjpbLTExNjI0OTUyNTJdfQ==
-->