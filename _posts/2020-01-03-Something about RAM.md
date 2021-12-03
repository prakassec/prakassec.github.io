---
layout: post
title: Something about RAM
date: 2020-01-03 17:49:00
desc: Basic info about RAM
---
**Why this post**  

When i planned to upgrade my Ram i faced some issues like what is my ram type, is it suitable for my motherboard, how many slot will be in my motherboard.  
Yes it is mandatory before you upgrade RAM else you will be called as spendthrift by your mother.(yah i find this word from google which means "a person who spends money in a way that waste it")  

Okay we can see about what are details you should know before buy a new RAM.  

As a traditional way we will see what is the abbreviation of RAM - Random Access Memory  
As the name itself indicate we can access the memory randomly without touching the preceding byte.  
Also some time you can hear the acronym like DDR,DRAM/SDRAM  


**DDR** - Double Data Rate Ram  
Two data transfer / clock cycle  
the higher number of pulses per second, the faster the computer processor will be able to process information  

**DRAM**- Dynamic Random Access Memory.  
It will be refreshed at a continuous amount of time.  
Most of the RAM in modern computers are Synchronous DRAM.  
Example : DDR3  
Size: Vary from 2GB to 32GB or more  
Where you can find : Present on motherboard.  

![DDR](https://user-images.githubusercontent.com/17383454/71723209-d80a3e00-2e51-11ea-8acb-f29098c41170.png)  

**SRAM** - Static Random Access Memory  
While DRAM is used to main memory. SRAM is used for system cache  
Since the memory in SRAM is not refreshed like DRAM(It will refresh thousands of time) it is faster than DRAM.  
Example : L2 and L3 cache in a CPU  
Size : 1MB to 16MB  
Where you can find : Present on Processors or between Processor and Main Memory.  

![SRAM](https://user-images.githubusercontent.com/17383454/71723223-e48e9680-2e51-11ea-8c5c-07d2c888433a.png)  

In some cases one cannot upgrade RAM without upgrading a Motherboard  

Using the command ```$ sudo dmidecode``` it is possible to know about your processor type, number of slot you have and other system related informaions.  
You need sudo access to perform this operation.  

![slot](https://user-images.githubusercontent.com/17383454/71723500-dd1bbd00-2e52-11ea-93c3-1a4b589b3481.png)
