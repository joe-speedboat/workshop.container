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


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkyNzUxNjY5NSwxNjAwNzA3Mzg5LC0yOD
c3Mjg5OTZdfQ==
-->