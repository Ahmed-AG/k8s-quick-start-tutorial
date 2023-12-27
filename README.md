# k8s-quick-start-tutorial

Welcome to this quick start tutorial about Kubertenes (k8s).

# Learning Example: Building a Frontend and Backend sample application 
## Detailed Track:

Follow the following labs to build the application:
- [Lab 0](./lab0.md)
- [Lab 1](./lab1.md)
- [Lab 2](./lab2.md)
- [Lab 3](./lab3.md)
- [Lab 4](./lab4.md)

## Fast Track:
Given that you have a K8s envinroment set, these are the commands needed to build the entire application:
### Create the secret (DB Username and Password)
```bash
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass
```
### Create Backend, ConfigMap and FrontEnd
```bash
kubectl apply -f example1-mogoApp/backend-mongo-db.yaml
kubectl apply -f example1-mogoApp/mongodb-configmap.yaml
kubectl apply -f example1-mogoApp/frontend-mongo-express.yaml
```
### Expose the Frontend Service
```bash
minikube service frontend-mongo-express
```
# Cleanup 

```bash
minikube delete
```
