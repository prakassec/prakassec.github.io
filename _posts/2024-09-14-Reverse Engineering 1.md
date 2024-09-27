---
title: Reverse Engineering 1
date: 2024-09-14 13:05:00 +/-TTTT
categories: [SOC, Malware]
tags: [malware]     # TAG names should always be lowercase
---

![Reverse engineering](https://drive.google.com/thumbnail?id=1kJ5c2RHXj8BzwcOCVgOLG9mBucfQT4A6&sz=w500)  


**GDB (GNU Debugger)**  

Debugging tool for programs written in languages like Ada, C, C++, Objective C and Golang   
Analyze the behavior of a program at runtime, inspect variables, control program execution, and identify bugs or errors.  
First step in learning reverse engineering is to familiarize with the basics of assembly language and to learn how to use the debuggers to analyze an executable.  


**Compilation**  

During the compilation lets compare the two different ways. One in normal way and another in the gcc while enabling the debug symbols.  
From the size of file output, file with debug enabled will be having more size than the other.  

![Reverse engineering](https://drive.google.com/thumbnail?id=187p96z9h-hiA6rQjnVxlShfzpDYA7dAM&sz=w700)  

![Reverse engineering](https://drive.google.com/thumbnail?id=1TzqqlHK9Heb582nk3HZriSusA1RVqCRW&sz=w700)  

Compiling a C file with GCC while enabling debug symbols means adding specific compiler flags that instruct GCC to include extra information in the generated executable.  It will help us to  

1. Identify line numbers from the source code.  
2. Map variables in the code to memory addresses.  
3. Track the function call stack.

![Reverse engineering](https://drive.google.com/thumbnail?id=1LKylko5ayfzCYkRdqYGpD8mTVlS3nOK-&sz=w700)  

![Reverse engineering](https://drive.google.com/thumbnail?id=1WyKVM42EbY4QANw157-r_QZ1zwZv14RR&sz=w700)  

**Passing Arguments**  

Passing arguments to a program in gdb (GNU Debugger) is done using the --args option or through the run command after starting gdb  

![Reverse engineering](https://drive.google.com/thumbnail?id=1F2SIKiPhSraq_XvqPq2TQUa0yHgGVqV6&sz=w700)  

![Reverse engineering](https://drive.google.com/thumbnail?id=1GpN1z7s1JHCSN_GDOEoWqYfbbpvgcUYN&sz=w700)  

**Program’s Environment variables**  

Some programs call custom binaries and use environment variables in their operation. And, GDB provides a way to define these for programs under analysis.  

![Reverse engineering](https://drive.google.com/thumbnail?id=1qIKSInYUiEhifiNLC2koLDYEQPEhCAUO&sz=w700)  

We can observe that the program takes two arguments and returns the sum of both. It also calls a binary “mydate” (which is present in the same directory and uses environment variable “author”.  

Since environment variable results in error, it also affects the mydata binary.  
To fix this problem, the path of present working directory needs to be added to path variable.  
The program was able to locate mydate now. However, it is still not able to read the environmental variable “author”.  
After we set the author we can get the expected result  



![Reverse engineering](https://drive.google.com/thumbnail?id=1maCMoiVUYpszlTQk3NVCTNTnM4TPnNE2&sz=w700)  







