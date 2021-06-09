# Docker Container Storage - hands on
TIME: 15 min

## Docker Volumes

 - [x] this is the standard, use it wherever you can.

### Cleanup your previous work before you continue
```bash
docker ps -a
	CONTAINER ID   IMAGE           COMMAND      CREATED         STATUS         PORTS                               NAMES
	9c8e05bbfe05   sebp/lighttpd   "start.sh"   4 seconds ago   Up 2 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp   web
	
docker stop web
	dweb
docker rm web
	web
docker ps -a
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

### Store persistent data via Volume
```bash
mkdir $PWD/webroot
docker run -d -it -p 80:8080 --restart unless-stopped -v $PWD/webroot:/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	Unable to find image 'mazzolino/tiddlywiki:latest' locally
	latest: Pulling from mazzolino/tiddlywiki
	...
	dc753678d06baae59e46b95945eeb689acc0082d9f35ca9ec93f5b61c2bd01d4

docker logs wiki
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
find webroot/
	webroot/
	webroot/mywiki
	webroot/mywiki/tiddlywiki.info
	webroot/mywiki/tiddlers
	webroot/mywiki/tiddlers/$__StoryList.tid
	webroot/mywiki/tiddlers/here we go.tid

docker stop wiki
	wiki

docker ps -a
	CONTAINER ID   IMAGE                  COMMAND                  CREATED              STATUS                       PORTS     NAMES
	dc753678d06b   mazzolino/tiddlywiki   "docker-entrypoint.s…"   About a minute ago   Exited (137) 4 seconds ago             wiki

docker rm wiki
	wiki

docker ps -a
	CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

* now start over and see if content got restored
```bash
docker run -d -it -p 80:8080 --restart unless-stopped -v $PWD/webroot:/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	5a425a91d63c48ac9ac34d50b92cdff058cb7004466f49dce6293938a2b96e0e
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgxODQ1ODc4NSwtODk5MDg1NjkyXX0=
-->