---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/CKAD scenarios from killercoda.md'
---
# CKAD scenarios from killercoda
Note Created: 2023-03-05

## Lab 

### Kubectl Contexts
> List all available kubectl contexts and write the output to `/root/contexts`
```console
k config get-contexts
k config get-contexts > /root/contexts
```

> Switch to context purple and list all Pods.
```console
kubectl config use-context purple
k get po
```

> Switch to context yellow and list all Pods.
```console
kubectl config use-context yellow
k get po
```

### Pod with Resources
> Create a new Namespace limit .
```console
k create ns limit
k get ns
k config set-context --current --namespace=limit
```

> In that Namespace create a Pod named resource-checker of image httpd:alpine .
The container should be named my-container .
It should request 30m CPU and be limited to 300m CPU.
It should request 30Mi memory and be limited to 30Mi memory.

```console
k run resource-checker --image=httpd:alpine --dry-run=client -oyaml > pod.yaml
vim pod.yaml 
k create -f pod.yaml
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: resource-checker
  name: resource-checker
spec:
  containers:
  - image: httpd:alpine
    name: my-container
    resources:
      requests:
        cpu: "30m"
        memory: "30Mi"
      limits:
        cpu: "300m"
        memory: "30Mi"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

### ConfigMap Access in Pods

> Create a ConfigMap named trauerweide with content tree=trauerweide
```console
kubectl create configmap trauerweide --from-literal=tree=trauerweide
```

> Create the ConfigMap stored in existing file /root/cm.yaml
```yaml
apiVersion: v1
data:
  tree: birke
  level: "3"
  department: park
kind: ConfigMap
metadata:
  name: birke
```
```console
k create -f cm.yaml
```

### Access ConfigMaps in Pod
> Create a Pod named pod1 of image nginx:alpine
```console
k run pod1 --image=nginx:alpine
```

> Make key tree of ConfigMap trauerweide available as environment variable TREE1
Mount all keys of ConfigMap birke as volume. The files should be available under /etc/birke/*
```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: pod1
  name: pod1
spec:
  containers:
  - image: nginx:alpine
    name: pod1
    volumeMounts:
      - name: config-vol
        mountPath: /etc/birke
    env:
      - name: TREE1
        valueFrom:
          configMapKeyRef:
            name: trauerweide
            key: tree
    resources: {}
  volumes:
    - name: config-vol
      configMap:
        name: birke
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```

Test env+volume access in the running Pod
```console
kubectl exec pod1 -- env | grep "TREE1=trauerweide"
kubectl exec pod1 -- cat /etc/birke/tree
kubectl exec pod1 -- cat /etc/birke/level
kubectl exec pod1 -- cat /etc/birke/department
```

### ReadinessProbe
> Create a Deployment named space-alien-welcome-message-generator of image httpd:alpine with one replica.
```console
k create deploy space-alien-welcome-message-generator --image=httpd:alpine --dry-run=client -oyaml > deploy.yaml
```
> It should've a ReadinessProbe which executes the command stat /tmp/ready . This means once the file exists the Pod should be ready.
The initialDelaySeconds should be 10 and periodSeconds should be 5 .
Create the Deployment and observe that the Pod won't get ready.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: space-alien-welcome-message-generator
  name: space-alien-welcome-message-generator
spec:
  replicas: 1
  selector:
    matchLabels:
      app: space-alien-welcome-message-generator
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: space-alien-welcome-message-generator
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
        resources: {}
        readinessProbe: # readinessProbe at container level
          exec:
            command:
            - stat
            - /tmp/ready
          initialDelaySeconds: 10
          periodSeconds: 5
status: {}
```
```console
k create -f deploy.yaml 
k get deploy
k get po
k describe po space-alien-welcome-message-generator-8594f484b-wwb59
```
> Make the Deployment ready.
Exec into the Pod and create file /tmp/ready .
Observe that the Pod is ready.

```console
k exec space-alien-welcome-message-generator-8594f484b-wwb59 -ti -- sh
/usr/local/apache2 # touch /tmp/ready
/usr/local/apache2 # exit
k get po
```
Pod is Running

