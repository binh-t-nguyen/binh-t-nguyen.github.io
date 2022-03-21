---
layout: "post"
title: "Basic Helm Commands"
categories: "kubernetes services"
permalink: "/:categories/:year/:month/:day/:title.html"
---

# List helm chart local repo:
```
helm repo list
```

# Add helm chart repo:
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

# Remove helm chart repo:
```
helm repo remove bitnami
```

# Update helm repo:
```
helm repo update
```

# Search for charts from repo:
```
helm search repo apache
```

# Install a release:
```
helm install devdb bitnami/mysql
```

# Install a release in a namespace:
```
helm install devdb bitnami/mysql --namespace dev-namespace --create-namespace
```

# Install a release with generated name:
```
helm install bitnami/mysql --generate-name
```

# Install a release with generated name with template:
```
helm install bitnami/mysql --generate-name --name-template="devdbserver-\{\{randAlpha 7 | lower\}\}"
```

# List installed releases:
```
helm list --namespace dev-namespace
```

# Uninstall a release and history:
```
helm uninstall --namespace dev-namespace devdb
```

# Uninstall a release but keep history (kept in kubernetes secret):
```
helm uninstall devdb --keep-history
```

# Check status of a release:
```
helm status devdb
```

# Upgrade a release:
```
helm upgrade --namespace dev-namespace devdb bitnami/mysql --set auth.rootPassword=$ROOT_PASSWORD
```

# Upgrade a release with custom values:
```
helm upgrade --namespace dev-namespace devdb bitnami/mysql --values=values.yaml
```

# Upgrade a release, if not exist, create one:
```
helm upgrade --install --namespace dev-namespace devdb bitnami/mysql
```

# The dry-run option:
This option is similar to the dry-run option in kubectl.
It will generate two parts: template & notes. Helm will connect to Kubernetes server to validate the template.
```
helm install testdb bitnami/mysql --dry-run
```

# Get template from a release:
```
helm template devdb bitnami/mysql
```

# Retrieve the note of a release:
```
helm get notes devdb
```

# Get customed values from a release:
```
helm get values devdb
```

# Get customed values from a revision of a release:
```
helm get values devdb --revision 2
```

# Get all values provided in a release:
```
helm get values devdb --all
```

# Get the manifest: 
This will generate manifest so we can save in yaml files and then kubectl apply -f yaml files
```
helm get manifest devdb
```

# List revision history: 
List the deployed revisions and the failed ones
```
helm history devdb
```

# Rollback to a history revision:
```
helm rollback devdb 1
```