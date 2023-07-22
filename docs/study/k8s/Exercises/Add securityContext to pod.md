---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Add securityContext to pod.md'
---
# Add securityContext to pod
Note Created: 2023-02-25

## Lab 

To specify security settings for a Pod, include the securityContext field in the Pod specification. The securityContext field is a PodSecurityContext object. The security settings that you specify for a Pod **apply to all Containers in the Pod**.

## Solution

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: security-context-demo
spec:
  securityContext:
    runAsUser: 1000
    runAsGroup: 3000
    fsGroup: 2000
  volumes:
  - name: sec-ctx-vol
    emptyDir: {}
  containers:
  - name: sec-ctx-demo
    image: busybox:1.28
    command: [ "sh", "-c", "sleep 1h" ]
    volumeMounts:
    - name: sec-ctx-vol
      mountPath: /data/demo
    securityContext:
      allowPrivilegeEscalation: false
```

- `runAsUser` field specifies that for any Containers in the Pod, all processes run with user ID 1000
- `runAsGroup` field specifies the primary group ID of 3000 for all processes within any containers of the Pod
- `fsGroup` field is specified, all processes of the container are also part of the supplementary group ID 2000. The owner for volume /data/demo and any files created in that volume will be Group ID 2000

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/security-context/