### Build and run a Container
> Create a new file /root/Dockerfile to build a container image from. It should:
- use bash as base
- run ping killercoda.com
```yaml
FROM bash
CMD ["ping", "killercoda.com"]
```
> Build the image and tag it as pinger .
```console
podman build -t pinger .
podman image ls
```

> Run the image (create a container) named my-ping .
```console
podman run --name my-ping pinger
```

> Tag the image, which is currently tagged as pinger , also as local-registry:5000/pinger .
```console
podman tag pinger:latest local-registry:5000/pinger
```
> Then push the image into the local registry.
```console
podman push local-registry:5000/pinger
```
> Without specifying a :tag , the default :latest will be used. Now we want to use tag :v1 instead.
Tag the image, which is currently tagged as pinger , also as pinger:v1 and local-registry:5000/pinger:v1 .
```console
podman tag pinger pinger:v1
podman tag pinger local-registry:5000/pinger:v1
podman image ls
```

> Then push the image into the local registry.
```console
podman push local-registry:5000/pinger:v1
```

### Rollout Rolling
> Application "wonderful" is running in default Namespace.
You can call the app using curl wonderful:30080 .
The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .
Set the maxSurge to 50% and the maxUnavailable to 0% . Then perform a rolling update.
Wait till the rolling update has succeeded.

```console
k get deploy wonderful-v1 -oyaml > deploy.yaml
```
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
  generation: 1
  labels:
    app: wonderful
  name: wonderful-v1
  namespace: default
spec:
  progressDeadlineSeconds: 600
  replicas: 3
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: wonderful
  strategy:
    rollingUpdate:
      maxSurge: 50% # update
      maxUnavailable: 0% # update
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: wonderful
    spec:
      containers:
      - image: nginx:alpine # update
        imagePullPolicy: IfNotPresent
        name: httpd
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
```
```console
k apply -f deploy.yaml
```
Option 2 is:
```console
k edit deploy wonderful-v1
```

### Rollout Green-Blue
> Application "wonderful" is running in default Namespace.
You can call the app using curl wonderful:30080 .
The application YAML is available at `/wonderful/init.yaml` .
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v1
spec:
  replicas: 4
  selector:
    matchLabels:
      app: wonderful
      version: v1
  template:
    metadata:
      labels:
        app: wonderful
        version: v1
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
  name: wonderful
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 30080
  selector:
    app: wonderful
    version: v1
  type: NodePort
```

> The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .
The switch should happen instantly. Meaning that from the moment of rollout, all new requests should hit the new image.
Create a new Deployment wonderful-v2 which uses image nginx:alpine with 4 replicas. It's Pods should have labels app: wonderful and version: v2
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v2
spec:
  replicas: 4
  selector:
    matchLabels:
      app: wonderful
      version: v2
  template:
    metadata:
      labels:
        app: wonderful
        version: v2
    spec:
      containers:
      - image: nginx:alpine
        name: nginx
```

> Once all new Pods are running, change the selector label of Service wonderful to version: v2
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
  name: wonderful
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 30080
  selector:
    app: wonderful
    version: v2
  type: NodePort
```

> Finally scale down Deployment wonderful-v1 to 0 replicas
```console
kubectl scale deploy wonderful-v1 --replicas 0
```

### Rollout Canary
> Application "wonderful" is running in default Namespace.
You can call the app using curl wonderful:30080 .
The application YAML is available at /wonderful/init.yaml .
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v1
spec:
  replicas: 10
  selector:
    matchLabels:
      app: wonderful
  template:
    metadata:
      labels:
        app: wonderful
    spec:
      containers:
      - image: httpd:alpine
        name: httpd
---
apiVersion: v1
kind: Service
metadata:
  labels:
    app: wonderful
  name: wonderful
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 30080
  selector:
    app: wonderful
  type: NodePort
