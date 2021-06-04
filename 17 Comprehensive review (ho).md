# Comprehensive review
To see if we did understand what we learned today, we deploy a multi container application

This is a classic Docker application deployment with persistent storage and two containers
```bash
mkdir database

docker run -d --restart unless-stopped --name db -e POSTGRES_DB=wiki -e POSTGRES_PASSWORD=wikijsrocks -e POSTGRES_USER=wikijs -v $PWD/database:/var/lib/postgresql/data postgres:11-alpine

docker run -d -p 80:3000 --restart unless-stopped --name wiki --link db:db -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_USER=wikijs -e DB_PASS=wikijsrocks -e DB_NAME=wiki requarks/wiki:
```
 
## Exercise
*  Read the [documentation](https://docs.requarks.io/install/docker) of wikijs
	* Setup a mariadb with docker
	* Setup a wikijs that connects to this service
	* write some content into the wiki
* stop the containers
* remove the containers
* deploy the application again
* verify if you can access the content again

## Addon
* Pack the db directory into a tar.gz and move it to your desktop
* Note the comands you used to deploy the wikijs with mariadb in a save place
* Restore the VM snapshot of your docker node
* Install docker
* Unpack your archive
* Start the container

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg3MjYxNjgxLC0xMDY3NDUxNTMzXX0=
-->