---
title: Core Windows Process.
date: 2021-12-05 19:29:00 +/-TTTT
categories: [SOC, General]
tags: [soc]     # TAG names should always be lowercase
---
# Windows
In this post i worked on the windowsinternals and how the normal windows processes look like, so that we can identify between the normal and malicious processes on system.  

Windows is in one of the most used OS and there is a common belief on pentesters that they can easily understand the linux environment process and it was diffcult to understand about the windows(I heared about this thing from some of the persons breaked the OSCP exam, it might be difficult for them or i heared it wrong. **But i feel it in the same way**).  

Nowadays AV detection is not enough, so we soc analyst came here to identify the anomalies/processes which AV miss.  
I do closely worked with the AV signature team, from my observation if we didnt already have the malware or even a clever minor change in the existing malware code will not be captured by the existing signature if it was poorly written.    


# Task Manager  
Most of the windows users were already aware of taskmanager. So i will go deep into that.  
From task manager, Each process falls into 1 of 3 categories (Apps, Background process, or Windows process).  

But as a analyse point of view, taskmanager has few limitations.
1. We cant directly view the parent process of a current process to identify the anamalies.
2. Few old/new variants of malware can hide from task manager

For example in the below screenshot from tryhackme lab, we do see that PID 384 is paired with a process named svchost.exe  

![Task Manager](https://drive.google.com/uc?export=view&id=1fsGYIiAYWL5rBvIR9Tn8O_6hRvziZ5X3)  


![Task Manager detailed view of path](https://drive.google.com/uc?export=view&id=12dmESvWmKVMuZEzpT7x9BpxnAXpLssOK)  
We can add extra fields in the task manager which can be found in the above picture.   


![Task Manager detailed view of path](https://drive.google.com/uc?export=view&id=1ax_3ekELJntn1_r4oWtVuYgAUEkLhIH_)   


Based on the above image, the PID for services.exe is 632. But wait, one of the svchost.exe processes has a PID of 384. How did svchost.exe start before services.exe? Well, it didn't. Task Manager doesn't show a Parent-Child process view.   

In some situations we cant use the **Process hacker and Process explorer**, which were well built to identify this parent process. So its better to get a hands on experience with task manager and tasklist, Get-Process or ps (PowerShell), and wmic   


# System   

PID of system process is always 4    

How to identify unusual behavior for this process in compromised machine

    A parent process (aside from System Idle Process (0))
    Multiple instances of System. (Should only be 1 instance) 
    A different PID. (Remember that the PID will always be PID 4)
    Not running in Session 0

# smss.exe  

smss.exe - Session Manager SubSystem (or) Windows Session Manager
This is responsible for creating new sessions  
This is the first user-mode process created by kernel.  

It starts the kernel mode and user mode of windows-subsystem  
This subsystem includes
1. win32k.sys(kernel mode)
2. winsrv.dll(user mode)
3. csrss.exe(user mode)

Smss.exe starts csrss.exe and wininit.exe in session 0  - Isolated windows session for operating system  
csrssexe and winlogon.exe for session 1 - user session  


Reference:  
https://tryhackme.com/room/btwindowsinternals  
https://en.wikipedia.org/wiki/Task_Manager_(Windows)  
https://forums.malwarebytes.com/applications/core/interface/file/attachment.php?id=241465  
