---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Use container logs.md'
---
# Use container logs
Note Created: 2023-02-26

## Lab 

View each container log.
[[Save pod logs to file]]

## Solution

- create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secondapp
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: busy
    image: busybox
    command:
      - sleep
      - "3600"
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```

- View Pod logs
```console
kubectl describe pod secondapp
kubectl logs secondapp
```

## Materials
LFD259 exercise 8.1