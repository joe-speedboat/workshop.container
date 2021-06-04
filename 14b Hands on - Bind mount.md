
# Docker Container Storage - hands on

## Bind mount 

 - [x] avoid using `bind mounts` if you can

### Cleanup your previous work before you continue
```bash
[root@node ~]# docker ps -a
	CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS          PORTS                                   NAMES
	5a425a91d63c   mazzolino/tiddlywiki   "docker-entrypoint.s…"   16 minutes ago   Up 16 minutes   0.0.0.0:80->8080/tcp, :::80->8080/tcp   wiki
[root@node ~]# docker kill wiki
	5a425a91d63c
[root@node ~]# docker rm wiki
	wiki
[root@node ~]# rm -rf webroot
```

### Store persistent data of container via bind mount
```bash
[root@node ~]# mkdir $PWD/webroot

[root@node ~]# docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	Unable to find image 'mazzolino/tiddlywiki:latest' locally
	latest: Pulling from mazzolino/tiddlywiki
	...
	dc753678d06baae59e46b95945eeb689acc0082d9f35ca9ec93f5b61c2bd01d4

[root@node ~]# docker logs wiki
	Copied edition 'server' to mywiki
	 syncer-server-filesystem: Dispatching 'save' task: $:/StoryList 
	Serving on http://0.0.0.0:8080
```

* Now go and write some content into the web page
[read the docs](https://hub.docker.com/r/mazzolino/tiddlywiki)
User: user
PW: wiki

* Stop and remove the container
```bash
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

[root@node ~]# docker rm wiki
	wiki

[root@node ~]# docker ps -a
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

* now start over and see if content got restored
```bash
[root@node ~]# docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	5a425a91d63c48ac9ac34d50b92cdff058cb7004466f49dce6293938a2b96e0e
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyOTIwMDg2MDBdfQ==
-->