# Container Architecture
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. With Docker, you can manage your infrastructure in the same ways you manage your applications. By taking advantage of Docker’s methodologies for shipping, testing, and deploying code quickly, you can significantly reduce the delay between writing code and running it in production.

## Docker  Containers vs. Operating System Applications
Docker, Kubernetes, and containers are indeed powerful technologies that can bring many benefits to a business. However, depending on what kind of workload you have, you might need to stick to using virtual machines (VMs) instead, or a combination of both containers and VMs.
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/containers-vs-virtual-machines.jpg)
## Under the hood
Let’s discuss a few key things before we dig deeper
# **_Namespaces_**

_Docker uses a technology called_ `_namespaces_` _to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container._

_These namespaces provide a layer of isolation. Each aspect of a container runs in a separate namespace and its access is limited to that namespace._

_Docker Engine uses namespaces such as the following on Linux:_

-   **_The_** `_pid_**` **_namespace:_** _Process isolation (PID: Process ID)._
-   **_The_** `_net_**` **_namespace:_** _Managing network interfaces (NET: Networking)._
-   **_The_** `_ipc_**` **_namespace:_** _Managing access to IPC resources (IPC: InterProcess Communication)._
-   **_The_** `_mnt_**` **_namespace:_** _Managing filesystem mount points (MNT: Mount)._
-   **_The_** `_uts_` **_namespace:_** _Isolating kernel and version identifiers. (UTS: Unix Timesharing System)._

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzOTUzODcxMzgsMTY3OTc5NTE4MywxMT
M2NDE1MzM5XX0=
-->