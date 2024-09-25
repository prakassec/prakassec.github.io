---
title: Reverse Engineering 2
date: 2024-09-25 23:26:00 +/-TTTT
categories: [SOC, MALWARE]
tags: [malware]     # TAG names should always be lowercase
---

**Debugging Running Process**  

GDB has capability to attach to the running process and debug it.  

From the perspective of malware analysis, attaching GDB (or a similar debugger) to a running process can provide deep insights into how a piece of malware operates.   

1. Dynamic Analysis (Behavioral Analysis)
   
   Attaching GDB to a live process allows you to perform dynamic analysis, which involves running the malware and observing its behavior in real-time.  
   
2. Memory Forensics
   
   By attaching GDB, you can analyze the memory layout of a running malware process(encrypted strings, how the malware allocates and uses memory, presence of malicious shellcode)  

3. Monitoring Process Injection  

   Malware often injects malicious code into other processes (process injection) to hide its presence or escalate privileges.  
   By attaching GDB we can monitor how the injection were performed, which system calls are used, how the injected code behaves in the target process.  

![Reverse engineering](https://drive.google.com/thumbnail?id=1IALJ3AvDLIXM9iZ-Aml0-2RbW2Khq0I6&sz=w700)  


![Reverse engineering](https://drive.google.com/thumbnail?id=1h5F8ewUh3YEs0cOUVqz2sjtTGPqZ5ugB&sz=w700)  


![Reverse engineering](https://drive.google.com/thumbnail?id=1uKZj99j3Xm5FoAlzM4kolD4L8Qy0phRA&sz=w700)


**Program with Multiple Threads**  

GDB has capability to deal with multiple threads of a process.  

It can be very useful when you're debugging multi-threaded applications or malware that uses threads for concurrency. In a multi-threaded environment, GDB allows you to inspect, control, and manipulate individual threads within a running process.  

1. Thread Identification and Listing

   GDB can identify and display all the threads running within a process. Each thread has a unique identifier (ID) that can be used to switch between and control threads.

2. Inspecting Thread-Specific Information

   Once you’ve switched to a thread, you can inspect its call stack and local variables. Each thread has its own stack, so the backtrace and variables can be different for each thread.

3. Inspecting Deadlocks and Race Conditions

   If the application or malware involves deadlocks or race conditions, GDB can help investigate by examining the call stacks of all threads. You can switch between threads and inspect their state to determine which threads are waiting for locks or resources and identify potential synchronization problems.


```gcc sample.c -g -pthread -o sample```

Above command line compile a C program with specific options that enable debugging and multi-threading support.  

-pthread tells GCC to include support for POSIX threads (often referred to as pthreads), which is a threading library used in many Unix-like systems, including Linux.  


Run the program in the background to keep interacting with the command prompt. This can be accomplished by using & character.  

![Reverse engineering](https://drive.google.com/thumbnail?id=1yZ4ZYgr4lVFrT747iRmc5KKTJr7xX_XT&sz=w700)  

![Reverse engineering](https://drive.google.com/thumbnail?id=1g61Hq1o7UhRNGmoIYK5IWRFPgwHN1HNz&sz=w700)


![Reverse engineering](https://drive.google.com/thumbnail?id=1FznTzMgaF0t521JpXJyLbYlzX2UEPgvv&sz=w700)


