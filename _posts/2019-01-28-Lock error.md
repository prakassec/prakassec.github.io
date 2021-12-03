---
layout: post
title: Lock error
date: 2019-01-28 21:08:00
categories: Linux
desc: Lock error message during package installation
---
When you started using ubuntu and tried to install some package you will came across the following error and got frustated. <br />  


Some of you may try to resolve this by surfing through some random sites and try to put the command which are mentioned in that site.  
I am taking to myself only.  
This is exactly what i do in most cases.  

So in this post i will try to teach myself what exactly this means by breaking down each and everthing.  

Lets break things down.  


This is the error which i mentioned previously  
```console
E: Could not get lock /var/lib/dpkg/lock - open (11: Resource temporarily unavailable)
E: Unable to lock the administration directory (/var/lib/dpkg/)
```

**Why in the world it should get locked?**  

This is simply means when you try to install a new package, there is some package trying to **updrade** 
or running in the background which might be launched by other users of the os.

*The way how package management tool on Ubuntu/Debian or any other Linux operating system works is that every time 
package installation or update is initiated, the package management tool, in this case apt or dpkg, 
creates a lock file `/var/lib/apt/lists/lock` or `var/lib/dpkg/lock` to prevent concurrent execution of another 
software installation or update process.*

**What causes it to lock?**  
There is chance that ubuntu tries to update automatically in the background.  
Solution is wait for it to complete.
You can also turn off the auto update of package in the background by the following method:

```console
$ sudo nano /etc/apt/apt.conf.d/20auto-upgrades
```

Once you have the file opened, switch off the Update-Package-Lists directive from **1 to 0**

**Finding the process and user who holding the lock?**  

1.Note the error message thrown in the terminal  
2.**$sudo fuser _Path of lock(see the error message )_**  
3.Using tha PID (which is found in step 2) find the user who causes the lock.  

```console
$ ps -p “PID”  -o  user,comm,args
```

**Unlocking the /var/lib/apt/lists/lcok**

>Warning: Do not forcefully remove the lock, if there is chance it can be done by itself. Let it do its work.  
>Force remove sometime cause harm to your system.

```bash
$ sudo kill -9 “PID”
```



