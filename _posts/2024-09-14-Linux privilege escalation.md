---
title: Linux privilege escalation 1
date: 2024-09-14 11:23:00 +/-TTTT
categories: [VAPT, Privilege escalation]
tags: [vapt]     # TAG names should always be lowercase
---  

![Linux Privilege Escalation](https://drive.google.com/thumbnail?id=1nIMK1FDAXIWsP9plB_pYse_LMZOFul7Q&sz=w500)  


**Linux Privilege Escalation**  

During an engagement, if we got the access for the low privilege user in the linux environment then it might be necessay to escalate our privilege to other user it might the user having similar access or to a high privilege user to avoid the detection and steathiness.  

1. Vertical Privilege Escalation (Elevation)
   
   A user with lower privileges (e.g., a regular user) gains higher privileges, such as administrative or root access.
   This could allow the user to perform system-level actions, modify sensitive files, or access restricted data.

2. Horizontal Privilege Escalation
   
   A user accesses another user’s privileges without involving their account in the system logs.


**Common Methods of Privilege Escalation in Linux**  

1. Sudo Misconfigurations    
2. SUID/SGID Executables  
3. Weak File Permissions  
4. Exploiting Crontab Jobs  
5. PATH Environment Variable Manipulation  
6. NFS Misconfigurations  
7. Password Reuse or Weak Credentials  
8. Exploit of Service Misconfigurations  

**DEMO TIME**  

**Exploiting Setuid Programs**  

Lets start with a small program which easily allows us to perform the privilege escalaton.  Vulnerable setuid programs on Linux systems could lead to privilege escalation attacks. In this exercise, we are using a regular user account and need to escalate the privileges to become root.   

`-rwsr-xr-x`  

First Character (-): This indicates the file type.  
 
> \- means it is a regular file.  
> d means it is a directory.  
> l means it is a symbolic link.  

Next Three Characters (rws): These are the owner (user) permissions.    

> r = read permission for the owner.  
> w = write permission for the owner.  
> s = setuid (set user ID) bit, which means that when this file is executed, it runs with the permissions of the file's owner (not the person who runs it). This is why it's s instead of x (execute), as it also sets the user ID.  

Next Three Characters (r-x): These are the group permissions.    

> r = read permission for the group.  
> \- = no write permission for the group.  
> x = execute permission for the group.  

Last Three Characters (r-x): These are the other (world) permissions.  

> r = read permission for others.  
> \- = no write permission for others.  
> x = execute permission for others.  

From the above concept lets check the following binary **welcome** is having the suid set or not.   

![Linux Privilege Escalation](https://drive.google.com/thumbnail?id=1Zc8lq44RWPaWCf0LH-tEUGlMg6VJJDDb&sz=w700)  

Observe that the welcome binary has suid bit set (or on). This means that this binary and its child processes will run with root privileges. Also from the strings analysis we can see that the welcome binary is calling the greeting binary.  

![Linux Privilege Escalation](https://drive.google.com/thumbnail?id=1HSrZzTWGYohi8qSCSH_qbH0sN7-l3Ds3&sz=w700)  

Delete greetings binary and then copy /bin/bash to its location and rename that to greetings.  


![Linux Privilege Escalation](https://drive.google.com/thumbnail?id=1wlJ0qG5nk5DvWe-KQiOKuoBMLMY4FZRR&sz=w700)  

By using this method we escalated the user account to root in the linux machine.  


