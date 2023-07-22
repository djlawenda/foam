---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create volume claim (pvc).md'
---
# Create volume claim (pvc)
Note Created: 2023-02-25

## Lab 

Pods use PersistentVolumeClaims to request physical storage. In this exercise, you create a PersistentVolumeClaim that requests a volume of at least three gibibytes that can provide read-write access for at least one Node.

Uses the volume from [[Create volumes (pv)]]

## Solution

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: task-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 3Gi
```
```console
kubectl apply -f pv-claim.yaml
kubectl get pvc task-pv-claim
```
NAME            STATUS    VOLUME           CAPACITY   ACCESSMODES   STORAGECLASS   AGE
task-pv-claim   Bound     task-pv-volume   10Gi       RWO           manual         30s

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/