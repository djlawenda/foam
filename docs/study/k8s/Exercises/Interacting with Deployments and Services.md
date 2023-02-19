---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Interacting with Deployments and Services.md'
---
# Interacting with Deployments and Services
Note Created: 2023-02-19

## Lab 

1. dump Pod logs for a Deployment
2. dump Pod logs for a Deployment (multi-container case)
3. listen on local port 5000 and forward to port 5000 on Service backend
4. listen on local port 5000 and forward to Service target port with name <my-service-port>

## Solution

1. kubectl logs deploy/my-deployment  
2. kubectl logs deploy/my-deployment -c my-container
3. kubectl port-forward svc/my-service 5000
4. kubectl port-forward svc/my-service 5000:my-service-port

## Materials