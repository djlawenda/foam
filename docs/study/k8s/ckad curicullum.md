study notes from [[k8s]]

## 1. Application Design and Build	20%
- [[Pod lifecycle]] 
  - [[Create new pod]]
- [[Add env variables to pod]]
- [[Add custom commands to pod]]
- [[Create config map from plain text]]
- [[Create ConfigMap from file]]
- [[Mount ConfigMap as env ref]] 
- [[Mount ConfigMap as volume]]
- [[Configure and run multiple containers in pod]]
  - [[Create InitContainers]]
  - [[Create sidecar adapter]]
  - [[Create sidecar ambassador]]
- [[Create volumes (pv)]]
- [[Create volume claim (pvc)]]
- [[Use volumes (emptyDir, ConfigMap, Secret]])
- [[Mount volume to pod]]

## 2. Application Deployment	20%
- [[Create deployment]]
  - [[Create deployment imperatively]]
- [[Edit deployment]]
- [[Scale deployment]] 
  - [[Scale resources]]
- [[Rollout, roll back deployment]]
  - [[Review object updates with rollout]]
- [[Create Jobs]]
  - [[Create Job imperatively]]
- [[Create CroneJobs]] 

## 3. Application Observability and Maintenance	15%
- [[Create resource quotas for pod]]
  - [[Exceed a Container's memory limit]]
- [[Create resource limits in namespace]]
- [[Create readiness probes]]
- [[Create liveness probes]]
- [[Change probes type (http, custom command, socket)]]
- [[Debug misbehaving pods (k get, k describe, k logs, k exec)]]
  - [[List events]]
- [[Assign label to object]] 
  - [[Get labels for object]]
- [[Use labels in selector]]
- [[Add annotation]]

## 4. Application Environment, Configuration and Security	25%
- [[Create Secrets]]
- [[Add securityContext to pod]] 
- [[Add securityContext to container]]
- [[SecurtyContext runAsUser, runAsGroup]]
- [[Create serviceAccount]]
- [[Assign serviceAccount to pod]]

## 5. Services and Networking	20%
- [[Create Service]]
  - [[Expose pod imperatively]]
- [[Update Service]]
- [[Create Network policy]]














