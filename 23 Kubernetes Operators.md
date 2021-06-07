# Kubernetes Operators

A [Kubernetes operator](https://www.redhat.com/en/resources/oreilly-kubernetes-operators-automation-ebook?intcmp=701f2000001OMH6AAO) is a method of packaging, deploying, and managing a Kubernetes application. A Kubernetes application is both deployed on [Kubernetes](https://www.redhat.com/en/topics/containers/what-is-kubernetes) and managed using the Kubernetes API (application programming interface) and kubectl tooling.

A Kubernetes operator is an application-specific controller that extends the functionality of the Kubernetes API to create, configure, and manage instances of complex applications on behalf of a Kubernetes user.

It builds upon the basic Kubernetes resource and controller concepts, but includes domain or application-specific knowledge to automate the entire life cycle of the software it manages.

In Kubernetes, controllers of the control plane implement control loops that repeatedly compare the desired state of the cluster to its actual state. If the cluster's actual state doesn’t match the desired state, then the controller takes action to fix the problem.

An operator is a custom Kubernetes controller that uses custom resources (CR) to manage applications and their components. High-level configuration and settings are provided by the user within a CR. The Kubernetes operator translates the high-level directives into the low level actions, based on best practices embedded within the operator’s logic.

A custom resource is the [API](https://www.redhat.com/en/topics/api) extension mechanism in Kubernetes. A custom resource definition (CRD) defines a CR and lists out all of the configuration available to users of the operator.

The Kubernetes operator watches a CR type and takes application-specific actions to make the current state match the desired state in that resource.

Kubernetes operators introduce new object types through custom resource definitions. Custom resource definitions can be handled by the Kubernetes API just like built-in objects, including interaction via kubectl and inclusion in role-based access control (RBAC) policies.

A Kubernetes operator continues to monitor its application as it runs, and can back up data, recover from failures, and upgrade the application over time, automatically.

The actions a Kubernetes operator performs can include almost anything: scaling a complex app, application version upgrades, or even managing kernel modules for nodes in a computational cluster with specialized hardware.

Kubernetes operators are a big step into this direction, since the migration of Docker applications into new versions needed often some attention. Operators are containerized system administrators that maintain a kind of workload.
This might be `prometheus` (which initially developed the operator concept).
`AWX` which is the OpenSource Version of the Ansible Tower.

Operators are the answer to missing kubernetes know-how and the leak of system administrators.

If you look into a running OpenShift cluster you can get an idea of where we will end:
```
[chris@control(wiki/system:admin) ~]☯ oc get clusteroperators.config.openshift.io
NAME                                       VERSION                         AVAILABLE   PROGRESSING   DEGRADED   SINCE
authentication                             4.7.0-0.okd-2021-05-22-050008   True        False         False      13h
baremetal                                  4.7.0-0.okd-2021-05-22-050008   True        False         False      95d
cloud-credential                           4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
cluster-autoscaler                         4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
config-operator                            4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
console                                    4.7.0-0.okd-2021-05-22-050008   True        False         False      9d
csi-snapshot-controller                    4.7.0-0.okd-2021-05-22-050008   True        False         False      17h
dns                                        4.7.0-0.okd-2021-05-22-050008   True        False         False      11d
etcd                                       4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
image-registry                             4.7.0-0.okd-2021-05-22-050008   True        False         False      9d
ingress                                    4.7.0-0.okd-2021-05-22-050008   True        False         False      117d
insights                                   4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
kube-apiserver                             4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
kube-controller-manager                    4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
kube-scheduler                             4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
kube-storage-version-migrator              4.7.0-0.okd-2021-05-22-050008   True        False         False      9h
machine-api                                4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
machine-approver                           4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
machine-config                             4.7.0-0.okd-2021-05-22-050008   True        False         False      15h
marketplace                                4.7.0-0.okd-2021-05-22-050008   True        False         False      9d
monitoring                                 4.7.0-0.okd-2021-05-22-050008   True        False         False      13h
network                                    4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
node-tuning                                4.7.0-0.okd-2021-05-22-050008   True        False         False      9d
openshift-apiserver                        4.7.0-0.okd-2021-05-22-050008   True        False         False      9h
openshift-controller-manager               4.7.0-0.okd-2021-05-22-050008   True        False         False      6d4h
openshift-samples                          4.7.0-0.okd-2021-05-22-050008   True        False         False      9d
operator-lifecycle-manager                 4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
operator-lifecycle-manager-catalog         4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
operator-lifecycle-manager-packageserver   4.7.0-0.okd-2021-05-22-050008   True        False         False      26h
service-ca                                 4.7.0-0.okd-2021-05-22-050008   True        False         False      283d
storage                                    4.7.0-0.okd-2021-05-22-050008   True        False         False      171d
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE2MTMwOTk4NzIsMTIzOTE2NjM4MF19
-->