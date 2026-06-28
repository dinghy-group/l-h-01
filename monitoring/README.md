# Deploying Prometheus on Kubernetes using KIND

- Check installation of kind,Create a new KIND cluster, and check it :​

```
kind version​
kind create cluster --name prometheus-cluster​
kubectl cluster-info --context kind-prometheus-cluster​
kubectl config get-contexts
kubectl get ns
kubectl get nodes​
```

## Install Prometheus using Helm

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts​
helm repo update​
helm install prometheus prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace​
kubectl config set-context --current --namespace=monitoring
kubectl get ns
kubectl config get-contexts
```
 - port-forward​ 
```
kubectl port-forward svc/prometheus-kube-prometheus-prometheus 9090 -n monitoring​
```
- Go to Browser and execute PromQL queries http://localhost:9090​

## Prometheus Service Discovery
- Run the –it ( Interactive mode )​ In order to view on Kubernetes Job Configuration in prometheus.yml​

```
kubectl get endpoints -n monitoring
kubectl get pods -n monitoring​
kubectl get svc -n monitoring​
docker ps​
kubectl get deployments -n monitoring​
helm list -n monitoring​
kubectl get pods -n monitoring | grep prometheus​
kubectl exec -n monitoring -it prometheus-prometheus-kube-prometheus-prometheus-0 -- sh -c "cat /etc/prometheus/prometheus.yml"​
kubectl get endpoints -n monitoring​
```

  - Prometheus UI: http://localhost:9090/targets
### Access Grafana​

```
  # Check the pod of grafana​
kubectl get pods -n monitoring​
  #Check the service of grafana​
kubectl get svc -n monitoring​
```

- port-forward: Redirect to port 3000​
  
```
kubectl port-forward svc/prometheus-grafana 3000:80 -n monitoring​
```
- Browser to grafana UI
```
http://127.0.0.1:3000
 # Generated the password
kubectl get secret prometheus-grafana -n monitoring -o jsonpath="{.data.admin-password}" | base64 --decode
```
