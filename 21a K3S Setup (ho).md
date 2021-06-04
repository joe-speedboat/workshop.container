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

firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --reload
reboot
```

## Install K3S
```bash



<!--stackedit_data:
eyJoaXN0b3J5IjpbMjg2ODU2MDA3LDczMDk5ODExNl19
-->