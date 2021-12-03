---
layout: post
title: Cross Site Scripting
date: 2020-01-07 21:42:00
desc: Intro about XSS
---
**XSS**

XSS is most common because of user input is validated or encoded.  
Using XSS it is possible to access cookie, session tokens, and other sensitive information of victim.  
Vector - Javascript, HTML, Flash and other type of code that the browser may execute.  

**Stored XSS** - Payload is permanently stored on the target server(DB,logs,comment field). When other user visit this data xss occur.   
**Reflected XSS** - Payload will trigger in the immediate HTTP response(Error message, Search Result). Payload is delivered to victim via email, some other website.  
**DOM-based XSS** - Payload trigger in client-side code rather than server-side code.  

**XSS Prevention**  

**1.`X-XSS-PROTECTION` Header**    

Content-Security-Policy itself disabled the inline javascript but this header can be used to provide xss prevention on older web browser that dont support CSP.  

`X-XSS-Protection: 0`   XSS filter will be in disabled state    
`X-XSS-Protection: 1`   If xss is detected browser will sanitize the page    
`X-XSS-Protection: 1; mode=block`   Broswer will not render the page      
`X-XSS-Protection: 1; report=reporting-uri`  Browser will sanitize and report the violation   

**2.`Content-Security-Policy` Header**  

X-Content-Security-Policy is the older version of CSP  
`<meta>` can also be used to configure CSP  

CSP allows scripts only from whitelisted domain.  
When domain want to completely prevent XSS can disallow script execution.  

`Content-Security-Policy: default-src 'self' `
Content load from own origin, subdomain will be excluded  

  
`Content-Security-Policy: default-src 'self' *.trusted.com     `
Content from oring and subdomain will be allowed. It doesnt need to be same domain  

  
`Content-Security-Policy: default-src 'self'; img-src *; media-src mp4.com mp3.com; script-src uniq.com   `
Image can be loaded from any site, media is restricted, script will loaded from specific site  

  
`Content-Security-Policy: default-src https:ssl.com   `
site content will be loaded over https  
