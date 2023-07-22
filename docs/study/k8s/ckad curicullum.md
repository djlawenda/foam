study notes from [[k8s]]

## 0. Prep
[[Step by step after exam start]]
[[Bookmarks for manifests]]
[[Change context]]
[[Setup Vim]]
[[Create aliases]]
[[Create YAML from existing object]]
[[Create YAML manifest quickly (pod, deploy, service, job)]]

## 1. Application Design and Build	20%

### Containers
- [[Define container images]]
- [[Build container images]]
- [[Modify container images]]
- [[Modify container capabilites]]
 
### Pod
- [[Pod lifecycle]] 
  - [[Create new pod]]
    - [[Create static Pods]] # todo
  - [[Pod quality of service]]
    - [[Create a Pod that gets assigned a QoS class of Guaranteed]]
    - [[Create a Pod that gets assigned a QoS class of Burstable]]
    - [[Create a Pod that gets assigned a QoS class of BestEffort]]
  - [[Attach Handlers to Container Lifecycle Events]] # todo
- [[Add env variables to pod]]
- [[Add custom commands to pod]]

### ConfigMap
- [[Create ConfigMap]]
  - [[Create config map from plain text]]
  - [[Create ConfigMap from file]]
  - [[Create ConfigMap from directory]]
- [[Mount ConfigMap as env ref]] 
- [[Configure a Pod to Use a Volume ConfigMap for Storage]]
- [[Configure and run multiple containers in pod]]

### Volume
- [[Create volumes (pv)]]
- [[Create volume claim (pvc)]]
- [[Use volumes (emptyDir, ConfigMap, Secret]])
  - [[Configure a Pod to Use a Volume emptyDir for Storage]]
  - [[Configure a Pod to Use a Volume ConfigMap for Storage]]
  - [[Configure a Pod to Use a Volume Secret for Storage]]
- [[Mount volume to pod]]

## 2. Application Deployment	20%

### Deployments
- [[Create deployment]]
  - [[Create deployment imperatively]]
- [[Edit deployment]]
- [[Scale deployment]] 
  - [[Scale resources]]
- [[Rollout, roll back deployment]] # todo
  - [[Rollout, roll back deployment]]

### Jobs
- [[Create Jobs]] # todo
  - [[Create Job imperatively]]
- [[Create CroneJobs]]
- [[Deploy packages with Helm]]

## 3. Application Observability and Maintenance	15%

### Resources
- [[Create resource quotas for pod]]
  - [[Exceed a container memory limit]]
- [[Create memory resource limits in namespace]]
- [[Create cpu resource limits in namespace]]
- [[Create memory min max constrains in namespace]]
  - [[Attempt to create pod that exceeds the max memory constrain in namespace]]
- [[Create pod quota for namespace]]
  - [[Attempt to create pod that exceeds the max cpu constrain in namespace]] 
- [[Create pod quota for namespace]]

### Probes
- [[Create readiness probes]]
- [[Create liveness probes]]
  - [[Create liveness probes with command]]
  - [[Create liveness probes with http request]]
  - [[Create liveness probes with tcp socket]]
  - [[Create liveness probes with gRPC]]
- [[Create startup probes]]
- [[Change probes type (http, custom command, socket)]]

### Debug
- [[Debug misbehaving pods (k get, k describe, k logs, k exec)]]
  - [[List events]]
  - [[Debug pod with exec]]
  - [[Debug pod with a copy]]
  - [[Debug pod with ephemeral debug container]]
- [[Monitor application]]
- [[Use container logs]]
  - [[Save pod logs to file]]

### Labels
- [[Assign label to object]] 
  - [[Get labels for object]]
- [[Use labels in selector]]
- [[Add annotation]]
- [[Sort by metadata]]

## 4. Application Environment, Configuration and Security	25%

### Secret
- [[Create Secrets]]
  - [[Get Secret]]
 
### RCAB
- [[SecurtyContext runAsUser, runAsGroup]]
  - [[Set privilage escalation in securityContext]]
- [[Create serviceAccount]]
- [[Create Role]]
- [[Create ClusterRole]]
- [[Create RoleBinding]]
  - [[Check if role can do stuff]]
- [[Assign serviceAccount to pod]]
- [[Assign Pods to Nodes nodeSelector nodeName]]
- [[Assign Pods to Nodes using Node Affinity]]

### CRD
- [[View CRDs]]


## 5. Services and Networking	20%

### Service
- [[Create Service]]
  - [[Create Service ClusterIP]]
  - [[Create multiport Service]]
  - [[Create Service NodePort]]
  - [[Create Service LoadBalancer]]
  - [[Expose pod imperatively]]
- [[Update Service]] # todo
- [[Debug Service]] # todo
- [[Create Network policy]]

### Ingress
- [[Create Ingress]]

### 6. Test yourself
- [[LFD259 domain review]]
  - [[LFD259 domian review solution ch2]]
  - [[LFD259 domian review solution ch3]]
  - [[LFD259 domian review solution ch4]]
  - [[LFD259 domian review solution ch5]]
  - [[LFD259 domian review solution ch6]]
  - [[LFD259 domian review solution ch7]]
  - [[LFD259 domian review solution ch8]]
- [[How to crush CKAD]]
- [[CKAD scenarios from killercoda]]
- https://github.com/dgkanatsios/CKAD-exercises
- https://thospfuller.com/2020/11/09/answers-to-five-kubernetes-ckad-practice-questions-2021/














