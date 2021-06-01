# Containers
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

## Container start options
Did you notice that the container immediately returned to the  operating system after executing the desired command?
A container image may suggest the process that get started after container is going up, but we can always override this settings.
So let us take a look of some of this options to get a better understanding:


### docker container run
This means we start a new container out of an image.

### --interactive --tty
This means that the container does avoid to run in background. The tty reason which allocates a terminal makes sense if you use the interactive option. You can see this options often in short form: <tt>-it</tt>

### --rm
This means that the container s
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc4MTQ2MDE2MSwtMTI4MDAyNDkzNiwtMT
MwODU2NjM5XX0=
-->