# Deploy Ansible AWX
TIME: 30 min

**Be aware, that you need 8GB of memory on your K8S, if you have not, you can not run this lab.**
## Prepare
You can find detailed instructions about this setup here:
https://github.com/ansible/awx-operator

## Deploy Operator and CRD
```bash
kubectl config set-context --current --namespace=default
kubectl apply -f https://raw.githubusercontent.com/ansible/awx-operator/devel/deploy/awx-operator.yaml
```

## Wait and verify what you have done

### wait until image got pulled
    kubectl get events -w --all-namespaces

### check for running operator pod
    kubectl get pods

### optionally check the operators logs

    kubectl logs -f deployment.apps/awx-operator

### check for new CRDs
    kubectl get crd

## Create new namespace
```bash
kubectl create namespace awx
kubectl config set-context --current --namespace=awx
```

## Create object with new CR
- `myawx.yml`
```yaml
---
apiVersion: awx.ansible.com/v1beta1
kind: AWX
metadata:
  name: awx
spec:
  ingress_type: Ingress
  route_tls_termination_mechanism: edge
  hostname: fqdn.domain.com
  ```

    kubectl apply -f myawx.yml

## Wait until images got pulled
    kubectl get events -w --all-namespaces

## Check operator logs

    kubectl logs -f deployment.apps/awx-operator -n default

### Wait for operator to finish its work
    PLAY RECAP *********************************************************************
    localhost: ok=42 changed=0 unreachable=0 failed=0 skipped=30 rescued=0 ignored=0

## Verify the deployment staus
two pods must be in running state

    kubectl get pods

## Verify awx service
notice the service port 80 for awx

    kubectl get svc
should show something like:

    NAME           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
    awx-postgres   ClusterIP   None            <none>        5432/TCP       35m
    awx-service    NodePort    10.3.12.26      <none>        80:31982/TCP   35m

## Fetch the secret and test the login

    kubectl get secret awx-admin-password -o jsonpath='{.data.password}' | base64 --decode

firefox https://fqdn.domain.com
-   user: admin

# Debugging notes

## Open Node Port for direct access

    PORT=$(kubectl describe svc awx-service | grep NodePort: | awk '{print $3}' | tr 'A-Z' 'a-z')
    echo PORT=$PORT
    firewall-cmd --zone=public --add-port=$PORT

## Disable SELinux and check autdit logs

    setenforce 0
    > /var/log/audit/audit.log 

    # do some bad things

    sealert -a /var/log/audit/audit.log

## Traefik Config

- https://levelup.gitconnected.com/a-guide-to-k3s-ingress-using-traefik-with-nodeport-6eb29add0b4b

    kubectl -n kube-system edit cm traefik

## Jump into container for debugging

# get pods

    kubectl get pods

# get containers inside of pods

    kubectl describe <pod-name>

    kubectl exec --stdin --tty <pod-name> -c <container-name> -- /bin/bash

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzI3ODcxMDRdfQ==
-->