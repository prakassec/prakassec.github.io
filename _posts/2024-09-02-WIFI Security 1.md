---
title: WIFI Security 1
date: 2024-09-02 20:34:00 +/-TTTT
categories: [VAPT, WIFI]
tags: [vapt]     # TAG names should always be lowercase
---

![wifi security_intro pic](https://drive.google.com/thumbnail?id=16a8e0uLT5uw1oiJJj7jzjba3ddiXSvN7&sz=w500) 

**IEEE 802.11**  

Its the original WLAN standard. Every wireless card supports a specific 802.11 protocol  

Original 802.11 defines the 1 and 2 Mbit/s data rates over radio frequencies using Direct-Sequence Spread-Spectrum (DSSS) and Frequency Hopping Spread-Spectrum (FHSS). It is often called pure-802.11.  

GPS and Zigbee make use of DSSS whereas Bluetooth is known for using FHS  

Wi-Fi radios can either receive or transmit, but cannot do both simultaneously. This functional limitation is why we refer to Wi-Fi radio as half duplex  

IEEE 802.11 uses Carrier Sense Multiple Access with Collision Avoidance (CSMA/CA)  


**Terminology** 

beamforming  
streams  
Direct-Sequence Spread-Spectrum (DSSS)  
Frequency Hopping Spread-Spectrum (FHSS)  

**Antenna Diversity vs MIMO**  

Antenna diversity uses multiple antennas to improve the quality of a wireless link  
While antenna diversity selects the best (single) antenna to receive or transmit, MIMO splits the data into multiple streams and uses multiple antennas to send them. The receiver then combines the streams.  

**Wireless Networks**  

Some of the configuration that will be assessed during the penetration involves
1. Infrastructure
2. Wireless Distribution System - connect multiple APs without Ethernet cables
3. Ad-Hoc Networks
4. Mesh Networks
5. Wi-Fi Direct
6. Monitor Mode - Its not an architecture but a mode used by wireless cards that will help capture wi-fi frames.

**Wi-Fi Encryption**  

Wi-Fi works over radio waves, which means it is subject to eavesdropping and therefore, encryption has to be used to protect the transmitted data.  

Wired Equivalent Privacy (WEP) - Easily cracked under one minute  
Wi-Fi Protected Access (WPA) - Created by IEEE to improve the wi-fi security  

