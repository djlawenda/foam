---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Add securityContext to container.md'
---
# Add securityContext to container
Note Created: 2023-02-25

## Lab 

Set the security context for a Container

## Solution

To specify security settings for a Container, include the securityContext field in the Container manifest. The securityContext field is a SecurityContext object. Security settings that you specify for a Container **apply only to the individual Container**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo-2
spec:
  securityContext:
    runAsUser: 1000
  containers:
  - name: sec-ctx-demo-2
    image: gcr.io/google-samples/node-hello:1.0
    securityContext:
      runAsUser: 2000
      allowPrivilegeEscalation: false
```
Get a shell into the running Container
```console
kubectl exec -it security-context-demo-2 -- sh
ps aux
```

USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
2000         1  0.0  0.0   4336   764 ?        Ss   20:36   0:00 /bin/sh -c node server.js
2000         8  0.1  0.5 772124 22604 ?        Sl   20:36   0:00 node server.js

The output shows that the processes are running as user 2000. This is the value of runAsUser specified for the Container. It overrides the value 1000 that is specified for the Pod.

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/security-context/