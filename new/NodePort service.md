---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/NodePort service.md'
---
# NodePort service
2023-02-19
Note Created: 2023-02-19

## Definition

NodePort [[service]] is accessible from outside cluster

nodePort must be in range 30000 to 32767

NodePort svc is accessible at IP of node and port of nodePort

NodePort and static [[port]] (i.e.30008) is not secure bc it gives the
access to cluster from external app better option is to use Load
Balancer