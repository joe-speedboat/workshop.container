# Deploy Kubernetes native workload
TIME: 15 m

Let us deploy a Kubernetes native workload.
So we can get familiar with some of the components.

## Get k8s resources
```bash
cd
mkdir nodered
cd nodered
for r in deployment.yml ingress.yml pod.yml pvc.yml svc.yml
do
   wget https://raw.githubusercontent.com/joe-speedboat/workshop.docker/main/files/k8s/nodered/$r
done
```
Pleas download this files as mentioned above and then look at this files and try to match the resources to the drawing below.


## Understand k8s resources 
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/k8s_workload.png)

## Configure depending container resources
Of course it is not given at any time that container needs are written to the logs.
If you can't find out the needs, you should look for:
- container registry documentation at  [dockerhub](https://hub.docker.com/r/nodered/node-red)
- Use `docker inspect` to look into a container
- Read the `Dockerfile` to see how the container got built.


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTI4MzM4ODQ1OSwtMTYyNTQxMjgzMV19
-->