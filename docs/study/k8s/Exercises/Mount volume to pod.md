---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Mount volume to pod.md'
---
# Mount volume to pod
Note Created: 2023-02-25

## Lab 

 Create a Pod that uses your PersistentVolumeClaim as a volume
Uses Volume [[Create volumes (pv)]]
Uses PersistentVolumeClaim [[Create volume claim (pvc)]]

## Solution

### Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: task-pv-pod
spec:
  volumes:
    - name: task-pv-storage
      persistentVolumeClaim:
        claimName: task-pv-claim
  containers:
    - name: task-pv-container
      image: nginx
      ports:
        - containerPort: 80
          name: "http-server"
      volumeMounts:
        - mountPath: "/usr/share/nginx/html"
          name: task-pv-storage
```
```console
kubectl apply -f pv-pod.yaml
```

### Check the file in volume
```console
kubectl exec -it task-pv-pod -- /bin/bash
apt update
apt install curl
curl http://localhost/
```

We can check file by curl bc volume is mounted at "/usr/share/nginx/html".

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/

## Lab 

Add emptyDir volume to Pod

## Solution

### Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: registry.k8s.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /cache
      name: cache-volume
  volumes:
  - name: cache-volume
    emptyDir:
      sizeLimit: 500Mi
```
```console
kubectl apply -f pv-pod.yaml
```