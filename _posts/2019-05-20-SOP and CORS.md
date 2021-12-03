---
layout: post
title: SOP and CORS
date: 2019-05-20 12:29:00
categories: WebApplication
desc: About same origin policy and cross orgin resource sharing
---

When we visit a website you cant notice what are resources are fetched in backend.  
To find the list of resource used in the website you should monitor the network activity of that specifice website.  
This can be done by pressing F12 and then navigate to Network tab.  

![cors network tab](https://user-images.githubusercontent.com/17383454/67632536-9e094280-f8ca-11e9-8fbf-acd4ce9b221b.png)


In this case an website may request resources from different origin.  
If the origin are unchecked during resource fetching there is a high probability that site also fetch malicious code from outside origin.  


To prevent this browsers follows **SECURITY POLICIES**  

**1. Same Origin Policy**  

Same Origin Policy is very strict in nature i.e. An resource(such as when using XMLHttpRequest or <img> element) must interact with its origin only.  

**How it detects origin?**  
Protocol, Host, Port number  

Internet explorer only checks the Host, Protocol  

In multiple host environment say, to access the **resource.site.com** you first need to authenticate in **login.site.com**  
Hence in this case developer will set the document.domain to root of the domain on both site  

```document.domain = "site.com"```  

Which allows anything in **site.com** domain can access the DOM in the current page  
When an vulnerable page vul.site.com is hosted on internet then **resource.site.com** is vulnerable too.  
If a attacker successfully inject an payload to **vul.site.com** then he can also attack **resource.site.com**  

For security reasons browser restrict cross origin Http request initiated from scripts  

XMLHttpRequest and Fetch API follow this method. It can be overwritten with CORS header.  
XMLHttpRequest used to retrieve data from url without doing a full page refresh. It is used mostly in Ajax programming.  

However resource loading other host like images,scripts,stylesheets, iframes, forms are not subject to this limitation. For that we need additonal features to monitor those process. Hence we use CSRF Tokens.  

**When cross site request are must needed then we use CORS.**  


**2. CORS - Cross Origin Resource Sharing**  

CORS is an mechanism that uses additional HTTP headers to request broswer to give web application running on one origin to access resource from different origin.  




To prevent cross-origin write = Unguessable token in the request(CSRF Token)  
To prevent cross-origin read = Avoid using embedded resources  




https://resources.infosecinstitute.com/bypassing-same-origin-policy-sop/#gref  
