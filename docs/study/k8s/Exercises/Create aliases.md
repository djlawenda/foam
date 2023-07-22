---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create aliases.md'
---
# Create aliases
Note Created: 2023-02-26

## Lab 

Setup aliases in shell
In CKAD console k should be ready. Check by:
```console
alias -p
```

## Solution

- kublectl
```console
alias k=kubectl
```

- vim
```console
alias v=vim
```

- dry run
```console
export drc='--dry-run=client -o yaml'
```

- explain
```console
alias kx= 'kubectl explain'
```

## Lab 

Setup aliases in ~/.bashrc

## Solution

- Edit bashrc
```console
vim ~/.bashrc
```
- Add lines
alias k=kubectl
alias kdr='kubectl --dry-run=client -o yaml
alias kx= 'kubectl explain'

## Materials
https://devopscube.com/create-kubernetes-yaml/