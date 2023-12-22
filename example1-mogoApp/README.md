# Example one
Frontend: Mongo-Express
Backend: Mongo-DB

# Setting secrets
Create two secrets:
- mongo-username
- mongo-password
  
```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```

```bash
kubectl create deployment -f example1-mogoApp/backend-mongo-db.yaml
```

