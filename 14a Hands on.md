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

### Store persistent data of container
```bash
[root@node ~]# docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	Unable to find image 'mazzolino/tiddlywiki:latest' locally
	latest: Pulling from mazzolino/tiddlywiki
	...
	dc753678d06baae59e46b95945eeb689acc0082d9f35ca9ec93f5b61c2bd01d4
[root@node ~]# docker logs wiki
[root@node ~]# docker logs wiki
Copied edition 'server' to mywiki
 syncer-server-filesystem: Dispatching 'save' task: $:/StoryList 
Serving on http://0.0.0.0:8080
(press ctrl-C to exit)
[root@node ~]# find webroot/
webroot/
webroot/mywiki
webroot/mywiki/tiddlywiki.info
webroot/mywiki/tiddlers
webroot/mywiki/tiddlers/$__StoryList.tid
webroot/mywiki/tiddlers/here we go.tid
[root@node ~]# docker stop wiki
wiki
[root@node ~]# docker ps -a
CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS                       PORTS     NAMES
dc753678d06b   mazzolino/tiddlywiki   "docker-entrypoint.s…"   About a minute ago   Exited (137) 4 seconds ago             wiki
[root@node ~]# docker rmi wiki
Error: No such image: wiki
[root@node ~]# docker rm wiki
wiki
[root@node ~]# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[root@node ~]# docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
5a425a91d63c48ac9ac34d50b92cdff058cb7004466f49dce6293938a2b96e0e


```
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTA1ODc0MTYzLC03MTk4MTU0NDgsMjA5MD
E5MTMyOCwxNzcyODAyNDU2LDE2ODE3ODE4MDddfQ==
-->