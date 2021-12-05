### Install metrics-server
```
kubectl apply -f metrics-server.yaml -n kube-system
```
### Install Ingress Nginx controller
Create ingress-nginx namespace
```
kubectl create ns ingress-nginx
```
Install using Helm chart.
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm install ingress-nginx ingress-nginx/ingress-nginx -n ingress-nginx
```
### Create `bggns` namespace
```
kubectl create ns bggns
```
### Provision a Persistent Volume Claim (PVC)
```
kubectl apply -f persist_vol.yaml -n bggns
```
### Deploy the database with the PVC
```
kubectl apply -f bggdb.yaml -n bggns
```
### Deploy the v1 and v2 of `stackupiss/bgg-backend`
```
kubectl apply -f bggconfig.yaml -n bggns
kubectl apply -f bggapp-v1.yaml -n bggns
kubectl apply -f bggapp-v2.yaml -n bggns
```
### Deploy the Nginx Ingress to route to the respective version of the deployed apps
Determine the external IP for the Ingress Nginx controller
```
kubectl -n bggns get all
```
You will see something like the following:

`service/ingress-nginx-controller             LoadBalancer   10.245.52.75     `**137.184.250.170**`   80:31953/TCP, 443:31714/TCP`

Change the host in the file to the hostname like the following: `bgg-137.184.250.170.nip.io`

Then deploy the Ingress Nginx:
```
kubectl apply -f bgg-ing.yaml -n bggns
```
### Deploy horizontal scaling for both app deployment
```
kubectl apply -f hpa-scaling.yaml -n bggns
```
