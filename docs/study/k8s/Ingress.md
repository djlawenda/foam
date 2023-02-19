---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Ingress.md'
---
# Ingress
2023-02-19
Note Created: 2023-02-19

## Definition

External service thru NodePort

Create internal svc which is default - ClusterIP

Host is the address (domain name or IP) that is the entry point to the
cluster. It can be the node in the cluster or it can be outside the
cluster that routes to cluster.

Ingress is the set of rules. To implement Ingress we need Ingress
Controller.