---
title: WIFI Security 1 - Intro
date: 2024-09-02 20:34:00 +/-TTTT
categories: [VAPT, WIFI]
tags: [vapt]     # TAG names should always be lowercase
---

![wifi security_intro pic](https://drive.google.com/thumbnail?id=16a8e0uLT5uw1oiJJj7jzjba3ddiXSvN7&sz=w500) 

Wi-Fi networks are often more exposed than wired ones, making them a prime target for attackers. It will be an serious threat to organisation, if the actors target the users personal and organsation routers. 

If you are wondering how it will impact the organiasation if the users personal router got compromised, in this case scenario attacker can drop the malwares directly to their endpoint devices which might be stealthy if the malwares were built perfectly. Also the chance of getting captured by the organisation's security perimeter is very less in this case.

**IEEE 802.11**  

Think of 802.11 as the framework that enables your devices to communicate wirelessly and reliably, no matter what brand or model they are. As new versions (like 802.11n, 802.11ac, or 802.11ax) come out Wi-Fi gets faster, more efficient, and can handle more devices at once.

802.11 is the original WLAN standard. Every wireless card supports a specific 802.11 protocol  

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

Lets deep dive into some of the traffic analysis from the pcap captured from the wifi traffic data betwen the end user and the access points

**DEMO**  
**Eviltwin attack**  

Attacker sets up a rogue Wi-Fi access point that mimics a legitimate one, often with the same name (SSID) as the real network. Lets use the following method to check the eviltwin detection attak from wifi pcap  

Using the LAN statistics feature of the wireshark, we can able to find the list of BSSID having more number of packets captured from the SSID. From the following screenshot we can see that the ec:22:80:c3:4a:68
is the highest number of packets towards the SSID PA_NET  

> **What is SSID and BSSID**   
> In simple terms SSID were the names we can find when connecting to the wifi endpoint, whereas BSSID is the accesspoint which delivers the traffic by interacting with the SSID  

![Eviltwindetection_startwithanhypothesis](https://drive.google.com/thumbnail?id=1dg5QInprH45UFChlkOTUTA8LHP1amDrO&sz=w700)  

Then we are tring to filter only the list of traffics related to the ec:22:80:c3:4a:68  

![Eviltwindetection_bssidfilter](https://drive.google.com/thumbnail?id=1gL_pPJXla3Yyv2IrFtiKGYe9YztKkYBM&sz=w700)  

To further have a detailed view we can use the following filter wlan.fc.type_subtype == 0x0008  

![Eviltwindetection_beaconfilter](https://drive.google.com/thumbnail?id=1tHOhXDCNcLtBNKBVDkj8EepKB4Ye4aMp&sz=w700)   

From the following screenshot we can see the anamoly of length. So from this we can confirm that there are two different interfaces with the same BSSID ec:22:80:c3:4a:68 

![Eviltwindetection_lengthanamoly](https://drive.google.com/thumbnail?id=1Use0FyXoWkpBztDUAHLLQgwkIvXklo4L&sz=w700)   


