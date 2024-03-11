---
layout: "post"
title: "How to Deploy Spring Boot Application to Azure Web App"
categories: "springboot azure webapp"
permalink: "/:categories/:year/:month/:day/:title.html"
---

Azure Web App Service:
======================
Azure Web App supports a wide range of programming languages:
- .NET (C#, F#, VB.NET)
- Java
- Node.js
- Python
- PHP
- Ruby
- Go

*In order to deploy Spring Boot application to Azure Web App, we need to create the resources before deploying the applications*

Create resources in Azure console:
==================================
- Login to Azure portal: <https://portal.azure.com>
- Create web app resource:
  - Subscription: **111111-11111-11111-1111111**
  - Resource group: **xxxxxxxx-rg**
  - Region: **eastus**
  - Name: example; **javawebap**
  - Runtime: **Java**
  - App Service Plan: **free, basic, premium**


Create Spring Boot application:
==============================
- Create spring boot application <https://start.spring.io/> using Maven
- Add REST controller
- Add the following Maven pluggin in the pom.xml:
```xml
	<plugin> 
	  <groupId>com.microsoft.azure</groupId>  
	  <artifactId>azure-webapp-maven-plugin</artifactId>  
	  <version>2.9.0</version>  
	  <configuration>
		<subscriptionId>111111-11111-11111-1111111</subscriptionId>
		<resourceGroup>xxxxxxxx-rg</resourceGroup>
		<appName>javawebap</appName>
		<pricingTier>B1</pricingTier>
		<region>eastus</region>
		<runtime>
		  <os>Linux</os>      
		  <webContainer>Java SE</webContainer>
		  <javaVersion>Java 11</javaVersion>
		</runtime>
		<deployment>
		  <resources>
			<resource>
			  <type>jar</type>
			  <directory>${project.basedir}/target</directory>
			  <includes>
				<include>*.jar</include>
			  </includes>
			</resource>
		  </resources>
		</deployment>
	  </configuration>
	</plugin>
```

Deploy Spring Boot application to Azure Web App:
================================================
```
mvn package azure-webapp:deploy
```


Reference:
==========
<https://github.com/microsoft/azure-maven-plugins/blob/develop/azure-webapp-maven-plugin/README.md>

