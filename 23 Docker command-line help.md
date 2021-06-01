# Docker command-line help

## Online resources

### Docker CLI
* Official
https://docs.docker.com/engine/reference/commandline/docker/
* Great alternative with examples
https://dockerlabs.collabnix.com/docker/cheatsheet/


## Cherry picking
After a few days with docker, you might see the value of this examples as well.
Just try it out and let us discuss the value/need of this hints.

### Find listen ports of a docker image
```bash
docker pull nodered/node-red

docker inspect --format="{{json .Config.ExposedPorts }}"  nodered/node-red
	{"1880/tcp":{}}
```

### Jump into a running container 
```bash 
# let us start a container, just to see how we can jump into

```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg1NzgyMzYwMV19
-->