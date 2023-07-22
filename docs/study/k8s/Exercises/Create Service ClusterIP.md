---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Service ClusterIP.md'
---
# Create Service ClusterIP
Note Created: 2023-02-25

## Lab 

You have a set of Pods that each listen on TCP port 9376 and are labelled as app.kubernetes.io/name=MyApp

## Solution

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app.kubernetes.io/name: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
```
Applying this manifest creates a new Service named "my-service", which targets TCP port 9376 on any Pod with the app.kubernetes.io/name: MyApp label.

We can bind the targetPort of the Service to the Pod port in the following way
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  labels:
    app.kubernetes.io/name: proxy
spec:
  containers:
  - name: nginx
    image: nginx:stable
    ports:
      - containerPort: 80
        name: http-web-svc

---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app.kubernetes.io/name: proxy
  ports:
  - name: name-of-service-port
    protocol: TCP
    port: 80
    targetPort: http-web-svc
```


## Materials
https://kubernetes.io/docs/concepts/services-networking/service/