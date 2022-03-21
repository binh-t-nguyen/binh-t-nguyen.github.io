---
layout: "post"
title: "Customize Helm Chart"
categories: "kubernetes helm"
permalink: "/:categories/:year/:month/:day/:title.html"
---

## Create a new chart:
By default, helm will generate chart with nginx template:
```
helm create mydevchart
```


That will create:
<ul>
  <li><strong> Chart.yaml </strong>: contains meta-data of the chart </li>
  <li><strong> values.yaml </strong>: values that will be used to replace in the templates </li>
  <li><strong> templates directory</strong>: contains templates. Example: deployment.yaml, ingress.yaml, service.yaml, service.yaml etc. </li>
  <li><strong> charts directory </strong>: contains charts as dependency </li>
</ul>


## Chart.yaml:

Required fields:
<ul>
  <li>apiVersion</li>
  <li>name</li>
  <li>description</li>
  <li>type: application or library</li>
  <li>appVersion: application version</li>
</ul>

Optional fiels:
<ul>
  <li>icon: icon of the project</li>
  <li>keywords: keywords being used in the project</li>
  <li>home: home of the projects</li>
  <li>sources: sources web sites etc.</li>
  <li>maintainer: team, persons, emails etc.</li>
</ul>


## Package a chart for distribution:
```
helm package mydevchart
```

Update dependent charts and then package a chart for distribution:
```
helm package mydevchart -u
```

## Create helm ignore file: .helmignore
Similar to .ignore file in git: it is used to ignore files that we don't want to include in the package. 
Reference: <https://helm.sh/docs/chart_template_guide/helm_ignore_file>

## Validate syntax the helm templates and values:
```
helm lint mydevchart
```

## Pull the dependencies for an updated chart:
```
helm dependency update mydevchart
```

## Add chart to local repo:

Create the index file for local repo:
```
helm repo index my-dev-local-repo/
```

Add the developed chart to chart repo: that will add the zip chart to the repo 
```
helm package mydevchart -d my-dev-local-repo/
```

Update chart repo index after adding the developed chart to repo directory:
```
helm repo index my-dev-local-repo/
```

Install chart from local repo:
```
helm install myapp my-dev-local-repo/mydevchart
```

Pull chart package from local repo:
```
helm pull my-dev-local-repo/mydevchart
```

Install the chart from zip file:
```
helm install myapp mydevchart-0.1.0.tgz
```

## Helm starter:

The helm starter allows developer create chart using an existing template.

The starter templates are stored in $HELM_HOME\staters
Example: C:\Users\xxxxx\AppData\Roaming\helm\starters

To verify helm enviroment:
```
helm env
```

Create a chart with starter option:
```
helm create --starter mychartstarter mynewchart
```

## Install helm plugin:
Reference: <https://github.com/salesforce/helm-starter>
```
helm plugin install https://github.com/salesforce/helm-starter.git
```

List the helm plugins:
```
helm plugin list
```