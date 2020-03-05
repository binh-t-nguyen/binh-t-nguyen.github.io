---
layout: "post"
title: "Kubernetes Pod IP Range"
categories: "kubernetes pod ip range"
permalink: "/:categories/:year/:month/:day/:title.html"
---

Kubernetes cluster maintains its own network with the IP range: 10.244.0.1-10.244.0.254

Run command: kubectl get pods -o wide # show the pods and the IP addresses:

```
osboxes@kube-master:~$ kubectl get pods -o wide
NAME                                             READY   STATUS    RESTARTS   AGE     IP            NODE         NOMINATED NODE   READINESS GATES
demo-deployment-779c656759-2ckn9                 1/1     Running   0          17m     10.244.1.29   kube-node1   <none>           <none>
demo-deployment-779c656759-c52h8                 1/1     Running   0          17m     10.244.2.22   kube-node2   <none>           <none>
demo-deployment-779c656759-pcsd7                 1/1     Running   0          17m     10.244.2.21   kube-node2   <none>           <none>
```
