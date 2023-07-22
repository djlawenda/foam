---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create ConfigMap from file.md'
---
# Create ConfigMap from file
Note Created: 2023-02-25

## Lab 

Use kubectl create configmap to create a ConfigMap from an individual file, or from multiple files

## Solution

Create sample files
```console
vim game.properties
```
```yaml
enemies=aliens
lives=3
enemies.cheat=true
enemies.cheat.level=noGoodRotten
secret.code.passphrase=UUDDLRLRBABAS
secret.code.allowed=true
secret.code.lives=30
```
```console
vim ui.properties
```
```yaml
color.good=purple
color.bad=yellow
allow.textmode=true
how.nice.to.look=fairlyNice
```

### Create configmap from 1 file --from-file=<file>
```console
kubectl create configmap game-config-2 --from-file=game.properties
```

### Create configmap from multiplefiles --from-file=<file>
```console
kubectl create configmap game-config-2 --from-file=game.properties --from-file=ui.properties
```

### Create configmap from env file --from-env-file=<file>

Sample env file
```yaml
# Env-files contain a list of environment variables.
# These syntax rules apply:
#   Each line in an env file has to be in VAR=VAL format.
#   Lines beginning with # (i.e. comments) are ignored.
#   Blank lines are ignored.
#   There is no special handling of quotation marks (i.e. they will be part of the ConfigMap value)).
# The env-file `game-env-file.properties` looks like below
cat configure-pod-container/configmap/game-env-file.properties
enemies=aliens
lives=3
allowed="true"

# This comment and the empty line above it are ignored
```
```console
kubectl create configmap game-config-env-file \
       --from-env-file=game-env-file.properties
```

## Materials
https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/