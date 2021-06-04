# Application Orchestration Technologies

## The past and the future

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/evol.png)
Even if you can repeat and automate your docker container deployments easily. 
It will become bigger and complexer with the amount of applications you maintain.

## The Virtual Machine vs Containers problem
Even if the deployment of an VM got automated this days, lot of manual work is needed to configure complex applications.
This makes it difficult to document, update, migrate your applications.

As you learned in this course, VMs and Containers have complete different approaches and needs about its ressources/components:
- Networking
- Storage
- Administration
- Configuration
- Documentation
- Backup/Restore
- Application Snapshoting
- Application Rollback
- Application Migration

## Kubernetes and VMs, everythin gets better or at least different?
Kubernetes is the new standard in Container management and to be honest, it does a fantastic job.
So all the Docker workload is moving into a Kubernetes Cluster ... sooner or later!
Kubernetes does orchestrate the whole container lifecycle:
- Deployment
- Configuration
- Storage
- Networking
- Security
- Lifecycle
Operators are a big step into this direction, since the migration of Docker applications into new versions needed often some attention. Operators are containerized system administrators that maintain a kind of workload.
This might be prometheus (which initally developed the operator concept)


![enter image description here](https://raw.githubusercontent.com/joe-speedboat/workshop.docker/main/images/components-of-kubernetes.svg)
If it is a K8S native, K3S, RKE, Tanzu, OpenShift or even OKD ... it doesn't matter.
At least for the next five to ten years, we will have some VMs running that have to interact with 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MzEwNjg4MTddfQ==
-->