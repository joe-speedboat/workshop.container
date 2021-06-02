# Docker Containers
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
Container images become containers at runtime and in the case of Docker containers - images become containers when they run on Docker Engine. Available for both Linux and Windows-based applications, containerized software will always run the same, regardless of the infrastructure. Containers isolate software from its environment and ensure that it works uniformly despite differences for instance between development and staging.

## Running Containers interactively
So let us first start a first command inside the container
```bash
docker container run --interactive --tty --rm busybox:latest ifconfig eth0
	eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
	          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
	          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
	          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
	          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
	          collisions:0 txqueuelen:0 
	          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)
```
If you compare the IP you got with the operating system IP, you can see that they are different.
We will look later deeper into the shared and/other separated components of a container.

## Container start
Did you notice that the container immediately returned to the  operating system after executing the desired command?
A container image may suggest the process that get started after container is going up, but we can always override this settings.
So let us take a look of some of this options to get a better understanding:


### docker container run
This means we start a new container out of an image.

### --interactive --tty
This means that the container does avoid to run in background. The tty reason which allocates a terminal makes sense if you use the interactive option. You can see this options often in short form: <tt>-it</tt>

### --rm
This means that the container should be removed once it has entered the exit state.
But what is the meaning and value of this option?
So let us try that by an example and discuss later on the results:

```bash
[root@node]# docker container run --interactive --tty --rm busybox:latest ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)

[root@node]# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES


[root@stream toolbox]# docker container run --interactive --tty busybox:latest ifconfig eth0
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)

[root@node]# docker ps -a
CONTAINER ID   IMAGE            COMMAND           CREATED         STATUS                     PORTS     NAMES
12b32a047897   busybox:latest   "ifconfig eth0"   7 seconds ago   Exited (0) 6 seconds ago             zealous_matsumoto

[root@node]# docker logs 12b32a047897
eth0      Link encap:Ethernet  HWaddr 02:42:AC:11:00:02  
          inet addr:172.17.0.2  Bcast:172.17.255.255  Mask:255.255.0.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:2 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:0 
          RX bytes:180 (180.0 B)  TX bytes:0 (0.0 B)

[root@stream toolbox]# docker rm 12b32a047897
12b32a047897

[root@stream toolbox]# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

## Run container like a service in background?
The most of us will probably want to start the containers like a service.
For this we have several options as well. Let us look at a common one:
```bash
docker run -d --restart unless-stopped -p 80:80 yeasy/simple-web:latest
```
Now go and try to access the port 80 of your VM with a webbrowser!
You should see something like that:
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/http_simple_web.png)

Now let us inspect the current status of docker.
```bash
docker container ps
	CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS         PORTS                               NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   13 seconds ago   Up 9 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   laughing_taussig
```
You can see that the container is still running.

### Simulate a internal error from within the container
Now let us jump into the container and kill the application manually:
```bash
docker container ps
	CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                               NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   5 minutes ago   Up 5 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   laughing_taussig

docker container exec -it a0260d433daf bash

root@a0260d433daf:/code# ps -ef
	UID          PID    PPID  C STIME TTY          TIME CMD
	root           1       0  0 10:30 ?        00:00:00 /bin/sh -c python index.py
	root           7       1  0 10:30 ?        00:00:00 python index.py
	root          14       0  1 10:36 pts/0    00:00:00 bash
	root          21      14  0 10:36 pts/0    00:00:00 ps -ef

root@a0260d433daf:/code# kill 7

docker container ps
	CONTAINER ID   IMAGE                     COMMAND                  CREATED         STATUS         PORTS                               NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   7 minutes ago   Up 6 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   laughing_taussig
```
As you can see, the container has now a **lower uptime** because of the automated restart.

## Stop a container running in background
```bash
docker container ps
	CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS         PORTS                               NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   12 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp, :::80->80/tcp   laughing_taussig

docker container stop a0260d433daf
	a0260d433daf

docker container ps
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES

docker container ps -a
	CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS                        PORTS     NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   13 minutes ago   Exited (137) 12 seconds ago             laughing_taussig

docker container rm a0260d433daf
	a0260d433daf

docker images
	REPOSITORY         TAG       IMAGE ID       CREATED       SIZE
	yeasy/simple-web   latest    172c78152bf6   3 years ago   679MB

docker rmi yeasy/simple-web
	Untagged: yeasy/simple-web:latest
	Untagged: yeasy/simple-web@sha256:356de309052fe233ba08eb4c9ad85ab89398f31555e8777326d57307ac913727
	Deleted: sha256:172c78152bf688785a3886063f586af38dbb18c59587f0a90bd57490ef06c251
	...
	Deleted: sha256:8fad67424c4e7098f255513e160caa00852bcff347bc9f920a82ddf3f60229de

docker images
	REPOSITORY   TAG       IMAGE ID   CREATED   SIZE
```

Do you remember the <tt>--rm</tt> option. 
Can you explain the benefit and disadvantage of it?  

## Stopping containers
If you need to stop a runing container, you might want to let the container finish its work and clean up the data.
So <tt>stop</tt> should be your preferred option.
You can as well use the <tt>kill</tt>option, but then you give the container no time to finish its work.
To give the container a limit to finish its work and if it do not, kill it, might be a good practice:
```bash
docker stop -t 30 <container-id>
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA1Mjg0MzEwMSwxNzk3MDI5NTAyLDY1MT
IwNTk1NiwxMzc3MjY2NjUwLC0xMjgwMDI0OTM2LC0xMzA4NTY2
MzldfQ==
-->