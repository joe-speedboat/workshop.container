# Docker Container Storage

By default all files created inside a container are stored on a writable container layer. 
This means that:

* The data doesn’t persist when that container no longer exists, and it can be difficult to get the data out of the container if another process needs it.
 * A container’s writable layer is tightly coupled to the host machine where the container is running. You can’t easily move the data somewhere else.
 * Writing into a container’s writable layer requires a storage driver to manage the filesystem. The storage driver provides a union filesystem, using the Linux kernel. This extra abstraction reduces performance as compared to using data volumes, which write directly to the host filesystem.

Docker has two options for containers to store files in the host machine, so that the files are persisted even after the container stops: volumes, and bind mounts. If you’re running Docker on Linux you can also use a tmpfs mount. If you’re running Docker on Windows you can also use a named pipe.

An easy way to visualize the difference among volumes, bind mounts, and tmpfs mounts is to think about where the data lives on the Docker host.

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/types-of-mounts.png)
## Choose the right type of mount
Types of mounts and where they live on the Docker host.
* Volumes are stored in a part of the host filesystem which is managed by Docker (/var/lib/docker/volumes/ on Linux). Non-Docker processes should not modify this part of the filesystem. Volumes are the best way to persist data in Docker.
* Bind mounts may be stored anywhere on the host system. They may even be important system files or directories. Non-Docker processes on the Docker host or a Docker container can modify them at any time.
* tmpfs mounts are stored in the host system’s memory only, and are never written to the host system’s filesystem.

No matter which type of mount you choose to use, the data looks the same from within the container. 
It is exposed as either a directory or an individual file in the container’s filesystem.

# Volumes
[read the docs](https://docs.docker.com/storage/volumes/)



## Config files

# Bind mounts
[read the docs](https://docs.docker.com/storage/bind-mounts/)
Bind mounts have been around since the early days of Docker. Bind mounts have limited functionality compared to [volumes](https://docs.docker.com/storage/volumes/). When you use a bind mount, a file or directory on the _host machine_ is mounted into a container. The file or directory is referenced by its absolute path on the host machine. By contrast, when you use a volume, a new directory is created within Docker’s storage directory on the host machine, and Docker manages that directory’s contents.

The file or directory does not need to exist on the Docker host already. It is created on demand if it does not yet exist. Bind mounts are very performant, but they rely on the host machine’s filesystem having a specific directory structure available. If you are developing new Docker applications, consider using [named volumes](https://docs.docker.com/storage/volumes/) instead. You can’t use Docker CLI commands to directly manage bind mounts.

# tmpfs
[read the docs](https://docs.docker.com/storage/tmpfs/)
When you create a container with a `tmpfs` mount, the container can create files outside the container’s writable layer.
As opposed to volumes and bind mounts, a `tmpfs` mount is temporary, and only persisted in the host memory. When the container stops, the `tmpfs` mount is removed, and files written there won’t be persisted.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMDk5MTE3MzEsLTEzODkyODY1NTVdfQ
==
-->