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
- kubectl get rc # short form for replicationcontroller
- kubctl delete  replicationcontroller/nginx-rc


# Structure of replicaset-definition.yml:
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
   name: demo-replicaset
   labels:
      app: demo-app
      type: front-end
spec:
   template:
      metadata:
         name: demo-pod
         labels:
            app: demo-app
            type: front-end
      spec:
         containers:
            - name: nginx-container
              image: nginx
   replicas: 3
   selector:
      matchLabels:
         type: front-end
```

# Basic commands for replicaset:
- kubectl create -f replicatset-definition.yml
- kubectl replace -f replicatset-definition.yml  #replace the existing replicaset
- kubectl scale --replicas=6 -f replicaset-definition.yml #scale up the replica to 6.
*Notes: the above command will not change replicaset insde the replicaset-definition.yml file*
- kubectl scale --replicas=6 replicaset demo-replicaset
- kubectl get rs
- kubectl edit rs demo-replicaset
- kubectl delete replicaset demo-replicaset # that will delete replicaset and all the underlying pods
- kubectl delete rs demo-replicaset #short form of replicaset
