# Docker container debugging

## Find listen ports of a docker image
```bash
docker inspect --format="{{json .Config.ExposedPorts }}"  nodered/node-red
```


## Examine the logs of a running container
```bash 

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTQ4NDExNDk3NCwtNjE2NzU0NzQ2LC0xOT
c2OTAzNjYzLDE2NTU3NTQ2ODhdfQ==
-->