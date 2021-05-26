# Docker container debugging

## Find listen ports of a docker image
```bash
docker pull nodered/node-red

docker inspect --format="{{json .Config.ExposedPorts }}"  nodered/node-red
	{"1880/tcp":{}}
```

## Examine the logs of a running container
```bash 

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYxNjE1MTY2NF19
-->