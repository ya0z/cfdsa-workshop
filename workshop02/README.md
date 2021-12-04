## Run the following .yaml files:
```
kubectl apply -f bggns.yaml
kubectl apply -n bggns -f bggconfig.yaml
kubectl apply -n bggns -f bggdb.yaml
kubectl apply -n bggns -f bgg-deployment.yaml
```