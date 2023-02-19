---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/api-server.md'
---
# api-server
2023-02-19
Note Created: 2023-02-19

## Definition

Kubernetes exposes an API via the API server.

The kube-apiserver is central to the operation of the Kubernetes
cluster. 

[All calls]{.underline}, both internal and external traffic,
[are handled via this agen]{.underline}t. 

All actions are accepted and
validated by this agent, and it is the [only connection to the etcd
database]{.underline}. It validates and configures data for API objects,
and services REST operations. As a result, it acts as a cp process for
the entire cluster, and acts as a frontend of the cluster\'s shared
state.
