---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create YAML manifest quickly (pod, deploy, service, job).md'
---
# Create YAML manifest quickly (pod, deploy, service, job)
Note Created: 2023-02-26

## Lab 

- Create a pod YAML named myapp which uses image nginx:latest.
```console
kubectl run mypod --image=nginx:latest --dry-run=client -o yaml > mypod.yaml
```
- Create a NodePort service YAML for running Pod
```console
kubectl expose pod mypod \
    --port=80 \
    --name mypod-service \
    --type=NodePort \
    --dry-run=client -o yaml > mypod-service.yaml
```
- Create a service type nodeport with port 30001 with service to pod TCP port mapping on port 80
```console
kubectl create service nodeport mypod \
    --tcp=80:80 \
    --node-port=30001 \
    --dry-run=client -o yaml > mypod-service.yaml
```
- Create Deployment YAML
```console
kubectl create deployment mydeployment \
    --image=nginx:latest \
    --dry-run=client -o yaml > mydeployment.yaml
```
- Create a NodePort service YAML for existing Deployment
```console
kubectl expose deployment mydeployment \
    --type=NodePort \
    --port=8080 \
    --name=mydeployment-service \
    --dry-run=client -o yaml > mydeployment-service.yaml
```
- Crate job named myjob with nginx image
```console
kubectl create job myjob \
    --image=nginx:latest \
    --dry-run=client -o yaml > myjob.yaml
```
- Create a cronjob named mycronjob with nginx image and a corn schedule
```console
kubectl create cj mycronjob \
    --image=nginx:latest \
    --schedule="* * * * *" \
    --dry-run=client -o yaml > mycronjob.yaml
```

## Materials
https://devopscube.com/create-kubernetes-yaml/