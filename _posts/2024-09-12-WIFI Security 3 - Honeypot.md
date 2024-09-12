---
title: WIFI Security 3 - Honeypot
date: 2024-09-12 13:34:00 +/-TTTT
categories: [VAPT, WIFI]
tags: [vapt]     # TAG names should always be lowercase
---

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1yloy8_XS5vU55ZmpYmJShA_YrC0fHi0H&sz=w500) 

**WEP honeypot**  

Its type of decoy wireless network designed to attract and detect malicious activities, typically targeting attackers who exploit weak security protocols.  
Since the WEP is an vulnerable encryption, attackers will try to connect to it easily. By which we can understand about their attack tactics.  

**DEMO**

Lets create a WEP honeypot using Hostapd and lure the client to connect to it.  

Hostapd  

Software application used to create and manage wireless access points on Linux-based systems.  
We can convert the computer to Access Point (AP) turning it to wireless router or hotspot.  

1. Lets check for the list of available Wifi interfaces on the machine. And from this we can see there were 2 interfaces present  
   `root@root: iw dev`  
   
   
   ![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1nqaAoZ7eyMn1KPDrnBdmLM-fZ2ehAfgD&sz=w700)  

3. Following command will capture and display information about nearby Wi-Fi networks and devices in monitor mode on the wireless interface wlan0  
   `airodump-ng wlan0`  
   
   ![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=13Vbz9Fq6LqWQhipeaYFOn6ngQJu_VrZa&sz=w700)  

   In this we can see that 4 clients are tyring to probe to connect to the network. So we can create an honeypot and let the clients to connect to the access point.  
   This can be achieved by trial and error method for all at once.    

4. Here we are creating an hostapd configuration for a WEP network for the SSID “Coffee-Shop-WiFi”. If we didnt got any user connected to it, then we can impersonate the other SSID which identified in the previous step  

   ![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1VTXi2__GeaTxUIzx_J2PVD5yvt2YD1Tq&sz=w700)  

5. Then we are trying to configure the hostapd configuration for the SSID “hostel-A”. And from that we can see that the client will connect to the network.

   ![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=17Vabec_udmw-1AvR5K8e-RmKyKikGPTW&sz=w700)  

   
   
