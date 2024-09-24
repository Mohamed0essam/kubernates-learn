Kubernetes-Learn
This repository contains Kubernetes manifests and steps to deploy an NGINX container and set up Prometheus and Grafana using Helm.

NGINX Deployment
Applied the manifest files to deploy an NGINX container.
Exposed the NGINX service locally using a NodePort service.
Prometheus and Grafana Setup (Using Helm)
Follow these steps to install Prometheus and Grafana:

Add the Helm Repository:
helm repo add -n task prometheus-community https://prometheus-community.github.io/helm-charts

Update the Helm Repositories:
helm repo update -n task

Install the Prometheus Stack:
helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace task

View Installed Resources:
kubectl get all -n task

Retrieve the Grafana Admin Password: You can retrieve the Grafana Admin Password from ArtifactHub by reading the DefaultValues file, or you can run this command:
kubectl get secret --namespace task prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

Access Grafana Locally: Run the following command to port-forward Grafana and access it locally:
kubectl port-forward --namespace task svc/prometheus-stack-grafana 3000:80

Access Prometheus Locally: Similarly, to access Prometheus, run this command:
kubectl port-forward --namespace task svc/prometheus-stack-prometheus-node-exporter 9090:9100
