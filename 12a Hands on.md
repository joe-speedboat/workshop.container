# Docker Images - hands on
TIME: 15min

* Use `man` to explore the `docker image` usage

* List the image you downloaded in last hands-on lab with the docker-cli (`sebp/lighttpd:latest`)

* Use `man` to explore the `docker inspect` usage

* Use `inspect` argument to explore the image you downloaded with docker-cli
	* Look for the section `ExposedPorts`
	* Look for the section `Volumes`

* Discuss the tasks and outcome with the class

## Identify depending container resources
If you can't find out the needs, you should look for:
- container registry documentation at  [dockerhub](https://hub.docker.com/r/nodered/node-red)
- Use `docker inspect` to look into a container
- Read the `Dockerfile` to see how the container got built.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE2MDQ0MjA1OF19
-->