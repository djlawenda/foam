---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Mount ConfigMap as volume.md'
---
# Mount ConfigMap as volume
Note Created: 2023-02-25

## Lab 

Add the ConfigMap name under the volumes section of the Pod specification

## Solution

Create ConfigMap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: special-config
  namespace: default
data:
  SPECIAL_LEVEL: very
  SPECIAL_TYPE: charm
```
```console
kubectl create -f configmap-multikeys.yaml
```

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: dapi-test-pod
spec:
  containers:
    - name: test-container
      image: registry.k8s.io/busybox
      command: [ "/bin/sh", "-c", "ls /etc/config/" ]
      volumeMounts:
      - name: config-volume
        mountPath: /etc/config
  volumes:
    - name: config-volume
      configMap:
        # Provide the name of the ConfigMap containing the files you want
        # to add to the container
        name: special-config
  restartPolicy: Never
```
```console
kubectl create -f pod-configmap-volume.yaml
ls /etc/config/
```
SPECIAL_LEVEL
SPECIAL_TYPE

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/