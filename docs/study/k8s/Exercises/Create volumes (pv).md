---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create volumes (pv).md'
---
# Create volumes (pv)
Note Created: 2023-02-25

## Lab 

Create a hostPath PersistentVolume backed by physical storage

## Solution

Create a folder\file on node and use it as a volume
```console
sudo mkdir /mnt/data
sudo sh -c "echo 'Hello from Kubernetes storage' > /mnt/data/index.html"
cat /mnt/data/index.html
Hello from Kubernetes storage
```
Create a PersistentVolume
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: task-pv-volume
  labels:
    type: local
spec:
  storageClassName: manual
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/mnt/data"
```
`kubectl apply -f pv-volume.yaml`

`kubectl get pv task-pv-volume`

NAME             CAPACITY   ACCESSMODES   RECLAIMPOLICY   STATUS      CLAIM     STORAGECLASS   REASON    AGE
task-pv-volume   10Gi       RWO           Retain          Available             manual                   4s

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/