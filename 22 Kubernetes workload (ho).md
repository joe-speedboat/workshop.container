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

```bash
grep namespace *
	ingress.yml:  namespace: nodered
	pod.yml:  namespace: nodered

grep host *
	ingress.yml:  - host: k3s.mydomain.com

# change host to fit your needs
vim ingress.yml
```

## Deploy the workload
- please not, that the pod will not get deployed by kubectl, it's integrated in the kubernetes deployment resource.
```bash
# create nodered namespace
kubectl create namespace nodered
	namespace/nodered created

# switch to namespace, so that new resouces get created within if they have not namespace defined within
kubectl config set-context --current --namespace=nodered
	Context "default" modified.

# find the resources we downloaded before
ls -1
	deployment.yml
	ingress.yml
	pod.yml
	pvc.yml
	svc.yml

# create the physical volume claim, pls. node the action of storage auto provisioner
kubectl create -f pvc.yml
	persistentvolumeclaim/nodered-claim created

# create the deployment, this will also create the pod 
kubectl create -f deployment.yml 
	deployment.apps/nodered created
# create the service, so connectivity to container will be possible
kubectl create -f svc.yml 
	service/nodered created

kubectl create -f ingress.yml 
	ingress.networking.k8s.io/www created

kubectl get all
	NAME                           READY   STATUS    RESTARTS   AGE
	pod/nodered-7c68d6cccd-bklhl   1/1     Running   0          19s

	NAME              TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
	service/nodered   ClusterIP   10.43.171.204   <none>        1880/TCP   14s

	NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
	deployment.apps/nodered   1/1     1            1           19s

	NAME                                 DESIRED   CURRENT   READY   AGE
	replicaset.apps/nodered-7c68d6cccd   1         1         1       19s

# you can as well check the k8s events. CTRL-C to exit
kubectl get events --all-namespaces -w

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyODI3NTQ4NjUsMTY4NzMwMTQwLC03MD
cwNTQyOTgsLTE2MjU0MTI4MzFdfQ==
-->