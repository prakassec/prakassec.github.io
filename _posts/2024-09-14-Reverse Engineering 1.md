---
title: Reverse Engineering 1
date: 2024-09-14 13:05:00 +/-TTTT
categories: [SOC, MALWARE]
tags: [malware]     # TAG names should always be lowercase
---

![Reverse engineering](https://drive.google.com/thumbnail?id=1kJ5c2RHXj8BzwcOCVgOLG9mBucfQT4A6&sz=w500)  


GBD (GNU Debugger)  

Debugging tool for programs written in languages like Ada, C, C++, Objective C and Golang   
Analyze the behavior of a program at runtime, inspect variables, control program execution, and identify bugs or errors.  
First step in learning reverse engineering is to familiarize with the basics of assembly language and to learn how to use the debuggers to analyze an executable.  


Compilation  

During the compilation lets compare the two different ways. One in normal way and another in the gcc while enabling the debug symbols.  
From the size of file output, file with debug enabled will be having more size than the other.  

![Reverse engineering](https://drive.google.com/thumbnail?id=187p96z9h-hiA6rQjnVxlShfzpDYA7dAM&sz=w700)  

![Reverse engineering](https://drive.google.com/thumbnail?id=1TzqqlHK9Heb582nk3HZriSusA1RVqCRW&sz=w700)  

Compiling a C file with GCC while enabling debug symbols means adding specific compiler flags that instruct GCC to include extra information in the generated executable.  It will help us to  

1. Identify line numbers from the source code.  
2. Map variables in the code to memory addresses.  
3. Track the function call stack.  

