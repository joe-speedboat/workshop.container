# Kubernetes Operators


# Operator pattern

Operators are software extensions to Kubernetes that make use of [custom resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) to manage applications and their components. Operators follow Kubernetes principles, notably the [control loop](https://kubernetes.io/docs/concepts/architecture/controller).

## Motivation[](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/#motivation)

The Operator pattern aims to capture the key aim of a human operator who is managing a service or set of services. Human operators who look after specific applications and services have deep knowledge of how the system ought to behave, how to deploy it, and how to react if there are problems.

People who run workloads on Kubernetes often like to use automation to take care of repeatable tasks. The Operator pattern captures how you can write code to automate a task beyond what Kubernetes itself provides.

## Operators in Kubernetes[](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/#operators-in-kubernetes)

Kubernetes is designed for automation. Out of the box, you get lots of built-in automation from the core of Kubernetes. You can use Kubernetes to automate deploying and running workloads, _and_ you can automate how Kubernetes does that.

Kubernetes' [controllers](https://kubernetes.io/docs/concepts/architecture/controller/) concept lets you extend the cluster's behaviour without modifying the code of Kubernetes itself. Operators are clients of the Kubernetes API that act as controllers for a [Custom Resource](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)

![enter image description here](https://github.com/joe-speedboat/workshop.docker/raw/main/images/k8s_operator.png)

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
eyJoaXN0b3J5IjpbMTkwMDkyNDMxN119
-->