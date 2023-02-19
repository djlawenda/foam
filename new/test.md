---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/test.md'
---
# test
Note Created: 2023-02-19

## Note

- Pod lifecycle
- Add env variables to pod
- Add custom commands to pod
- Create config map from CLI - 
  - from plain text
  - from file
- ConfigMap 
  - as env ref 
  - volume
- Secrets
- securityContext at pod and container level - runAsUser, runAsGroup
- Resource quotas in namespace - min and max resource for pod
- serviceAccount - assign to pod
- Configure and run multiple containers in pod
  - InitContainers
  - sidecar
    - adapter
    - ambassador
- probes
  - readiness
  - liveness
  - how?
    - http
    - custom command
    - socket
- debug misbehaving pods
  - k get
  - k describe
  - k logs
  - k exec
- Deployment
  - create, edit
  - scale
  - rollout, roll back
- Jobs
  - CroneJobs
- Labels
  - add
  - use in selector
- Annotations
- Service
  - create, update
  - network policy

