---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Ephemeral volume.md'
---
# Ephemeral volume
Note Created: 2023-03-04

## Definition

Ephemeral volume for applications that need additional storage but don't care whether that data is stored persistently across restarts.
Ephemeral volumes __follow the Pod's lifetime__ and get created and deleted along with the Pod, Pods can be stopped and restarted without being limited to where some persistent volume is available.

Types of ephemeral volumes
- `emptyDir`: empty at Pod startup, with storage coming locally from the kubelet base directory (usually the root disk) or RAM
- `configMap`, downwardAPI, `secret`: inject different kinds of Kubernetes data into a Pod

`emptyDir`, `configMap`, downwardAPI, `secret` are provided as local ephemeral storage. They are managed by kubelet on each node.

[[Mount volume to pod]]
[[Use volumes (emptyDir, ConfigMap, Secret]]