```

> The app has a Deployment with image httpd:alpine , but should be switched over to nginx:alpine .
The switch should not happen fast or automatically, but using the Canary approach:
- 20% of requests should hit the new image
- 80% of requests should hit the old image
For this create a new Deployment wonderful-v2 which uses image nginx:alpine .
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: wonderful
  name: wonderful-v2
spec:
  replicas: 2
  selector:
    matchLabels:
      app: wonderful
  template:
    metadata:
      labels:
        app: wonderful
    spec:
      containers:
      - image: nginx:alpine
        name: nginx
```
There is a NodePort Service wonderful which listens on port 30080 . It has the Pods of Deployment of app "wonderful" as selector. We need to point Service to both depoyments, Selector needs to choose common labels for both.

The total amount of Pods of both Deployments combined should be 10.
```console
k scale deploy wonderful-v1 --replicas=8
```
Test by:
```console
curl wonderful:30080
```
### Custom Resource Definitions
> Write the list of all installed CRDs into /root/crds .
```console
k get crd > /root/crds
```
> Write the list of all DbBackup objects into /root/db-backups .
```console
k get db-backups -A > /root/db-backups
```
> The team worked really hard for months on a new Shopping-Items CRD which is currently in beta.
Install it from `/code/crd.yaml` .
```console
k create -f /code/crd.yaml
```
> Then create a ShoppingItem object named bananas in Namespace default . The dueDate should be tomorrow and the description should be buy yellow ones .
```yaml
apiVersion: "beta.killercoda.com/v1"
kind: ShoppingItem
metadata:
  name: bananas
spec:
  description: buy yellow ones
  dueDate: tomorrow
```
```console
k get shopping-item
```
> You spent hours figuring out this "amazing" new CRD ShoppingItems created by the team.
But in the end you realised that it's pretty much the most useless CRD ever encountered.
If you need to run a Kubernetes cluster for managing your shopping list then things might have gone too far.
Delete the CRD and all ShoppingItem objects again.
```console
k delete shopping-item bananas
k delete -f /code/crd.yaml
```
or
```console
k delete crd shopping-items.beta.killercoda.com
```
### Helm
> Write the list of all Helm releases in the cluster into /root/releases .
```console
helm ls -A > /root/releases
```
> Delete the Helm release apiserver 
```console
helm ls -A
helm -n team-yellow uninstall apiserver
```
> Install the Helm chart nginx-stable/nginx-ingress into Namespace team-yellow .
The release should've the name devserver .
```console
helm install devserver nginx-stable/nginx-ingress -n team-yellow
```

### Create Ingress 
> There are two existing Deployments in Namespace world which should be made accessible via an Ingress.
```console
k config set-context --current --namespace=world
k get deploy
```
`asia.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  generation: 1
  labels:
    app: asia
  name: asia
  namespace: world
  resourceVersion: "1587"
spec:
  progressDeadlineSeconds: 600
  replicas: 2
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: asia
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: asia
    spec:
      containers:
      - image: nginx:1.21.5-alpine
        imagePullPolicy: IfNotPresent
        name: c
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: html
        - mountPath: /etc/nginx
          name: nginx-conf
          readOnly: true
      dnsPolicy: ClusterFirst
      initContainers:
      - command:
        - sh
        - -c
        - echo 'hello, you reached ASIA' > /html/index.html
        image: busybox:1.28
        imagePullPolicy: IfNotPresent
        name: init-container
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /html
          name: html
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - emptyDir: {}
        name: html
      - configMap:
          defaultMode: 420
          items:
          - key: nginx.conf
            path: nginx.conf
          name: nginx-conf
        name: nginx-conf
```
`europe.yaml`
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: "1"
  generation: 1
  labels:
    app: europe
  name: europe
  namespace: world
  resourceVersion: "1597"
