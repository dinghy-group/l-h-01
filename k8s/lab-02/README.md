# Hands-On - Exercise 02 - my first ReplicaSet and Service

  - Create a three replicatset to pod from exercise-01
  - Get the number of replicasets
  - Get all the info of replicasets
  - Change the number of rs from 3 to 2
  - Create a service to the my-first-pod pod from exercise-01

## Solution via one yaml file
```
kubectl apply -f my-pod-rs-svc.yaml
kubectl port-forward svc/example-service 8080:80

  # Cleanup if needed - First command delete pod and rs, second the svc, it will take after few min to see it deleted

kubectl delete all --all     
kubectl delete svc --all
kubectl delete configmap --all
kubectl delete secret --all
kubectl delete pvc --all
kubectl delete ingress --all
```
## Solution via separate yaml files

  - Create ReplicaSets (rs)

```
kubectl get pods
kubectl get replicasets
kubectl apply -f my-first-replicaset.yaml
kubectl get pods
kubectl get rs
kubectl describe rs
kubectl edit rs example-replicaset
# or
kubectl scale --replicas=2 rs/example-replicaset

  # Change the number of rs from 3 to 2 and save the file
kubectl get rs
  # You should see 2 rs that up and running
```

  - Number of replicasets after apply
![Alt text](after-replicaset.png)
![Alt text](after-replicaset-pod-command.png)

  - Create Service (svc)
```
kubectl get svc
kubectl apply -f my-first-svc.yaml
kubectl get svc
kubectl get pods
kubectl get replicasets
kubectl port-forward svc/example-service 8080:80
```

  - Go to the browser http://localhost:8080/

![Alt text](login-nginx.png)


