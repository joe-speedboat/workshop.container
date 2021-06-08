# Deploy Kubernetes native workload
TIME: 15 min

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
Please download this files as mentioned above and then look at this files and try to match the resources to the drawing below.


## Understand k8s resources 
![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/k8s_workload.png)

## Edit the application resources to fit your needs




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTcwNzA1NDI5OCwtMTYyNTQxMjgzMV19
-->