spec:
  progressDeadlineSeconds: 600
  replicas: 2
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: europe
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: europe
    spec:
      containers:
      - image: nginx:1.21.5-alpine
        imagePullPolicy: IfNotPresent
        name: c
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /usr/share/nginx/html
          name: html
        - mountPath: /etc/nginx
          name: nginx-conf
          readOnly: true
      dnsPolicy: ClusterFirst
      initContainers:
      - command:
        - sh
        - -c
        - echo 'hello, you reached EUROPE' > /html/index.html
        image: busybox:1.28
        imagePullPolicy: IfNotPresent
        name: init-container
        resources: {}
        terminationMessagePath: /dev/termination-log
        terminationMessagePolicy: File
        volumeMounts:
        - mountPath: /html
          name: html
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
      volumes:
      - emptyDir: {}
        name: html
      - configMap:
          defaultMode: 420
          items:
          - key: nginx.conf
            path: nginx.conf
          name: nginx-conf
        name: nginx-conf
```

First: create ClusterIP Services for both Deployments for port 80 . The Services should have the same name as the Deployments.
```console
k expose deploy asia --port=80
k expose deploy europe --port=80
```
> The Nginx Ingress Controller has been installed.
Create a new Ingress resource called world for domain name world.universe.mine . The domain points to the K8s Node IP via /etc/hosts .
The Ingress resource should have two routes pointing to the existing Services:
http://world.universe.mine:30080/europe/
and
http://world.universe.mine:30080/asia/

!! Ingress needs to be in the same Namespace as application.
!! Check IngressClass - class in controller and rules need to match
```console
k get ingressclass
```
NAME    CLASS   HOSTS                 ADDRESS   PORTS   AGE
world   nginx   world.universe.mine             80      8s
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: world
spec:
  ingressClassName: nginx # needs to match class of controller!
  rules:
  - host: "world.universe.mine"
    http:
      paths:
      - pathType: Prefix
        path: "/asia"
        backend:
          service:
            name: asia
            port:
              number: 80
      - pathType: Prefix
        path: "/europe"
        backend:
          service:
            name: europe
            port:
              number: 80
```

### NetworkPolicy Namespace Selector
> There are existing Pods in Namespace space1 and space2 .
```console
k get po -n space1 --show-labels
```
NAME     READY   STATUS    RESTARTS   AGE    LABELS
app1-0   1/1     Running   0          4m2s   app=app1,controller-revision-hash=app1-58f9476d9f,statefulset.kubernetes.io/pod-name=app1-0

```console
k get po -n space2 --show-labels
```
NAME              READY   STATUS    RESTARTS   AGE     LABELS
microservice1-0   1/1     Running   0          4m13s   app=microservice1,controller-revision-hash=microservice1-5846475cbc,statefulset.kubernetes.io/pod-name=microservice1-0
microservice2-0   1/1     Running   0          4m13s   app=microservice2,controller-revision-hash=microservice2-66b65db57b,statefulset.kubernetes.io/pod-name=microservice2-0

We need a new NetworkPolicy named np that restricts all Pods in Namespace space1 to only have outgoing traffic to Pods in Namespace space2 . Incoming traffic not affected.
The NetworkPolicy should still allow outgoing DNS traffic on port 53 TCP and UDP.
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: np
  namespace: space1 # pods from space1
spec:
  podSelector: {} # all pods
  policyTypes:
    - Egress # restriction is for outgoing
  egress:
    - ports: # allow outgoing traffic on port 53
        - protocol: TCP
          port: 53
        - protocol: UDP
          port: 53
    - to: # allow to namespace space 2
        - namespaceSelector:
            matchLabels:
              kubernetes.io/metadata.name: space2
```
> Verify
```console
# these should work
k -n space1 exec app1-0 -- curl -m 1 microservice1.space2.svc.cluster.local
k -n space1 exec app1-0 -- curl -m 1 microservice2.space2.svc.cluster.local
k -n space1 exec app1-0 -- nslookup tester.default.svc.cluster.local
k -n space1 exec app1-0 -- nslookup killercoda.com

# these should not work
k -n space1 exec app1-0 -- curl -m 1 tester.default.svc.cluster.local
k -n space1 exec app1-0 -- curl -m 1 killercoda.com
```
### Admission Controllers


## Solution

## Materials