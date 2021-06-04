# K3S Setup - hands on
[K3S homepage](https://k3s.io/)
K3S is a minimalistic Kubernetes distribution which moved all Kubernetes components into containers and reduced them to the absolute minimum. 

But in the end, K3S is a fully functioning Kubernetes distribution, which has its Target on lightweight setups like:
- Embedded Computers
- Closed Product shipping
- Secured Docker application deployments

## Reset LAB VM
Please reset your LAB VM to the minimal setup and start with the exercise below:

## Prepare the OS
```bash
dnf -y upgrade
dnf -y install vim tar wget jq git bash-completion lsof

sed -i  '/swap/d' /etc/fstab
swapoff -a

dnf -y install firewalld
systemctl enable firewalld --now
firewall-cmd --permanent --zone=public --set-target=ACCEPT
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --reload
reboot
```

## Install K3S
```bash
curl -sfL https://get.k3s.io | sh

cat /etc/systemd/system/k3s.service
systemctl status k3s

kubectl get nodes
# all pods in running state? fine!
kubectl get pods --all-namespaces
```

## Create Wildcard DNS for ingress routing
-   Create a CNAME
```
*.vm-name.domain.tld -> vm-name.domain.tld
```    
If you can't do so, you have to create entries in your hosts file for every application in the labs.
No problem, but not really nerdy! ;-/


##
 curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | sh
 grep 'helm completion bash' $HOME/.bashrc || echo 'source <(helm completion bash)' >> $HOME/.bashrc

 grep KUBECONFIG $HOME/.bashrc || echo 'export KUBECONFIG=/etc/rancher/k3s/k3s.yaml' >> $HOME/.bashrc


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1MDk5NDI0MCw3MzA5OTgxMTZdfQ==
-->