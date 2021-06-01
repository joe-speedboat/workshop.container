# Setup Docker
In March 2017, Docker released Docker Enterprise Edition (EE), merging their previous enterprise offering of Docker Datacenter and renaming their free offering to Docker Community Edition (CE).

Docker Inc. positions CE for development and Docker EE for business-critical deployments. In this article, we’ll dive deeper into the differences between Docker CE and Docker EE, so you can identify the best option for your project as it stands today, and the best option for your project as it matures.

## Docker CE vs EE: An Overview
Docker CE is a free and open source containerization platform. It is a rebranded version of the Docker open source solution that has been freely available since the launch of Docker in 2013.

CE can run on Windows 10 and Mac, on Azure and AWS, as well as CentOS, Debian, Fedora, and Ubuntu. CE can be downloaded directly from the Docker Store.

Docker EE, on the other hand, is a premium version of CE. Docker EE is an integrated, fully supported, and certified container platform that runs on Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES), Oracle Linux, Ubuntu, Windows Server 2016, as well as Azure and AWS.

## Setup a Docker CE host on CentOS8
This user can be used later on to manage Docker, but will have no privileges to manage the underlying operating system.

### Install Docker CE
```
yum -y install epel-release
yum install -y yum-utils device-mapper-persistent-data lvm2
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum -y install docker-ce docker-ce-cli containerd.io
systemctl start docker
systemctl enable docker
```
### Create Docker Admin
```
useradd dadmin
usermod -aG docker dadmin
```

### Configure Firewalling
```bash
dnf -y install firewalld
systemctl enable firewalld --now
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --zone=public --add-masquerade --permanent
firewall-cmd --reload
```

### Install helpers

```bash
dnf -y install vim tar wget jq git bash-completion
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTgzNzc5MDAzMSwtMTk3NzY1MDA1NF19
-->