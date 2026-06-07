# Hands-On - Exercise 02 - my first ReplicaSet and Service

  - Create a three replicatset to pod from exercise-01
  - Get the number of replicasets
  - Get all the info of replicasets
  - Change the number of rs from 3 to 2
  - Create a service to the my-first-pod pod from exercise-01

## Solution via one yaml file
```
kubectl apply -f my-first-replicaset.yaml

  # Cleanup if needed - First command delete pod and rs, second the svc, it will take after few min to see it deleted

kubectl delete all --all     

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
