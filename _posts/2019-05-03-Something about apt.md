---
layout: post
title: Something about apt
date: 2019-05-03 19:39:12
categories: Linux 
desc: Basic information about apt command
---
**Hello,** (I hope there is someone in the world reading this post)

One fine day, when i try to install some application for my ubuntu machine. I do an update and try to install that specific application.  
Then it strikes my mind why the hell that i need to update my machine each time before installing a new application.  
That results in creation of this post.

**apt-get update vs apt-get upgrade**

`Ubuntu` is a Debian based linux and it uses `dpkg` packaging system.   
`APT (Advanced Packaging Tool)` is used to interact with packaging system. It is userfriendly when compared to dpkg  
APT and apt are different  
There are various tool that can interact with APT to install and manage packages. apt is one such tool that interact with APT  

apt commands contains most widely used features from apt-get and apt-cache.  
apt command is more user-friendly than compared with apt-get  
For example : It shows number of upgradable packages, progress bar while installing a package.  
![Image of apt vs apt-get](https://user-images.githubusercontent.com/17383454/57142548-679ab100-6dda-11e9-9f03-0e21196edc45.png)

Each local ubuntu machine has a copy of list of packages that are in ubuntu's repository. During the time of installation of any application, apt-get first reads this list and founds a specific url to download the application that the user has intended.  

apt-get update first updates the copy of list of packages if it is changed in main repository.  
apt-get upgrade installs application depending on updated repository version.  

When you update the package there are 3 commands you will possibly encounter  
1. Hit - no change in the package version  
2. Get - there is change occured  
3. ign - ignored (This is not an error, no need to worry)  

However it is not necessary to update the repository each time, if you knew that there is no change occured in the main repository.  
Actually they update their repository because of bugs in the application.   
