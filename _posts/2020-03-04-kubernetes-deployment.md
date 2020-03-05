---
layout: "post"
title: "Kubernetes Deployment"
categories: "kubernetes pod deployment"
permalink: "/:categories/:year/:month/:day/:title.html"
---

# Structure of deployment-definition.yml:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: demo-deployment
  labels:
    app: demo-app
    type: front-end
spec:
  template:
    metadata:
      name: demo-app
      labels:
        app: demo-app
        type: front-end
    spec:
      containers:
        - name: nginx-container
          image: nginx:1.16.1
  replicas: 3
  selector:
    matchLabels:
      type: front-end
```

# Basic deployment commands:
- kubectl create -f deployment-definition.yml —record
- kubectl get deployment
- kubectl describe deployment demo-deployment
- kubectl rollout status deployment/demo-deployment
- kubectl rollout history deployment/demo-deployment
- kubectl apply -f deployment-definition.yml
- kubectl set image deployment/demo-deployment nginx-container=nginx:1.17.9
- kubectl rollout undo deployment/demo-deployment
