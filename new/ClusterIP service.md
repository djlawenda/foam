---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/ClusterIP service.md'
---
# ClusterIP service
2023-02-19
Note Created: 2023-02-19

## Definition

ClusterIP [[service]] is accessible within [[cluster]] only

ClusterIP which is used to connect inside the cluster, not the IP of the
cluster. As the graphic shows, this can be used to connect to a NodePort
for outside the cluster, an IngressController or proxy, or another
"backend"pod or pods.