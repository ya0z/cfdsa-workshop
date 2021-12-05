### Create `wordpress` namespace
```
kubectl create ns wordpress
```
### Deploy wordpress using Kustomize
```
kubectl apply -n wordpress -k ./
```