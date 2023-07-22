---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Secrets.md'
---
# Create Secrets
Note Created: 2023-02-25

## Lab 

You can create the Secret by passing the raw data in the command.

Create a Secret that stores the username admin and the password S!B\*d$zDsb=

## Solution

```console
kubectl create secret generic db-user-pass \
    --from-literal=username=admin \
    --from-literal=password='S!B\*d$zDsb='
```

## Lab 

Create the Secret storing the credentials in files that you pass in the command

## Solution

```console
echo -n 'admin' > ./username.txt
echo -n 'S!B\*d$zDsb=' > ./password.txt

kubectl create secret generic db-user-pass \
    --from-file=username=./username.txt \
    --from-file=password=./password.txt
```

## Lab 

Create the Secret using Configuration File

## Solution

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
type: Opaque
data:
  username: YWRtaW4=
  password: MWYyZDFlMmU2N2Rm
```
```console
kubectl apply -f ./secret.yaml
```

## Materials
https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/