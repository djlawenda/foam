---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Deployment.md'
---
# Deployment
2023-02-19
Note Created: 2023-02-19

## Definition

The default and feature-filled operator for containers is a Deployment.
A Deployment does not directly work with pods. Instead it manages
ReplicaSets. The ReplicaSet is an operator which will create or
terminate pods according to a podSpec. The podSpec is sent to the
kubelet, which then interacts with the container engine to download and
make available the required resources, then spawn or terminate
containers until the status matches the spec.

-   Operator Deployment \>\> manages \>\> operator ReplicaSet

-   Operator ReplicaSet \>\> acts according to \>\> podSpec

-   podSpec \>\> goes to \>\> kubelet

-   kubelet \>\> tells what to do \>\> container engine

-   Container engine \>\> creates, terminates, updates \>\> containers