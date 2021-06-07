# Deploy Kubernetes native workload
Let us deploy a Kubernetes native workload.
So we can get familiar with some of the components.

## Deploy a node-red pod
```bash
kubectl create namespace nodered
	namespace/nodered created
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
kubectl config set-context --current --namespace=nodered
	Context "default" modified.
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
kubectl create deployment --image=nodered/node-red nodered
	deployment.apps/nodered created
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
kubectl get pods
	NAME                       READY   STATUS              RESTARTS   AGE
	nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          9s
### 07.06.2021_10:19 root@k3s:~ ✯ nodered 
kubectl get events
LAST SEEN   TYPE     REASON              OBJECT                          MESSAGE
	nodered/nodered-7555b955f9-9s88b to k3s
	16s         Normal   Pulling             pod/nodered-7555b955f9-9s88b    Pulling image "nodered/node-red"
	0s          Normal   Pulled              pod/nodered-7555b955f9-9s88b    Successfully pulled image "nodered/node-red" in 15.644227527s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
kubectl get pods
NAME                       READY   STATUS              RESTARTS   AGE
nodered-7555b955f9-9s88b   0/1     ContainerCreating   0          20s
### 07.06.2021_10:20 root@k3s:~ ✯ nodered 
kubectl get pods
	NAME                       READY   STATUS    RESTARTS   AGE
	nodered-7555b955f9-9s88b   1/1     Running   0          40s
```
  
## Examine container logs

    kubectl logs nodered-7555b955f9-9s88b 

```bash
> node-red-docker@1.3.5 start /usr/src/node-red
> node $NODE_OPTIONS node_modules/node-red/red.js $FLOWS "--userDir" "/data"

7 Jun 08:20:24 - [info] 

Welcome to Node-RED
===================

7 Jun 08:20:24 - [info] Node-RED version: v1.3.5
7 Jun 08:20:24 - [info] Node.js  version: v10.24.1
7 Jun 08:20:24 - [info] Linux 4.18.0-305.3.1.el8_4.x86_64 x64 LE
7 Jun 08:20:24 - [info] Loading palette nodes
7 Jun 08:20:24 - [info] Settings file  : /data/settings.js
7 Jun 08:20:24 - [info] Context store  : 'default' [module=memory]
7 Jun 08:20:24 - [info] User directory : /data
7 Jun 08:20:24 - [warn] Projects disabled : editorTheme.projects.enabled=false
7 Jun 08:20:24 - [info] Flows file     : /data/flows.json
7 Jun 08:20:24 - [warn] 

---------------------------------------------------------------------
Your flow credentials file is encrypted using a system-generated key.

If the system-generated key is lost for any reason, your credentials
file will not be recoverable, you will have to delete it and re-enter
your credentials.

You should set your own key using the 'credentialSecret' option in
your settings file. Node-RED will then re-encrypt your credentials
file using your chosen key the next time you deploy a change.
---------------------------------------------------------------------

7 Jun 08:20:24 - [info] Server now running at http://127.0.0.1:1880/
7 Jun 08:20:25 - [info] Starting flows
7 Jun 08:20:25 - [info] Started flows
```

From logs you can take two needs of the current container:
- Persistent volume (storage): `/data`
- Listen port: `1880`

Of course it is not given at any time that container needs are written to the logs.
If you can't find out the needs, you should look for:
- container registry documentation at  [dockerhub](https://hub.docker.com/r/nodered/node-red)
- Use docker inspect to look into a container
- Read the `Dockerfile` to see how the container got built
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTk3NjMzNzAxLC0xODIxNTY1NTEzLDczMD
k5ODExNl19
-->