---
title: Core Windows Process
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

**PID of system process is always 4**      
PID for other process will be assign at random  
System process is home for special kind of threads that runs only in **kernel-mode**

>
Windows has two modes: `usermode and kernel mode`   
## Usermode  
Application run in usermode and os components run in kernel mode  
Each application will allocate with private virtual address space and private handle table  
So one applicatin cant alter other and if it crashed it will limited to that only  

## Kernel mode  
Few drivers run in usermode and other run in kernel mode  
Single virtual address space is shared by all drivers  
If a drivers a wrong data on virtual address space it will also impact other drivers  


![User mode and kernel mode-from ms blog](https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/images/userandkernelmode01.png)  


How to identify unusual behavior for this process in compromised machine  

![Task Manager detailed view of path](https://drive.google.com/uc?export=view&id=1KpTGvwWGqQFqyHUF8MG5dAI8Ja2XfluS)   
system on process hacker  

![Task Manager detailed view of path](https://drive.google.com/uc?export=view&id=1zugxocLhZbpbuuNXw5O5Cq_lu7nhFg-J)   
system on process explorer  


1. A parent process (aside from System Idle Process (0))
2. Multiple instances of System. (Should only be 1 instance) 
3. A different PID. (Remember that the PID will always be PID 4)
4. Not running in Session 0

# smss.exe  

smss.exe - Session Manager SubSystem (or) Windows Session Manager
This is responsible for creating new sessions  
This is the first user-mode process created by kernel.  

It starts the kernel mode and user mode of windows-subsystem  
This subsystem includes
1. win32k.sys(kernel mode)
2. winsrv.dll(user mode)
3. csrss.exe(user mode)

Smss.exe starts `csrss.exe and wininit.exe` in session 0  - Isolated windows session for operating system  
`csrss.exe and winlogon.exe` for session 1 - user session  

Session 0  
![session 0 tree](https://drive.google.com/uc?export=view&id=1ls3A3nyZJcywM5sMKHjHfLAXKmW7887K)    

![session 0 prop](https://drive.google.com/uc?export=view&id=19gwnvKxDYevZYEtX-Rh8Q9dB8O9bII-f)  

Session 1  

![session 1 tree](https://drive.google.com/uc?export=view&id=1DAEl6YiUd30Q5bp7aNRLFZ6Hwfi5jmV0)  

![session 1 prop](https://drive.google.com/uc?export=view&id=1uT0RKjyYdeSsOSPSStcMmpaI2-nvGvQJ)   


properties of smss.exe under normal circumstance

![smss.exe prop](https://drive.google.com/uc?export=view&id=1Dzwf0L7a5JGtepdO9k5BTLiMkMIBcdW2)     

Unusual behaviour of smss.exe  

1. A different parent process other than System(4)
2. Image path is different from C:\Windows\System32
3. More than 1 running process. (children self-terminate and exit after each new session)
4. User is not SYSTEM
5. Unexpected registry entries for Subsystem 


# csrss.exe  

csrss.exe - Client Server Runtime proceSS  
User-mode side of windows sub-system  
It will always run and it is a critical one  
As mentioned above csrss.exe is a child process of smss.exe but it will self-terminate once it makes the child process.  

![csrss.exe comp](https://drive.google.com/uc?export=view&id=1FV7d3c3IPElMQw0IHIuQKzggdYywiZbI) 

Unusual about csrss.exe  

1. An actual parent process. (smss.exe calls this process and self-terminates)
2. Image file path other than C:\Windows\System32  
3. Subtle misspellings to hide rogue process masquerading as csrss.exe in plain sight
4. User is not SYSTEM  

# wininit.exe  

wininit.exe - Windows Initialization Process  
It launches  
1. services.exe(Service Control Manager)  
2. lsass.exe(Local Security Authority)  
3. lsaiso.exe within session 0  

lsaiso can be shown if credential guard and key guard were enabled  
![wininit.exe comp](https://drive.google.com/uc?export=view&id=1eBgBdos0MTj6reZAL9jSd33TK5vpIssf) 

Unusual about wininit.exe  

1. An actual parent process. (smss.exe calls this process and self-terminates)
2. Image file path other than C:\Windows\System32
3. Subtle misspellings to hide rogue process in plain sight
4. Multiple running instances
5. Not running as SYSTEM


## services.exe
Responsible for handling system services - loading, interacting, start/end services  
This process also loads device drivers marked as auto-start into memory  
This process is parent to other key process - svchost.exe, spoolsv.exe, msmpeng,exe, dllhost.exe  

![services.exe prop](https://drive.google.com/uc?export=view&id=1wE8zAYoyuuRt0lhXbkvBDRlRrX1Bh7G3)   

Unusual behaviour of services.exe  

1. A parent process other than wininit.exe
2. Image file path other than C:\Windows\System32
3. Subtle misspellings to hide rogue process in plain sight
4. Multiple running instances
5. Not running as SYSTEM

### svchost.exe  

Responsible for hosting and managing windows services  
Services running in this process are implemented as DLL  

![svchost gif](https://drive.google.com/uc?export=view&id=1hhuY5q4q6d0Rp2OA5xzfiU6CjqkvB8A-)    

Unusual behaiour of svchost.exe  

1. A parent process other than services.exe
2. Image file path other than C:\Windows\System32
3. Subtle misspellings to hide rogue process in plain sight
4. The absence of the -k parameter  

# lsass.exe  

LSASS - Local Security Authority Subsystem Service  
Enforcing the security policy on system  
Verfies users login, handle password chanegs, create access token, write security log  


Unusual behaviour of lsass.exe   

1. A parent process other than wininit.exe
2. Image file path other than C:\Windows\System32
3. Subtle misspellings to hide rogue process in plain sight
4. Multiple running instances
5. Not running as SYSTEM

# winlogon.exe  

It Handling: 
1. Secure Authentication Sequence(SAS)  
2. Locking screen, running screensaver  

Unusual behaviour of winlogon.exe

1. An actual parent process. (smss.exe calls this process and self-terminates)
2. Image file path other than C:\Windows\System32
3. Subtle misspellings to hide rogue process in plain sight
4. Not running as SYSTEM
5. Shell value in the registry other than explorer.exe


# explorer.exe  
Handles user access to file/folder, start menu, taskbar etc  


Unusual behaviour of windows explorer  

1. An actual parent process. (userinit.exe calls this process and exits)
2. Image file path other than C:\Windows
3. Running as an unknown user
4. Subtle misspellings to hide rogue process in plain sight
5. Outbound TCP/IP connections


Reference:  
https://tryhackme.com/room/btwindowsinternals  
https://en.wikipedia.org/wiki/Task_Manager_(Windows)  
https://forums.malwarebytes.com/applications/core/interface/file/attachment.php?id=241465  
https://docs.microsoft.com/en-us/windows-hardware/drivers/gettingstarted/user-mode-and-kernel-mode
