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
sleep 10
kubectl get crd

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MTIxODgyNTAsMTYwMDcwNzM4OSwtMj
g3NzI4OTk2XX0=
-->