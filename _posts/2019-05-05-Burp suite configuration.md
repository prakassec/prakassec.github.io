---
layout: post
title: Burp suite configuration
date: 2019-05-05 12:16:12
categories: WebApplication 
desc: Burpsuite intro & configuration
---
**Getting started with Burp suite**

Burp suite is a tool which is used in penetration testing. It contains collection of tools used to analyse a web application.  
Before installing Burp into your machine ensure that java is already installed.  

```
$java –version
```  

If not install a jre in your local machine(jre is enough for this, if you want to develop something in java related platform then jdk is needed for eg, android studio)  

```
$sudo apt-get update  
```
```
$sudo apt-get install openjdk-6-jre-headless
```

**Configuring the browser to use burp suite**

Inorder to intercept the outgoing traffic we need to integrate burp suite with browser. We can manually configure each time to make the browser listen to burp suite, but it tedious and time consuming.  

Preferences -> Network settings -> select manual proxy configuration

![network](https://user-images.githubusercontent.com/17383454/57189780-6e3b3c80-6f30-11e9-8b86-101ed41dd781.png)

Since burpsuite is sites in between the browser and the outside internet, you browser will show a warning message. Inorder to solve this you need to install Bupsuite CA certificate in your browser.  

![burp ca](https://user-images.githubusercontent.com/17383454/57189788-814e0c80-6f30-11e9-8219-d28cc92e0e3e.png)

Then import the downloaded certificate to your browser.
