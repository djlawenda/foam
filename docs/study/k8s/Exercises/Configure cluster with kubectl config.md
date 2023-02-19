---
type: exercise-note
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Configure cluster with kubectl config.md'
---
# Configure cluster with kubectl config
2023-02-19
Note Created: 2023-02-19

## Lab 

1. show Merged kubeconfig settings
2. display list of contexts
3. display the current-context
4. set the default context to my-cluster-name
5. permanently save the namespace for all subsequent kubectl commands

## Solution

1. kubectl config view
2. kubectl config get-contexts
3. kubectl config current-context
4. kubectl config use-context my-cluster-name
5. kubectl config set-context --current --namespace=name

## Materials
https://kubernetes.io/docs/reference/kubectl/cheatsheet/