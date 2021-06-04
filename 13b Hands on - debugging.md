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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY0NDAzMTIyLC01NTUyOTUzMzYsLTE5MD
g4Mzg2OTJdfQ==
-->