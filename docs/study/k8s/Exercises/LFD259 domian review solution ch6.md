---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch6.md'
---
# LFD259 domian review solution ch6
Note Created: 2023-02-26

## Lab 

> Create a new deployment which uses the nginx image.

```console
k create deploy new-deploy --image=nginx
```

> Create a new LoadBalancer service to expose the newly created deployment. Test that it works.
```console
k expose deploy new-deploy --type=LoadBalancer --port=80
```

3. Create a new NetworkPolicy called netblock which blocks all traffic to pods in this deployment only. Test that all traffic is blocked to deployment.
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: netblock
spec:
  podSelector:
    matchLabels:
      app: new-deploy
  policyTypes:
  - Ingress
```
```console
k create -f np.yaml
k get po
k describe po <new-deploy> # grab pod IP
curl <podIP>
```

> Update the netblock policy to allow traffic to the pod on port 80 only. Test that you can access the default nginx web page.
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: netblock
spec:
  podSelector:
    matchLabels:
      app: new-deploy
  policyTypes:
  - Ingress
  ingress:
    - {} # allows all ingress
```
```console
k delete networkpolicies netblock
k create -f np.yaml
k get po
k describe po <new-deploy> # grab pod IP
curl <podIP>
```

> Find and use the `security-review1.yaml` file to create a pod.
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: securityreview
spec:
  securityContext:
    runAsUser: 2100
  containers:
  - name:  webguy
    image: nginx
    securityContext:
      runAsUser: 3000
      allowPrivilegeEscalation: false
```

> View the status of the pod.
```console
k get po
k describe po securityreview
k logs securityreview
```
> Use the following commands to figure out why the pod has issues.
```console
student@cp:˜$ kubectl get pod securityreview
student@cp:˜$ kubectl describe pod securityreview
student@cp:˜$ kubectl logs securityreview
```
Back-off restarting failed container webguy in pod securityreview_default(6afb4062-cde8-4e5b-9873-342bf3ad0ca2)
2023/03/04 10:04:11 [emerg] 1#1: mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)
nginx: [emerg] mkdir() "/var/cache/nginx/client_temp" failed (13: Permission denied)

>  After finding the errors, log into the container and find the proper id of the nginx user.
```console
k exec securityreview -c webguy -it -- sh
```
error: unable to upgrade connection: container not found ("webguy") ???
* [ ] check with Cheryl?

> Edit the yaml and re-create the pod such that the pod runs without error.
```yaml
???
```

----------------------

>  Create a new serviceAccount called securityaccount.
```console
k create serviceaccount securityaccount 
```

>  Create a ClusterRole named secrole which only allows create, delete, and list of pods in all apiGroups.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  namespace: default
  name: secrole
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["create", "delete", "list"]
```

>  Bind the clusterRole to the serviceAccount.
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: secrole_bind
  namespace: default
subjects:
- kind: ServiceAccount
  name: securityaccount
  namespace: kube-system
roleRef:
  kind: ClusterRole #this must be Role or ClusterRole
  name: secrole # this must match the name of the Role or ClusterRole you wish to bind to
  apiGroup: rbac.authorization.k8s.io
```

>  Locate the token of the securityaccount. Create a file called /tmp/securitytoken. Put only the value of token: is equal to, a long string that may start with eyJh and be several lines long. Careful that only that string exists in the file.
```console
k get serviceaccount securityaccount -oyaml
```
```yaml
apiVersion: v1
kind: ServiceAccount
metadata:
  creationTimestamp: "2023-03-04T10:18:16Z"
  name: securityaccount
  namespace: default
  resourceVersion: "6693"
  uid: f2fd8b38-4759-4789-9678-c20f10c7ce70
```
Starting from v1.24 token is not created automatically for serviceAccount. Need to do it manually.
https://stackoverflow.com/questions/72256006/service-account-secret-is-not-listed-how-to-fix-it

>  Delete any resources created during this review.

## Materials