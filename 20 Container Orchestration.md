# Application Orchestration Technologies

## The Virtual Machine vs/and Containers problem
Even if the deployment of an VM got automated this days, lot of manual work is needed to configure complex applications.
This makes it difficult to document, update, migrate your applications.

As you learned in this course, VMs and Containers have complete different approaches and needs about its ressources/components:
- Networking
- Storage
- Administration
- Configuration
- Documentation
- Backup/Restore
- Application Snapshoting
- Application Rollback
- Application Migration


## The past and the future

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/evol.png)
If it is a K8S native, K3S, RKE, Tanzu, OpenShift or even OKD ... it doesn't matter how you orchestrate your Container workload ... Everywhere, Kubernetes is inside.

Problem is, at least for the next five to ten years, we will have some VMs running that have to interact with.
Since VMware adapted the worker nodes into it's VM concept, OpenSource is going the other way round.
As you can see in most right image above.

Linux worker nodes can as well virtualize VMs because of KVM (Kernel virtualization module).
So with KubeVirt, Kubernetes can as well drive VMs, which brings a great benefit.
- Native `network isolation` and segmentation, managed by Kubernetes
- Shared and redundant and automated `Storage`/Backup/Snapshot with Open Source technologies like
	- CephFS
	- Gluster
	- Longhorn
	- BlockDev
	- ...
OKD/OpenShift with Red Hat did not spend lot of attention to this topic because of the size their projects have.
RedHat speaks of KMUs if they have 600 or less employees.
In Switzerland, we look bit different at that size. 
And it might be a cause too that we still have more money to drive our projects than other countries have.

But others spent a lot of attention to this problem.
Slightly and silent, [Ranger products](https://rancher.com/) found their way to European on-prem Kubernetes cluster setups.

And incredible fast, they started developing a hyperconverged OpenSource VM and Container management platform.
End of Mai 2021, they reached the first beta release target: https://github.com/harvester/harvester/releases

I checked it and it is built very promising and solid:
-   [Raw block device support](https://github.com/rancher/harvester/issues/227)
-   [VM Live Migration](https://github.com/rancher/harvester/issues/384)
-   [VM backup/restore](https://github.com/harvester/harvester/issues/385) can now backup/restore VMs to an S3 or NFS server outside of the cluster
-   [PXE support](https://github.com/rancher/harvester/issues/217)
-   [Zero downtime upgrade](https://github.com/rancher/harvester/issues/383)
-   [Per node NIC configuration](https://github.com/harvester/harvester/issues/369)
-   [Install Rancher with Harvester](https://github.com/rancher/harvester/issues/513)
-   [Provision Kubernetes cluster using Harvester and Rancher](https://github.com/rancher/harvester/issues/512)
-   [Support bundle](https://github.com/rancher/harvester/issues/579)



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgyNjMzNTQ0N119
-->