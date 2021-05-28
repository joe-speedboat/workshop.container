# Containers


## Running Containers interactively
So lets start a first command inside the container
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
If you compare the IP you got with the OS IP, you can see that they are different.
We will look later deeper into the shared and/other separated components of a container.
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjA2NzU1NTkzMV19
-->