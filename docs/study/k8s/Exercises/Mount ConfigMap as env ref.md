---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Mount ConfigMap as env ref.md'
---
# Mount ConfigMap as env ref
Note Created: 2023-02-25

## Lab 

Define a container environment variable with data from a single ConfigMap

## Solution

Create ConfigMap
```console
kubectl create configmap special-config --from-literal=special.how=very
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
      command: [ "/bin/sh", "-c", "env" ]
      env:
        # Define the environment variable
        - name: SPECIAL_LEVEL_KEY
          valueFrom:
            configMapKeyRef:
              # The ConfigMap containing the value you want to assign to SPECIAL_LEVEL_KEY
              name: special-config
              # Specify the key associated with the value
              key: special.how
  restartPolicy: Never
```
```console
kubectl create -f pod-single-configmap-env-variable.yaml
```

## Lab 

Define container environment variables with data from multiple ConfigMaps

## Solution

Create 2 ConfigMaps

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: special-config
  namespace: default
data:
  special.how: very
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: env-config
  namespace: default
data:
  log_level: INFO
```
```console
kubectl create -f configmaps.yaml
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
      command: [ "/bin/sh", "-c", "env" ]
      env:
        - name: SPECIAL_LEVEL_KEY
          valueFrom:
            configMapKeyRef:
              name: special-config
              key: special.how
        - name: LOG_LEVEL
          valueFrom:
            configMapKeyRef:
              name: env-config
              key: log_level
  restartPolicy: Never
```
```console
kubectl create -f pod-multiple-configmap-env-variable.yaml
```

## Lab

Configure all key-value pairs in a ConfigMap as container environment variables

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
      command: [ "/bin/sh", "-c", "env" ]
      envFrom:
      - configMapRef:
          name: special-config
  restartPolicy: Never
```
```console
kubectl create -f pod-configmap-envFrom.yaml
```


## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/