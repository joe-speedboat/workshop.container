# Docker Container Variables
Variables are used to inject variable Information into a container or image.
If we do it during the build time, it is called an ARG. ARGs are not visible in running containers.
In running containers, this variables are called ENV. ENVs are visible in running containers.

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/docker_env_arg.png)
## Setting ARG Values
How to set them, and where? 
You can leave them blank in the Dockerfile, or set default values. 
If you don’t provide a value to expected ARG variables which don’t have a default, you’ll get an error message.

Here is a Dockerfile example, both for default values and without them:

```
ARG some_variable_name
# or with a hard-coded default:
#ARG some_variable_name=default_value

RUN echo "Oh dang look at that $some_variable_name"
# you could also use braces - ${some_variable_name}

```

[relevant docs](https://docs.docker.com/engine/reference/builder/#arg)

When building a Docker image from the commandline, you can set **ARG** values using _–build-arg_:

```
$ docker build --build-arg some_variable_name=a_value

```

Running that command, with the above Dockerfile, will result in the following line being printed (among others):

```
Oh dang look at that a_value

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3MzUyMTU2NywtOTQ3ODM3NTYzXX0=
-->