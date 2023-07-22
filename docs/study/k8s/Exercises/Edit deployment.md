---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Edit deployment.md'
---
# Edit deployment
Note Created: 2023-02-25

## Lab 

Update the deployment by applying a new YAML file

## Solution

Generate YAML from running deployment
```console
kubectl get deploy nginx-deployment -o yaml > deployment-update.yaml
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.16.1 # Update the version of nginx from 1.14.2 to 1.16.1
        ports:
        - containerPort: 80
```
Apply the new YAML file
```console
kubectl apply -f deployment-update.yaml
```

## Materials
https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/