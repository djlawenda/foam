---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create ConfigMap from directory.md'
---
# Create ConfigMap from directory
Note Created: 2023-02-25

## Lab 

When you are creating a ConfigMap based on a directory, kubectl identifies files whose filename is a valid key in the directory and packages each of those files into the new ConfigMap.

## Solution

Create directory
```console
mkdir -p configure-pod-container/configmap/
```

Create sample files
```console
vim game.properties
```
enemies=aliens
lives=3
enemies.cheat=true
enemies.cheat.level=noGoodRotten
secret.code.passphrase=UUDDLRLRBABAS
secret.code.allowed=true
secret.code.lives=30

```console
vim ui.properties
```
color.good=purple
color.bad=yellow
allow.textmode=true
how.nice.to.look=fairlyNice

Create configmap
```console
kubectl create configmap game-config --from-file=configure-pod-container/configmap
```

get configmap
```console
kubectl get configmaps game-config -o yaml
```
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  creationTimestamp: 2022-02-18T18:52:05Z
  name: game-config
  namespace: default
  resourceVersion: "516"
  uid: b4952dc3-d670-11e5-8cd0-68f728db1985
data:
  game.properties: |
    enemies=aliens
    lives=3
    enemies.cheat=true
    enemies.cheat.level=noGoodRotten
    secret.code.passphrase=UUDDLRLRBABAS
    secret.code.allowed=true
    secret.code.lives=30    
  ui.properties: |
    color.good=purple
    color.bad=yellow
    allow.textmode=true
    how.nice.to.look=fairlyNice
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/