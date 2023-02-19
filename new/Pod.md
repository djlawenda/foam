---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Pod.md'
---
# Pod
2023-02-19
Note Created: 2023-02-19

## Definition

A [[Pod]] consists of one or more containers which share an IP address,
access to storage and namespace. Typically, one container in a Pod runs
an application, while other containers support the primary application.

Containers in a Pod are started in parallel. As a result, there is no
way to determine which container becomes available first inside a pod.
The use of InitContainers can order startup, to some extent.
