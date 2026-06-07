# Create your first Cluster

```
kind create cluster --name kind-01 --config kind-config.yaml

kubectl config get-contexts | awk '{print $1,"        "$5 }'
kind get clusters
```
