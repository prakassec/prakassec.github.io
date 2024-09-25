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

