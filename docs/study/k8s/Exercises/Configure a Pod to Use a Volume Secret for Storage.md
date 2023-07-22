---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Configure a Pod to Use a Volume Secret for Storage.md'
---
# Configure a Pod to Use a Volume Secret for Storage
Note Created: 2023-02-25

## Lab 

Create a Pod which references the secret with the SSH key and consumes it in a volume

## Solution

### Create secret with ssh keys
```console
kubectl create secret generic ssh-key-secret --from-file=ssh-privatekey=/path/to/.ssh/id_rsa --from-file=ssh-publickey=/path/to/.ssh/id_rsa.pub
```
### Create a Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-test-pod
  labels:
    name: secret-test
spec:
  volumes:
  - name: secret-volume
    secret:
      secretName: ssh-key-secret
  containers:
  - name: ssh-test-container
    image: mySshImage
    volumeMounts:
    - name: secret-volume
      readOnly: true
      mountPath: "/etc/secret-volume"
```

## Materials
https://kubernetes.io/docs/concepts/configuration/secret/