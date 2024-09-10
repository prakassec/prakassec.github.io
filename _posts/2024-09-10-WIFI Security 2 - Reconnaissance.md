---
title: WIFI Security 2 - Reconnaissance
date: 2024-09-10 14:18:00 +/-TTTT
categories: [VAPT, WIFI]
tags: [vapt]     # TAG names should always be lowercase
---

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1415Cf9Yw2EuSuq6jgITH73fs6vvkCor6&sz=w500) 

**Reconnaissance**

Wi-Fi reconnaissance is the process of identifying and exploiting wireless networks. Using reconnaissance we can identify the unauthorized access points (rogue APs) or malicious devices on a network.  

Passive Reconnaissance  

By observing beacon frames and probe requests, an attacker can map out access points, clients, and SSIDs (network names). Tools like wireshark, kismet can be used for this purpose  

Active Reconnaissance  

Using probing we can reach the access point and gather informations like signal strength, device manufacturer etc  
Deauthentication Attacks - Forcing the device off to observe their behaviour  

**DEMO**  

A dual-band monitor mode capable WiFi interface is present on the user machine. Lets use Airodump-ng and Horst to analyze the live WiFi traffic  

Lets start typing airmon-ng to check whether the airmon was present in the machine  

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1knS9h_eb4Jx3kxy2BtCbOyuQzHPOog3c&sz=w700)   

Again we are tyring to enable the monitor mode and listens on the channel 13 by setting itup in the interface
We sent 30 packets to the accesspoint, from this we can see that none of came back to the client. So it shows that we cannot transmit on channel 13  


![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1qyktwAbITpNJtAa3jrgbTk07f0o_11WX&sz=w700)   

That ok, but why we cant transmit on the channel 13. Lets explore it further  

From the screenshot we can see that channel 13 is having (no IR) which means it not having intial raidation. So we are not allowed talk first to the channel.

```
2467 MHz [12] (20.0 dBm) (no IR)  
2472 MHz [13] (20.0 dBm) (no IR)  
2484 MHz [14] (20.0 dBm) (no IR)    
```

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1eRlkBUn9y5zgHnLfMSgV7T2UwKLnkuTl&sz=w700)   

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1E_88YDFgnQ5Bgqt304c4BgESoGCOMTmj&sz=w700)  

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1jY6niAZsNqykcale-V5KM1iu0vs8XQdI&sz=w700) 

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1Rs3RbL_9e7bkpAEJEA8Yc2XetVbwNl2c&sz=w700) 

Using this command `root@root:~#  iw reg get` we can see that the channel 12,13 and 14 are in the passive-scan only. Hence we cant inject on those channels.

```(2457 - 2482 @ 20), (N/A, 20), (N/A), AUTO-BW, PASSIVE-SCAN```  

![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=1dk-Blj-vH0kO_DsRnYWgts4xoKGgtqSD&sz=w700) 






![wifi_security_reconnaissace](https://drive.google.com/thumbnail?id=16knsBlPoCbftraCgyxvgJl11TUeIu44I&sz=w700) 
