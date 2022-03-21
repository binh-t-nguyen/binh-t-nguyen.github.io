---
layout: "post"
title: "Install Minikube and Helm on AWS EC2 Linux AMI"
categories: "kubernetes services"
permalink: "/:categories/:year/:month/:day/:title.html"
---

# Install docker:
```
yum update

sudo amazon-linux-extras install docker

docker --version

systemctl enable docker

systemctl start docker

systemctl status docker

usermod -aG docker $USER
```

# Install conntrack which is required for minikube:
```
yum -y install conntrack
```

# Install minikube:
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
```

# Install helm:
```
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh

chmod 700 get_helm.sh

get_helm.sh
```

# Testing:
```
minikube start --vm-driver=none

minikube status

helm --version
```