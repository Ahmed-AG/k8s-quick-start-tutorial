# Task 5: Namespaces
`Namespaces` are a way to divide cluster resources between multiple users, teams, or projects. They provide a scope for Kubernetes objects, such as pods, services, and replication controllers, within a cluster.

Namespaces are useful for organizing and isolating resources, allowing different teams or projects to operate independently within the same Kubernetes cluster without interfering with each other. They help in avoiding naming collisions and provide a level of resource isolation and security.

By default, Kubernetes has a 'default' namespace, but you can create multiple namespaces to logically segregate and manage your resources more effectively. Each namespace operates as a separate virtual cluster within the larger Kubernetes cluster, enabling teams to work in their dedicated space without conflicting with others.

To explore namespaces run the following:
```bash
kubectl get namespaces
```
```
$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   17h
kube-node-lease   Active   17h
kube-public       Active   17h
kube-system       Active   17h
```
Notice that there is a `default` namespace. This is where we created all of our resources so far.
Run the following command to view all resources in the default namespace:

```bash
kubectl get all -n default
```

## Blue/Green Deployment
There are many way for us to use namespaces, we can specify the namespace inside YAML configuration file itself under `metadata`:
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-mongodb-deployment
  namespace: my-awesome-namespace
  labels:
    app: backend-mongodb
```

Or we can pass the namespace as a parameter when we apply a configuration file: `kubectl apply -f <file.yaml> --namespace my-awesome-namespace`.
For our example, we will use Namespaces to deploy two versions of our application. a Blue one and a Green one. Assuming that we will use deployment piplines to deploy these, it makes sense for us to use the command line option.

Let us first clean up the previous deployments we have:
```bash
kubectl delete -f example1-mongoApp/backend-mongo-db.yaml
kubectl delete -f example1-mongoApp/mongodb-configmap.yaml
kubectl delete -f example1-mongoApp/frontend-mongo-express.yaml
kubectl delete secret mongodb-secret
```
Verify your work by running:
```bash
kubectl get all
```
Now that we have a clean slate, let us create our two namespaces:
```bash
kubectl create namespace blue
kubectl create namespace green
```
Let us deploy our `Blue` deployment first:
```bash
deployment=blue
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $deployment
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/frontend-mongo-express.yaml --namespace $deployment
```

Notice that we are using the `$deployment` variable to simulate what we would do in a deployment pipeline.
Let us check out our work:
```bash
kubectl get all
```
The above command should not show our resources. But the next one should:
```bash
kubectl get all -n blue
```

Let us expose that. If we run `minikube service frontend-mongo-express`, we should see the following error:
```bash
$ minikube service frontend-mongo-express

❌  Exiting due to SVC_NOT_FOUND: Service 'frontend-mongo-express' was not found in 'default' namespace.
You may select another namespace by using 'minikube service frontend-mongo-express -n <namespace>'. Or list out all the services using 'minikube service list'
```
So let us specify the namespace:
```bash
minikube service frontend-mongo-express -n blue
```
Great! We have our blue deployment up and running!
Let us create the green deployment:
```bash
deployment=green
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $deployment
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/frontend-mongo-express.yaml --namespace $deployment
sleep 60
minikube service frontend-mongo-express -n $deployment
```
OOPS! We need to change the port!
```
The Service "frontend-mongo-express" is invalid: spec.ports[0].nodePort: Invalid value: 30000: provided port is already allocated

❌  Exiting due to SVC_NOT_FOUND: Service 'frontend-mongo-express' was not found in 'green' namespace.
You may select another namespace by using 'minikube service frontend-mongo-express -n <namespace>'. Or list out all the services using 'minikube service list'
```
To fix that, we can create another version of `example1-mongoApp/frontend-mongo-express.yaml` with a different port. We have created one that has `nodePort: 3001` located in `example1-mongoApp/frontend-mongo-express-green.yaml`. Let us try again using the green version:
```bash
deployment=green
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $deployment
kubectl apply -f example1-mongoApp/backend-mongo-db.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/mongodb-configmap.yaml --namespace $deployment
kubectl apply -f example1-mongoApp/frontend-mongo-express-green.yaml --namespace $deployment
sleep 60
minikube service frontend-mongo-express -n $deployment
```
To verify your work you can use your browser or run:
```bash
kubectl get services -n blue
kubectl get services -n green
```
```
$ kubectl get services -n blue
NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
backend-mongodb          ClusterIP      10.104.133.115   <none>        27017/TCP        19h
frontend-mongo-express   LoadBalancer   10.102.67.181    <pending>     8081:30000/TCP   19h
$ kubectl get services -n green
NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
backend-mongodb          ClusterIP      10.96.81.254     <none>        27017/TCP        19h
frontend-mongo-express   LoadBalancer   10.111.153.234   <pending>     8081:30001/TCP   8m16s
```

Nice! Now you have two versions running on different ports! But that is not the best way to do that! A better way would be to use a placeholder with `sed` to dynamically set the `nodePort`. The other option is to use [HELM Charts](https://helm.sh/docs/topics/charts/). We will cover HELM in a later task.

## Cleanup
```bash
deployment=blue
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $deployment
kubectl delete -f example1-mongoApp/backend-mongo-db.yaml --namespace $deployment
kubectl delete -f example1-mongoApp/mongodb-configmap.yaml --namespace $deployment
kubectl delete -f example1-mongoApp/frontend-mongo-express.yaml --namespace $deployment
```

```bash
deployment=green
kubectl create secret generic mongodb-secret --from-literal=mongo-username=mongouser --from-literal=mongo-password=mongopass --namespace $deployment
kubectl delete -f example1-mongoApp/backend-mongo-db.yaml --namespace $deployment
kubectl delete -f example1-mongoApp/mongodb-configmap.yaml --namespace $deployment
kubectl delete -f example1-mongoApp/frontend-mongo-express.yaml --namespace $deployment
```
