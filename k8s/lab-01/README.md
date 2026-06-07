# Create your first Cluster

```
kind create cluster --name kind-01 --config kind-config.yaml

kubectl config get-contexts | awk '{print $1,"        "$5 }'
kind get clusters
```

## Hands-On  - Exercise 01 - my first Pod
  - Create namespace with name ns-my-first-pod based on exist cluster​
  - Create yaml file  my-first-pod.yaml based on image latest of nginx​
  - Apply the pod​ to the namespace ns-my-first-pod
  - Check that the pod is running correctly under test ns  
    

### Solution  - Lab 01

```
kubectl get pod
kubectl get ns
```
```
 
cat << EOF > ~/ns-my-first-pod.yaml 
apiVersion: v1
kind: Namespace
metadata:
  name: test
EOF

```
 ### Check namespace
```
kubectl config set-context --current --namespace=test
kubectl get ns
kind get clusters
kubectl config get-contexts
kubectl config get-contexts | awk '{print $1,$5}'

```
### Create the first pod
```
kubectl apply -f my-first-pod.yaml​
kubectl get pod

```
