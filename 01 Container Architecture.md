# Container Architecture
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

## Docker  Containers vs. Operating System Applications
Docker, Kubernetes, and containers are indeed powerful technologies that can bring many benefits to a business. However, depending on what kind of workload you have, you might need to stick to using virtual machines (VMs) instead, or a combination of both containers and VMs.
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/containers-vs-virtual-machines.jpg)
## Namespaces
Docker uses a technology called `namespaces` to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container.
These namespaces provide a layer of **isolation**. Each aspect of a container runs in a separate namespace and its access is limited to that namespace.

Docker Engine uses namespaces such as the following on Linux:
-   **_The_** `pid` **_namespace:_** _Process isolation (PID: Process ID)._
-   **_The_** `net` **_namespace:_** _Managing network interfaces (NET: Networking)._
-   **_The_** `ipc` **_namespace:_** _Managing access to IPC resources (IPC: InterProcess Communication)._
-   **_The_** `mnt` **_namespace:_** _Managing filesystem mount points (MNT: Mount)._
-   **_The_** `uts` **_namespace:_** _Isolating kernel and version identifiers. (UTS: Unix Timesharing System)._

## Control groups
Docker Engine on Linux also relies on another technology called control groups (`cgroups`). A cgroup limits an application to a specific set of resources. Control groups allow Docker Engine to share available hardware resources to containers and optionally **enforce limits** and **constraints**. For example, you can limit the memory available to a specific container.

## Union file systems
Union file systems, or UnionFS, are file systems that operate by **creating layers**, making them very lightweight and fast. Docker Engine uses UnionFS to provide the building blocks for containers. Docker Engine can use multiple UnionFS variants, including AUFS, btrfs, **vfs**, and **DeviceMapper**.

## Container format
Docker Engine combines the **namespaces**, **control groups**, and **UnionFS** into a wrapper called a container format. The default container format is `libcontainer`.

Under the hood might not be the correct heading for this topic, but these are things which strike me when I first start using Docker.

The usage and handling of Docker Containers is depending on several components, below I tried to describe it in a meaning way, so we can discuss it now...

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/docker_overview_bychris.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU1OTA3MTg5OCwtMjY4MzY0NzYyLC0xND
IwODgyMTQwXX0=
-->