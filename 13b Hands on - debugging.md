# Docker Container - hands on - debugging
TIME: 15 min

## docker exec
* Use `man` to explore the `docker exec` argument
* Try to jump into the running `lighttpd` containers `shell`

### change container name to make this exercise working
If you do not provide the --name argument when starting a container, it will randomly create a name for you.
For a running container, docker will as well assign a random unique id, which is immutable.
```bash
[root@node ~]# docker ps
CONTAINER ID   IMAGE           COMMAND      CREATED          STATUS          PORTS                               NAMES
3e7503e5577e   sebp/lighttpd   "start.sh"   14 minutes ago   Up 13 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   nice_swanson
[root@node ~]# docker container rename 3e7503e5577e web
[root@node ~]# docker ps
CONTAINER ID   IMAGE           COMMAND      CREATED          STATUS          PORTS                               NAMES
3e7503e5577e   sebp/lighttpd   "start.sh"   14 minutes ago   Up 14 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   web
```


### Jump into running container

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTk2MTM5MzNdfQ==
-->