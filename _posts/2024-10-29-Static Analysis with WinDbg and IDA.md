---
title: Static Analysis with WinDbg and IDA
date: 2024-10-29 11:27:00 +/-TTTT
categories: [SOC, Malware]
tags: [malware]     # TAG names should always be lowercase
---

![Binary reversing](https://drive.google.com/thumbnail?id=1yuNgVGm8cMuG7lWMDGMWs71F3x38Wz2_&sz=w700) 

While examining compiled executables from low-level languages like C or C++ we often do not have access to the source code. In this case, an analysis of the binary can help us understand the structure, content, and flow of a binary executable itself  

A debugger like WinDbg8 for example, can help us to display instructions in plain ordered assembly  

Using WinDbg and IDA in binary analysis  

Address Space Layout Randomization (ASLR) can cause every binary to have a different address when executing, we cannot always know the base address of an executable in advance. However, if we can gather this information from our debugging session and pass it to IDA, we can synchronize both pieces of information.  

Address Space Layout Randomization (ASLR) is a security technique that places program components in random memory locations each time it runs. This randomness makes it much harder for attackers to predict where critical parts are, reducing the chance of successful attacks.  

![Binary reversing](https://drive.google.com/thumbnail?id=1_gQWbyc0Y77FPDdCoEQ0jziUjWMzqqsg&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1tonvFgEcJBJ_6lExXhFVPEqhZKs5SQ6i&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1J0rfKRsbPzFXSn9ga3FMCjcjZQ2sWmYE&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1JQ-xw0RXLxPjrGrITkyYonGPAUYK0ZF6&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1_RP4uu39ioogiU4lwfgbs9o0n0JSUmWx&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1X6hjvtpLvi0SVA0tuYFret_8093AW65q&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=19DnDcF7wjSZmGvxo19w4tvQ46nPWqsp9&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=1KEfiOuvZvEH7WSh4xmiw7kQIr2BKdNKv&sz=w700) 

![Binary reversing](https://drive.google.com/thumbnail?id=17W7FEu8it06Wi9jj_7ByhollChfohJHn&sz=w700) 
