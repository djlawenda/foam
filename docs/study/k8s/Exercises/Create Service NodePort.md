---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Service NodePort.md'
---
# Create Service NodePort
Note Created: 2023-02-25

## Lab 

For some parts of your application (for example, frontends) you may want to expose a Service onto an external IP address, that's outside of your cluster.

NodePort: Exposes the Service on each Node's IP at a static port (the NodePort).

## Solution

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: NodePort
  selector:
    app.kubernetes.io/name: MyApp
  ports:
      # By default and for convenience, the `targetPort` is set to the same value as the `port` field.
    - port: 80
      targetPort: 80
      # Optional field
      # By default and for convenience, the Kubernetes control plane will allocate a port from a range (default: 30000-32767)
      nodePort: 30007
```

## Materials
https://kubernetes.io/docs/concepts/services-networking/service/