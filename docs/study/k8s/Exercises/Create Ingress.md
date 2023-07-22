---
type: exercise-note
tags: exercise
foam_template:
    name: exercise-note
    description: Exercise
    filepath: 'new/Create Ingress.md'
---
# Create Ingress
Note Created: 2023-02-26

## Lab 

Create Ingress rule

## Solution

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: ingress-test
  annotations:
    kubernetes.io/ingress.class: "nginx"
  namespace: default
spec:
  rules:
  - host: www.example.com
    http:
      paths:
      - backend:
          service:
            name: secondapp
            port:
              number: 80
        path: /
        pathType: ImplementationSpecific
  - host: www.something.com
    http:
      paths:
      - backend:
          service:
            name: thirdapp
            port:
              number: 80
        path: /
        pathType: ImplementationSpecific      
```

## Materials
LFD259 exercise 7.2