---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Persistent volume.md'
---
# Persistent volume
Note Created: 2023-03-04

## Definition

A [[PersistentVolume]] (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using [[Storage Class]]es. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a __lifecycle independent of any individual Pod__ that uses the PV.

[[Create volumes (pv)]]
[[Configure a Pod to Use a Volume ConfigMap for Storage]]

[pv](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)