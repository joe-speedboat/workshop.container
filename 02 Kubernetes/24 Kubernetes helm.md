# Helm charts
Helm is a tool for managing Kubernetes packages called _charts_. Helm can do the following:

-   Create new charts from scratch
-   Package charts into chart archive (tgz) files
-   Interact with chart repositories where charts are stored
-   Install and uninstall charts into an existing Kubernetes cluster
-   Manage the release cycle of charts that have been installed with Helm

For Helm, there are three important concepts:

1.  The _chart_ is a bundle of information necessary to create an instance of a Kubernetes application.
2.  The _config_ contains configuration information that can be merged into a packaged chart to create a releasable object.
3.  A _release_ is a running instance of a _chart_, combined with a specific _config_.

## Deploy a sample application with helm

```bash
kubectl create namespace zammad

kubectl config set-context --current --namespace=zammad

helm repo add zammad https://zammad.github.io/zammad-helm

export KUBECONFIG=/etc/rancher/k3s/k3s.yaml # for K3S

helm upgrade --install zammad zammad/zammad --namespace zammad

kubectl get all
```
That's all.

## Create ingress routing
Since we don't want to run the application on port `8080` as it comes with helm, we have to rewire the web service.
```bash
kubectl get svc

kubectl delete svc zammad

kubectl expose pod/zammad-0 --port=8080 --name=zammad

kubectl create ingress ingress-www --rule=zammad.vm20.test.domain.ch/*=zammad:8080
```
Please replace the fqdn depending on your needs.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU5ODk1OTkyMV19
-->