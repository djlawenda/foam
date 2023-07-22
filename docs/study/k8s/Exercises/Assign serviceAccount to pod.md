---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Assign serviceAccount to pod.md'
---
# Assign serviceAccount to pod
Note Created: 2023-02-25

## Lab 

A service account provides an identity for processes that run in a Pod, and maps to a ServiceAccount object. When you authenticate to the API server, you identify yourself as a particular user. Kubernetes recognises the concept of a user, however, Kubernetes itself does not have a User API.

This task guide is about ServiceAccounts, which do exist in the Kubernetes API. The guide shows you some ways to configure ServiceAccounts for Pods.

## Solution

When Pods contact the API server, Pods authenticate as a particular ServiceAccount (for example, default). There is always at least one ServiceAccount in each namespace.

### Fetch the details for a Pod
```console
kubectl get pods/<podname> -o yaml
```

see a field `spec.serviceAccountName`


### Check available ServiceAccount
```console
kubectl get serviceaccounts
```
NAME      SECRETS    AGE
default   1          1d

### Create ServiceAccount
[[Create serviceAccount]]

### Launch a Pod using service account
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  serviceAccountName: build-robot
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/