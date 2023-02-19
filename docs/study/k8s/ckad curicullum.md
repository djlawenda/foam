study notes from [[k8s]]

# DOMAIN	WEIGHT
Application Design and Build	20%
Application Deployment	20%
Application Observability and Maintenance	15%
Application Environment, Configuration and Security	25%
Services and Networking	20%

Prep work

- [[Pod lifecycle]] 
  - [[Create new pod]]
- [[Add env variables to pod]]
- [[Add custom commands to pod]]
- [[Create config map from plain text]]
- [[Create ConfigMap from file]]
- Mount ConfigMap as env ref 
- Mount ConfigMap as volume
- Create Secrets
- Add securityContext to pod and 
- Add securityContext to container
- SecurtyContext runAsUser, runAsGroup
- Create resource quotas for pod
- Create resource limits in namespace
- Create serviceAccount
- Assign serviceAccount to pod
- Configure and run multiple containers in pod
- Create InitContainers
- Create sidecar adapter
- Create sidecar ambassador
- Create readiness probes
- Create liveness probes
- Change probes type (http, custom command, socket)
- Debug misbehaving pods (k get, k describe, k logs, k exec)
  - [[List events]]
- Create deployment
  - [[Create deployment imperatively]]
- Edit deployment
- Scale deployment 
  - [[Scale resources]]
- Rollout, roll back deployment
  - [[Review object updates with rollout]]
- Create Jobs
  - [[Create Job imperatively]]
- Create CroneJobs
- Add labels 
  - [[Assign label to object]] 
  - [[Get labels for object]]
- Use labels in selector
- Create Annotations 
  - [[Add annotation]]
- Create Service
  - [[Expose pod imperatively]]
- Update Service
- Create Network policy
- Create volumes (pv)
- Create volume claim (pvc)
- Use volumes (emptyDir, ConfigMap, Secret)
- Mount volume to pod

