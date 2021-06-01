# Docker command-line help

## Online resources

### Docker CLI
* Official
https://docs.docker.com/engine/reference/commandline/docker/
* Great alternative with examples
https://dockerlabs.collabnix.com/docker/cheatsheet/


## Cherry picking
After a few days with docker, you might see the value of this examples as well.
Just try it out and let us discuss the value/need of this pr
## Find listen ports of a docker image
```bash
docker pull nodered/node-red

docker inspect --format="{{json .Config.ExposedPorts }}"  nodered/node-red
	{"1880/tcp":{}}
```

## Examine the logs of a running container
```bash 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3OTI3MzUzXX0=
-->