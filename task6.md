# Ingress

```bash
minikube addons enable ingress
```


```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
kubectl apply -f example2-mongoApp/backend-mongo-db.yaml
kubectl apply -f example2-mongoApp/mongodb-configmap.yaml
kubectl apply -f example2-mongoApp/frontend-mongo-express.yaml
kubectl apply -f example2-mongoApp/ingress.yaml
```

```bash
echo "
```
