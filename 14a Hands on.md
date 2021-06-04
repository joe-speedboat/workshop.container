# Docker Container Storage - hands on

## Bind mount
### Cleanup your previous work before you continue
```bash
[root@node ~]# docker ps -a
	CONTAINER ID   IMAGE           COMMAND      CREATED         STATUS         PORTS                               NAMES
	9c8e05bbfe05   sebp/lighttpd   "start.sh"   4 seconds ago   Up 2 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   web
[root@node ~]# docker stop web
	dweb
[root@node ~]# docker rm web
	web
[root@node ~]# docker ps -a
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### Inject a web-app directory into container
```bash

[root@node ~]# docker run -d -it -p 80:80 --mount type=bind,source=$PWD/html5-todo-list-master,target=/var/www/localhost/htdocs --name web sebp/lighttpd 
	81f0d4cda66db47275570076615b392326c953257d9d4e3500a6a2da26fab5dc

[root@node ~]# docker inspect --format="{{json .Mounts }}" web | jq
	...
	    "Source": "/root/html5-todo-list-master",
	    "Destination": "/var/www/localhost/htdocs",
	    "Mode": "",
	    "RW": true,
	...
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcxOTgxNTQ0OCwyMDkwMTkxMzI4LDE3Nz
I4MDI0NTYsMTY4MTc4MTgwN119
-->