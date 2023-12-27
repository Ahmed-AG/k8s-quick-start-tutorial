# Lab 3: Create the backend

The full configuration file is [here](./example1-mongoApp/backend-mongo-db.yaml). But let us disect it.
This file will create two resources:
- A `Deployment` for the backend
- A `Service` for that backend

## Backend Deployment

First we need to configure the resource Type and some Metadata
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-mongodb-deployment
  labels:
    app: backend-mongodb
```

Above sets a name for this deployment and also a label that will be used to reference this deployment later on.
Next,  we need to set some specifications:
```
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend-mongodb
  template:
    metadata:
      labels:
        app: backend-mongodb
```
In the above code we set the replicas to `1` because we need one Pod. and we also set the selector to select the label `app: backend-mongodb`

Next, we need to set the container specification. We have an `Container Image` that is already configured with MongoDB. We will se that, and we will also set the default port.
```
    spec:
      containers:
      - name: backend-mongodb
        image: mongo
        ports:
        - containerPort: 27017
```
The Next step is for us to configure the username and password for the Database. We can do that by setting the envrinoemnt variables `MONGO_INITDB_ROOT_USERNAME` and `MONGO_INITDB_ROOT_PASSWORD` inside the container. The values of those are being referenced from the `mongodb-secret` secret we set earlier.

```
        env:
        - name: MONGO_INITDB_ROOT_USERNAME
          valueFrom:
            secretKeyRef:
              name: mongodb-secret
              key: mongo-username
        - name: MONGO_INITDB_ROOT_PASSWORD
          valueFrom: 
            secretKeyRef:
              name: mongodb-secret
              key: mongo-passwor
```
## Creating the service
Finally, we are going to create service and tie it to the deployment we just created:
```
apiVersion: v1
kind: Service
metadata:
  name: backend-mongodb
spec:
  selector:
    app: backend-mongodb
  ports:
    - protocol: TCP
      port: 27017
      targetPort: 27017
```

Notice that we used the `app: backend-mongodb` as a selector and we exposed the same port `27017`. Notice also that we dont have anything that dictates wether we should expose access to this service externally. The default is that we will not.

## Apply the Backend

```bash
kubectl apply -f example1-mogoApp/backend-mongo-db.yaml
```