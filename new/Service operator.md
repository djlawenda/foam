---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Service operator.md'
---
# Service operator
2023-02-19
Note Created: 2023-02-19

## Definition

[[controller]] operator which listens to the endpoint operator to provide a persistent
IP for Pods. Pods have ephemeral IP addresses chosen from a pool. Then
the service operator sends messages via the kube-apiserver which
forwards settings to kube-proxy on every node, as well as the network
plugin.