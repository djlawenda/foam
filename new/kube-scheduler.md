---
type: definition-note
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/kube-scheduler.md'
---
# kube-scheduler
2023-02-19
Note Created: 2023-02-19

## Definition

The [[kube-scheduler]] is forwarded the pod spec for running containers
coming to the API and finds a suitable node to run those containers.

The kube-scheduler uses an algorithm to determine which node will host a
Pod of containers. The scheduler will try to view available resources
(such as volumes) to bind, and then try and retry to deploy the Pod
based on availability and success. There are several ways you can affect
the algorithm, or a custom scheduler could be used instead. You can also
bind a Pod to a particular node, though the Pod may remain in a pending
state due to other settings