---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/LFD259 domian review solution ch5.md'
---
# LFD259 domian review solution ch5
Note Created: 2023-02-26

## Lab 

> Create a new secret called specialofday using the key entree and the value meatloaf.
```console
k create secret generic specialofday --from-literal=key=entree --from-literal=value=meatloaf
```

> Create a new deployment called foodie running the nginx image.
```console
k create deploy foodie --image=nginx --dry-run=client -o yaml > deployment.yaml
```

> Add the specialofday secret to pod mounted as a volume under the /food/ directory.
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: foodie
  name: foodie
spec:
  replicas: 1
  selector:
    matchLabels:
      app: foodie
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: foodie
    spec:
      containers:
      - image: nginx
        name: nginx
        resources: {}
        volumeMounts: # mount
        - name: foo
          mountPath: "/food/"
          readOnly: true
      volumes: # volume
      - name: foo
        secret:
          secretName: specialofday
          optional: true
status: {}
```
```console
k apply -f deployment.yaml
```

> Execute a bash shell inside a foodie pod and verify the secret has been properly mounted.
```console
k exec foodie -it -- sh
$ ls
$ cd food
$ cat key
$ cat value
$ exit
```

> Update the deployment to use the nginx:1.12.1-alpine image and verify the new image is in use.
Update YAML
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: foodie
  name: foodie
spec:
  replicas: 1
  selector:
    matchLabels:
      app: foodie
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: foodie
    spec:
      containers:
      - image: nginx:1.12.1-alpine # change image
        name: nginx
        resources: {}
        volumeMounts:
        - name: foo
          mountPath: "/food/"
          readOnly: true
      volumes:
      - name: foo
        secret:
          secretName: specialofday
          optional: true
status: {}
```
```console
k apply -f deployment.yaml
```

> Roll back the deployment and verify the typical, current stable version of nginx is in use again.
```console
k rollout history deployment foodie 
k rollout undo deployment foodie
```

> Create a new 200M NFS volume called reviewvol using the NFS server configured earlier in the lab.
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: reviewvol
spec:
  capacity:
    storage: 100Gi
  volumeMode: Filesystem
  accessModes:
  - ReadWriteOnce
  persistentVolumeReclaimPolicy: Delete
  storageClassName: local-storage
  local:
    path: /mnt/disks/ssd1
  nodeAffinity:
    required:
      nodeSelectorTerms:
      - matchExpressions:
        - key: kubernetes.io/hostname
          operator: In
          values:
          - node01
```

> Create a new PVC called reviewpvc which will uses the reviewvol volume.
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: reviewpvc
  namespace: default
spec:
  storageClassName: local-storage
  volumeName: reviewvol
  resources:
      requests:
        storage: 8Mi
  accessModes:
      - ReadWriteOnce
```

> Edit the deployment to use the PVC and mount the volume under /newvol
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  creationTimestamp: null
  labels:
    app: foodie
  name: foodie
spec:
  replicas: 1
  selector:
    matchLabels:
      app: foodie
  strategy: {}
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: foodie
    spec:
      containers:
      - image: nginx:1.12.1-alpine
        name: nginx
        resources: {}
        volumeMounts:
        - name: foo
          mountPath: "/food/"
          readOnly: true
        - name: review
          mountPath: "/newvol/"
      volumes:
      - name: foo
        secret:
          secretName: specialofday
          optional: true
      - name: review
        persistentVolumeClaim:
          claimName: reviewpvc
status: {}
```

> Execute a bash shell into the nginx container and verify the volume has been mounted.
```console
k exec foodie-65984c9fcf-n2xtj -ti -- sh
cd food
ls
cd ..
cd newvol
exit
```

> Delete any resources created during this review.

## Solution

## Materials