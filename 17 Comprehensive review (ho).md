# Comprehensive review
To see if we did understand what we learned today, we deploy a multi container application

This is a classic Docker application deployment with persistent storage and two containers
```bash
mkdir database

docker run -d --restart unless-stopped --name db -e POSTGRES_DB=wiki -e POSTGRES_PASSWORD=wikijsrocks -e POSTGRES_USER=wikijs -v $PWD/database:/var/lib/postgresql/data postgres:11-alpine

docker run -d -p 80:3000 --restart unless-stopped --name wiki --link db:db -e DB_TYPE=postgres -e DB_HOST=db -e DB_PORT=5432 -e DB_USER=wikijs -e DB_PASS=wikijsrocks -e DB_NAME=wiki requarks/wiki:
```
 
 Now it's your turn:
*  Read the [documentation](https://docs.requarks.io/install/docker) of wikijs
* Setup a mariadb via docker
<!--stackedit_data:
eyJoaXN0b3J5IjpbNTU1MDQxMTQ2LC0xMDY3NDUxNTMzXX0=
-->