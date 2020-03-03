---
layout: "post"
title: "Kubernetes Pod - ReplicationController - ReplicaSet"
categories: "kubernetes pod replicationcontroller replicaset"
permalink: "/:categories/:year/:month/:day/:title.html"
---

# Structure of pod-definition.yml:
```yaml
apiVersion: v1
kind: Pod
metadata:
   name: nginx-pod
   labels:
      app: nginx-app
      type: pod
spec:
   containers:
      - name: nginx-container
        image: nginx
```

# Basic Pod commands:
- kubectl create -f pod-definition.yml
- kubctl get pods
- kubeclt get pods -o wide
- kubectl get pod nginx-pod
- kubectl describe pods nginx-pod


# Structure of replicationcontroller-definition.yml:
```yaml
apiVersion: v1
kind: ReplicationController
metadata:
   name: nginx-rc
   labels:
      app: nginx-rc
      type: front-end
spec:
   template:
      metadata:
         name: nginx-pod
         labels:
            app: nginx-app
            type: front-end
      spec:
         containers:
            - name: nginx-container
              image: nginx
   replicas: 3
```

# Basic replication controller commands:
- kubectl create -f replicationcontroller-definition.yml
- kubectl get replicationcontrollers
- kubectl get rc
- kubctl delete  replicationcontroller/nginx-rc
