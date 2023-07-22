---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Configure a Pod to Use a Volume emptyDir for Storage.md'
---
# Configure a Pod to Use a Volume emptyDir for Storage
Note Created: 2023-02-25

## Lab 

Create a Pod that runs one Container. This Pod has a Volume of type emptyDir that lasts for the life of the Pod, even if the Container terminates and restarts.

## Solution

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: redis
spec:
  containers:
  - name: redis
    image: redis
    volumeMounts:
    - name: redis-storage
      mountPath: /data/redis
  volumes:
  - name: redis-storage
    emptyDir: {}
```
```console
kubectl apply -f redis.yaml
kubectl get pod redis --watch
```

Switch to another terminal, get shell of container and create file in `/data/redis/`
```console
kubectl exec -it redis -- /bin/bash
root@redis:/data# cd /data/redis/
root@redis:/data/redis# echo Hello > test-file
```

In the container shell kill the redis process to kill container
```console
root@redis:/data/redis# apt-get update
root@redis:/data/redis# apt-get install procps
root@redis:/data/redis# ps aux
root@redis:/data/redis# kill < pid> #<pid> is the Redis process ID (PID)
```
At this point, the Container has terminated and restarted. This is because the Redis Pod has a restartPolicy of Always.

Get a shell into the restarted Container and check file in `/data/redis/`
```console
kubectl exec -it redis -- /bin/bash
root@redis:/data/redis# cd /data/redis/
root@redis:/data/redis# ls
test-file
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-volume-storage/