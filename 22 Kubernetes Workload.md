# Deploy Kubernetes native workload
Let us deploy a Kubernetes native workload.
So we can get familiar with some of the components.

```bash
  # kubectl create namespace nodered
namespace/nodered created
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
# kubectl config set-context --current --namespace=nodered
Context "default" modified.
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
# kubectl create deployment --image=nodered/node-red nodered
deployment.apps/nodered created
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          9s
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
# kubectl get events
LAST SEEN   TYPE     REASON              OBJECT                          MESSAGE
16s         Normal   ScalingReplicaSet   deployment/nodered              Scaled up replica set nodered-7555b955f9 to 1
16s         Normal   SuccessfulCreate    replicaset/nodered-7555b955f9   Created pod: nodered-7555b955f9-9s88b
16s         Normal   Scheduled           pod/nodered-7555b955f9-9s88b    Successfully assigned nodered/nodered-7555b955f9-9s88b to k3s
16s         Normal   Pulling             pod/nodered-7555b955f9-9s88b    Pulling image "nodered/node-red"
0s          Normal   Pulled              pod/nodered-7555b955f9-9s88b    Successfully pulled image "nodered/node-red" in 15.644227527s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          20s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          27s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          33s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          35s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          37s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
# kubectl get pods
NAME                       READY   STATUS    RESTARTS   AGE
nodered-7555b955f9-9s88b   1/1     Running   0          40s

  


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE1NzU4ODQ5MSw3MzA5OTgxMTZdfQ==
-->