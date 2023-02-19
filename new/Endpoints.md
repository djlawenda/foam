---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Endpoints.md'
---
# Endpoints
2023-02-19
Note Created: 2023-02-19

## Definition

The endpoint is created at the same time as the [[service]]. Note that it
uses the pod IP address, but also includes a [[port]]. The service connects
network traffic from a node high-number port to the endpoint using
iptables with ipvs on the way. 

The [[kube-controller-manager]] handles the
watch loops to monitor the need for endpoints and services, as well as
any updates or deletions.