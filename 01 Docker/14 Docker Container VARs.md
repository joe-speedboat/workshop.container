# Docker Container Variables
Variables are used to inject variable Information into a container or image.
If we do it during the build time, it is called an ARG. ARGs are not visible in running containers.
In running containers, this variables are called ENV. ENVs are visible in running containers.

![enter image description here](https://github.com/joe-speedboat/workshop.container/raw/main/images/docker_env_arg.png)
## Setting ARG Values
How to set them, and where? 
You can leave them blank in the Dockerfile, or set default values. 
If you don’t provide a value to expected ARG variables which don’t have a default, you’ll get an error message.

Here is a Dockerfile example, both for default values and without them:

```
ARG myarg
# or with a hard-coded default:
#ARG myarg=default_value

RUN echo "OMG look at that $myarg"
# you could also use braces - ${myarg}

```

[relevant docs](https://docs.docker.com/engine/reference/builder/#arg)

When building a Docker image from the commandline, you can set **ARG** values using _–build-arg_:

```
$ docker build --build-arg myarg=custom_value

```

Running that command, with the above Dockerfile, will result in the following line being printed (among others):

```
OMG look at that custom_value

```

## Setting ENV Values

So, how to set ENV values? 
You can do it when starting your containers, but you can also provide default ENV values directly in your Dockerfile by hard-coding them. Also, you can set dynamic default values for environment variables!

When building an image, the only thing you can provide are ARG values, as described above. 
You can’t provide values for ENV variables directly. 
However, both ARG and ENV can work together. 
You can use ARG to set the default values of ENV vars. 
Here is a basic Dockerfile, using hard-coded default values:

```
# no default value
ENV myenv
# a default value
ENV foo /bar
# or ENV foo=/bar

# ENV values can be used during the build
ADD . $foo
# or ADD . ${foo}
# translates to: ADD . /bar
```
[relevant docs](https://docs.docker.com/engine/reference/builder/#env)

And here is a snippet for a Dockerfile, using dynamic on-build env values:
```
# expect a build-time variable
ARG A_VARIABLE
# use the value to set the ENV var default
ENV an_env_var=$A_VARIABLE
# if not overridden, that value of an_env_var will be available to your containers!
```

**Once the image is built**, you can launch containers and provide values for ENV variables in **different ways**. All of those will override any default ENV values in the Dockerfile. 
Unlike ARG, you can pass all kinds of environment variables to the container. Even ones not explicitly defined in the Dockerfile. 
It depends on your application whether that’ll do anything however.

### 1. Provide values one by one
From the commandline, use the -e flag:
```
$ docker run -e "env_var_name=another_value" alpine env
```
[relevant docs](https://docs.docker.com/engine/reference/builder/#environment-replacement)

### 2. Pass environment variable values from your host
It’s the same as the above method. The only difference is, you don’t provide a value, but just name the variable. This will make Docker access the current value in the host environment and pass it on to the container.
```
$ docker run -e env_var_name alpine env
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNDQzNjQ5NjgyXX0=
-->