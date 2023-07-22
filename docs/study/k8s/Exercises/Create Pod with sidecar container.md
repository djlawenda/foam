---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Pod with sidecar container.md'
---
# Create Pod with sidecar container
Note Created: 2023-02-25

## Lab 

Sidecar containers extend and enhance the "main" container, they take existing containers and make them better.  

As an example, consider a container that runs the Nginx web server.  Add a different container that syncs the file system with a git repository, share the file system between the containers and you have built Git push-to-deploy. 

![Sidecar]([https://](https://d33wubrfki0l68.cloudfront.net/b7b7a33a62a27dead666a7c5ffc61cb89eeecf78/040b2/images/blog/2015-06-00-the-distributed-system-toolkit-patterns/sidecar-containers.png))

## Solution

- the main container, which contains an nginx application that displays a simple HTML page
- a sidecar container, which is a dummy container that simulates an application that extracts logs from the main container and sends it to a centralized aggregator.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp
  labels:
    app: webapp
spec:
  containers:
    - name: main-application
      image: nginx
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
    - name: sidecar-container
      image: busybox
      command: ["sh","-c","while true; do cat /var/log/nginx/access.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
  volumes:
    - name: shared-logs
      emptyDir: {}

---

# Service Configuration
# --------------------
apiVersion: v1
kind: Service
metadata:
  name: simple-webapp
  labels:
    run: simple-webapp
spec:
  ports:
  - port: 80
    protocol: TCP
  selector:
    app: webapp
  type: NodePort
```

## Materials
https://kubernetes.io/blog/2015/06/the-distributed-system-toolkit-patterns/
https://www.containiq.com/post/kubernetes-sidecar-container