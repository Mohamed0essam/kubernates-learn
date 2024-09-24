# kubernates-learn
- i applyed those manifest files to install nginx container and expose it localy using nodeport service 
- then i installed prometheus and grafana using helm by applying those steps:
1: helm repo add -n task prometheus-community https://prometheus-community.github.io/helm-charts
2: helm repo update -n task
3: helm install prometheus-stack prometheus-community/kube-prometheus-stack --namespace task
4: then we can view the installed resources by using: kubectl get all -n task
5: i can view the Grafana Admin Password by accessing the ArtifactHub and read the DefaultValues file or i can just simply write : kubectl get secret --namespace task prometheus-stack-grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
6: then to access grafana service localy i run this command : kubectl port-forward --namespace task svc/prometheus-stack-grafana 3000:80
7: the same thing while accessing prometheus : kubectl port-forward --namespace task svc/prometheus-stack-prometheus-node-exporter 9090:9100
