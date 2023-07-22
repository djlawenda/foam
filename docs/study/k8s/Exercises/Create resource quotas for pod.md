---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Create resource quotas for pod.md'
---
# Create resource quotas for pod
Note Created: 2023-02-22

## Specify a memory request and a memory limit

### memory resource
To specify a memory request for a Container, include the `resources:requests` field in the Container's resource manifest. 
To specify a memory limit, include `resources:limits`.

example
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: memory-demo
  namespace: mem-example
spec:
  containers:
  - name: memory-demo-ctr
    image: polinux/stress
    resources:
      requests:
        memory: "100Mi"
      limits:
        memory: "200Mi"
    command: ["stress"]
    args: ["--vm", "1", "--vm-bytes", "150M", "--vm-hang", "1"]
```



### cpu resource



Materials
https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/