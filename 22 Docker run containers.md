
Now go and try to access the port 80 of your VM with a webbrowser!
You should see something like that:
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/http_simple_web.png)

Now let us inspect the current status of docker.
```bash

```

As with real operating systems services, we can decide if containers should restart, run in background, and so on.
So we do now

## Start a container in background
```bash
docker container run -d --restart unless-stopped -p 80:80 yeasy/simple-web:latest
	Unable to find image 'yeasy/simple-web:latest' locally
	latest: Pulling from yeasy/simple-web
	f2b6b4884fc8: Pull complete 
	...
	f05b81527a11: Pull complete 
	779bb3fb81b2: Pull complete 
	Digest: sha256:356de309052fe233ba08eb4c9ad85ab89398f31555e8777326d57307ac913727
	Status: Downloaded newer image for yeasy/simple-web:latest
	a0260d433daf4146c42015029e269234038284e35739f4bfb42dde75177bb6c2
docker container ps
	CONTAINER ID   IMAGE                     COMMAND                  CREATED          STATUS         PORTS                               NAMES
	a0260d433daf   yeasy/simple-web:latest   "/bin/sh -c 'python …"   13 seconds ago   Up 9 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   laughing_taussig
```
If you now logout and login back again, you can see that the container is still running.

Now let us jump into the container and kill the application:
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
As you can see, the container has now a lower uptime because of the automated restart.

Let us clean up again
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
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4NTQxNzgwNTYsMjc5MDI1MDg3LDU2Mz
YzNDkxMl19
-->