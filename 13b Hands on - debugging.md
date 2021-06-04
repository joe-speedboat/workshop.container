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


### Jump into running container and do some work
```bash
docker exec -it web sh
/ # ps -ef
PID   USER     TIME  COMMAND
    1 lighttpd  0:00 lighttpd -D -f /etc/lighttpd/lighttpd.conf
  113 root      0:00 sh
  120 root      0:00 ps -ef
/ # echo go away > /var/www/localhost/htdocs/index.html
/ # cat /var/www/localhost/htdocs/index.html
go away
/ # exit
```

* Now try to access the web service on the node again, do you see the change?

* Do you understand what happened?

* If you start a new container instance.
	* Will you see the "go away" page?
	* Why?

### one shot execution
Sometimes you have to execute a single command in a running container, eg: DB shema deploy, ...
You can do this as well with the `exec` option
```bash
docker exec web sh -c "/bin/echo this is for sure not persitent > /var/www/localhost/htdocs/index.html"
```

* Now try to access the web service on the node again, do you see the change?

* Do you understand what happened?

## Understand container states
A running container acts somehow like a running operating system. But how looks a stopped container like?
Let us get an idea by doing an exercise:

```bash
[root@node ~]# docker ps
CONTAINER ID   IMAGE           COMMAND      CREATED          STATUS          PORTS                               NAMES
3e7503e5577e   sebp/lighttpd   "start.sh"   34 minutes ago   Up 34 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   web

[root@node ~]# docker stop web
web

[root@node ~]# docker ps -a
CONTAINER ID   IMAGE           COMMAND      CREATED          STATUS                      PORTS     NAMES
3e7503e5577e   sebp/lighttpd   "start.sh"   34 minutes ago   Exited (1) 25 seconds ago             web
```
Okay, we can see now that the container is not in running state any more.
Let's take a closer look.

## Copy content from/to container filesystem
```bash
[root@node ~]# docker cp web:/var/www/localhost/htdocs/index.html .
[root@node ~]# cat index.html 
this is for sure not persitent
```
## Get the Logs of a container
```bash
[root@node ~]# docker logs web
2021-06-04 09:35:54: (server.c.1513) server started (lighttpd/1.4.57)
2021-06-04 09:36:06: (server.c.1975) server stopped by UID = 0 PID = 0
```
You can add the `-f` option which is following the live logs, finish that view with CTRL-C

## Do you understand?
```bash
[root@node ~]# docker rm web
web
[root@node ~]# docker cp web:/var/www/localhost/htdocs/index.html .
Error: No such container:path: web:/var/www/localhost/htdocs/index.html
```
The overlay-fs and the logs stay if the container is in stopped mode.
Be aware that if you use the `--rm` option when starting a container, everything about the container get removed immediately.

# Fun exercise

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0OTUzNzM2NTUsLTU1NTI5NTMzNiwtMT
kwODgzODY5Ml19
-->