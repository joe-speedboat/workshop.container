
# Docker Container Storage - hands on
TIME: 15 min

## Bind mount 

 - [x] avoid using `bind mounts` if you can

### Cleanup your previous work before you continue
```bash
docker ps -a
	CONTAINER ID   IMAGE                  COMMAND                  CREATED          STATUS          PORTS                                   NAMES
	5a425a91d63c   mazzolino/tiddlywiki   "docker-entrypoint.s…"   16 minutes ago   Up 16 minutes   0.0.0.0:80->8080/tcp, :::80->8080/tcp   wiki

docker kill wiki
	5a425a91d63c

docker rm wiki
	wiki

rm -rf webroot
```

### Store persistent data of container via bind mount
```bash
mkdir $PWD/webroot

docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
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
docker run -d -it -p 80:8080 --restart unless-stopped --mount type=bind,source=$PWD/webroot,target=/var/lib/tiddlywiki --name wiki mazzolino/tiddlywiki
	5a425a91d63...3938a2b96e0e
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMDMyODY5ODNdfQ==
-->