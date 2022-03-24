---
layout: "post"
title: "Install Openshift Origin on on AWS EC2 Linux AMI"
categories: "openshift"
permalink: "/:categories/:year/:month/:day/:title.html"
---

# Create Security Group:

```
Inbound Rules:
80	TCP	
22	TCP
8443    TCP
443	TCP	
```

# Install docker:
```
yum update

sudo su

amazon-linux-extras install docker

docker --version

systemctl enable docker

systemctl start docker

systemctl status docker

usermod -aG docker $USER
```

# Set insecure registry:
```
echo '{
   "insecure-registries": [
     "172.30.0.0/16"
   ]
}' > /etc/docker/daemon.json

systemctl daemon-reload

systemctl restart docker
```

# Restart the EC2 instance

# Install oc:
```
curl -o ~/openshift-origin-client-tools-v3.9.0-191fece-linux-64bit.tar.gz -L https://github.com/openshift/origin/releases/download/v3.9.0/openshift-origin-client-tools-v3.9.0-191fece-linux-64bit.tar.gz

cd ~

tar -xzvf openshift-origin-client-tools-v3.9.0-191fece-linux-64bit.tar.gz

cd openshift-origin-client-tools-v3.9.0-191fece-linux-64bit/oc /usr/local/bin

exit

```

# Start Openshift:
```
oc cluster up --public-hostname=$(curl -s ifconfig.co)

Using Docker shared volumes for OpenShift volumes
Using public hostname IP 54.196.28.110 as the host IP
Using 54.196.28.110 as the server IP
Starting OpenShift using openshift/origin:v3.9.0 ...
OpenShift server started.

The server is accessible via web console at:
    https://54.196.28.110:8443

You are logged in as:
    User:     developer
    Password: <any value>

To login as administrator:
    oc login -u system:admin
```

# Shutdown Openshift:
```
 oc cluster down
```