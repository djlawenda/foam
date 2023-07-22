---
type: definition-note
tags: definition
foam_template:
    name: definition-note
    description: Definition
    filepath: 'new/Stroage class.md'
---
# Stroage class
Note Created: 2023-03-04

## Definition

A StorageClass provides a way for administrators to describe the "classes" of storage they offer.

Each StorageClass contains the fields `provisioner`, `parameters`, and `reclaimPolicy`, which are used when a PersistentVolume belonging to the class needs to be dynamically provisioned.

Example:
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
reclaimPolicy: Retain
allowVolumeExpansion: true
mountOptions:
  - debug
volumeBindingMode: Immediate
```