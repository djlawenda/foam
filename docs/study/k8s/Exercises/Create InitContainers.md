---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create InitContainers.md'
---
# Create InitContainers
Note Created: 2023-02-25

## Lab 

> A Pod can have multiple containers running apps within it, but it can also have one or more init containers, which are run before the app containers are started.
> Kubelet runs the Pod's init containers in the order they appear in the Pod's spec

This example defines a simple Pod that has two init containers. The first waits for myservice, and the second waits for mydb. Once both init containers complete, the Pod runs the app container from its spec section.

## Solution

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app.kubernetes.io/name: MyApp
spec:
  containers:
  - name: myapp-container
    image: busybox:1.28
    command: ['sh', '-c', 'echo The app is running! && sleep 3600']
  initContainers:
  - name: init-myservice
    image: busybox:1.28
    command: ['sh', '-c', "until nslookup myservice.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for myservice; sleep 2; done"]
  - name: init-mydb
    image: busybox:1.28
    command: ['sh', '-c', "until nslookup mydb.$(cat /var/run/secrets/kubernetes.io/serviceaccount/namespace).svc.cluster.local; do echo waiting for mydb; sleep 2; done"]
```
At this stage pod myapp-pod is waiting for initcontainers to complete. They will complete if they are able to find services: myservice and mydb.

| NAME    |    READY  |   STATUS  |   RESTARTS | AGE |
|---------|---------|---------|---------|---------|
| myapp-pod |  0/1   |    Init:0/2 |  0    |      6m|

Create services
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myservice
spec:
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9376
---
apiVersion: v1
kind: Service
metadata:
  name: mydb
spec:
  ports:
  - protocol: TCP
    port: 80
    targetPort: 9377
```
Once services are created, initcontainers can complete and pod has status Running.

| NAME    |    READY  |   STATUS  |   RESTARTS | AGE |
|---------|---------|---------|---------|---------|
| myapp-pod |  1/1   |    Running |  0    |      6m|

## Materials
https://kubernetes.io/docs/concepts/workloads/pods/init-containers/

## Lab

 Create a Pod that has one application Container and one Init Container. The init container runs to completion before the application container starts.

## Solution

- The Pod has a Volume that the init container and the application container share.
- The init container mounts the shared Volume at /work-dir
- The init container runs the following command and then terminates `wget -O /work-dir/index.html http://info.cern.ch`
- The application container mounts the shared Volume at /usr/share/nginx/html

Create Pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-demo
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80
    volumeMounts:
    - name: workdir
      mountPath: /usr/share/nginx/html
  # These containers are run during pod initialization
  initContainers:
  - name: install
    image: busybox:1.28
    command:
    - wget
    - "-O"
    - "/work-dir/index.html"
    - http://info.cern.ch
    volumeMounts:
    - name: workdir
      mountPath: "/work-dir"
  dnsPolicy: Default
  volumes:
  - name: workdir
    emptyDir: {}
```
```console
kubectl apply -f init-containers.yaml
kubectl get pod init-demo
kubectl exec -it init-demo -- /bin/bash
root@nginx:~# apt-get update
root@nginx:~# apt-get install curl
root@nginx:~# curl localhost
```
The output shows that nginx is serving the web page that was written by the init container

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/