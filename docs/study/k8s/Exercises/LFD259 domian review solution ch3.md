---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch3.md'
---
# LFD259 domian review solution ch3
Note Created: 2023-02-26

## Lab 

> Deploy a new nginx webserver. Add a LivenessProbe and a ReadinessProbe on port 80. Test that both probes and the webserver work.

Create YAML
```console
k create deploy new-deploy --dry-run=client --image=nginx -o yaml > new-deploy.yaml
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: new-deploy
  name: new-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: new-deploy
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: new-deploy
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
status: {}
```
Add ReadinessProbe and LivenessProbe
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: new-deploy
  name: new-deploy
spec:
  replicas: 1
  selector:
    matchLabels:
      app: new-deploy
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: new-deploy
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
        readinessProbe: # here
          tcpSocket:
            port: 80
          initialDelaySeconds: 5
          periodSeconds: 10
        livenessProbe: # here
          tcpSocket:
            port: 80
          initialDelaySeconds: 15
          periodSeconds: 20
status: {}
```

> Use the `build-review1.yaml` file to create a non-working deployment. Fix the deployment such that both containers are running and in a READY state. The web server listens on port 80, and the proxy listens on port 8080.
LivenessProbe and ReadinessProbe were set for port 808 instead of 8080 or 80.

> View the default page of the web server. When successful verify the GET activity logs in the container log. The message should look something like the following. Your time and IP may be different.
```console
192.168.124.0 - - [30/Jan/2020:03:30:31 +0000] "GET / HTTP/1.1" 200 612 "-" "curl/7.58.0" "-"
```

```console
k describe po break2
# get pod IP
curl IP
# check pod logs
k logs break2
```
192.168.0.0 - - [26/Feb/2023:14:14:22 +0000] "GET / HTTP/1.1" 200 615 "-" "curl/7.68.0" "-"

> Delete any resources created during this review.

## Solution

## Materials