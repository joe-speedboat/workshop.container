# Docker Container Storage - hands on

## Bind mount
* Cleanup your previous work before you continue
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA5MDE5MTMyOCwxNzcyODAyNDU2LDE2OD
E3ODE4MDddfQ==
-->