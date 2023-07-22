---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Pod quality of service.md'
---
# Pod quality of service
Note Created: 2023-02-25

## Definition

Kubernetes classifies the Pods that you run and allocates each Pod into a specific `quality of service (QoS) class`.
Kubernetes does this classification based on the resource requests of the Containers in that Pod, along with how those requests relate to resource limits.

The possible QoS classes are Guaranteed, Burstable, and BestEffort.

`Guaranteed`
Pods that are Guaranteed have the strictest resource limits and are least likely to face eviction.

`Burstable`
Pods that are Burstable have some lower-bound resource guarantees based on the request, but do not require a specific limit.

`BestEffort`
Pods in the BestEffort QoS class can use node resources that aren't specifically assigned to Pods in other QoS classes. The kubelet prefers to evict BestEffort Pods if the node comes under resource pressure.