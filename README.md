<h1>Simulated LIVE Cyber Threat Monitoring with Azure</h1>

<h2>Description</h2>
<p align="center">
This project consists of building a honeypot virtual machine using Azure in order to simulate cyber attacks in real-time. The skills used in this project include Microsoft Azure cloud, Microsoft Sentinel, and threat monitoring. 
<br />
<br />

<img src="https://i.imgur.com/MMVkp80.png" height="40%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>Objective</h2>

The objective of this fun project was to conduct threat monitoring using a honeypot virtual machine designed to mimic a legitimate desktop but was intentionally left insecure. This setup attracted cyber attacks, which allowed me to analyze them and where they were coming from. By disabling the firewall on the honeypot VM, I gained insights into its critical role in preventing unauthorized access to our networks.

<h2>Technology Used </h2>

- Windows 10 (22H1)
- Microsoft Azure 
- Microsoft Sentinel (SIEM)
- Virtual Machine
- Terminal (MacOS command-line)
- Microsoft Remote Desktop
- Microsoft Defender for Cloud
- PowerShell

<h2>Observations</h2>

<p align="center">
  <br/>
<img src="https://i.imgur.com/X7l5TzJ.png" height="40%" width="80%" alt="Disk Sanitization Steps"/>
<br />
After letting the virtual machine to run for a few hours, I observed several key findings. First, there were many failed attempts at logging in all over the world. Russia, by far had the most, at 68%, but Asia and the United States also had noticeably high numbers. Second, many of the hackers trying to brute force their way in used 'admin' in their username guess. Third, these security events only happened after the firewall was turned off and only got worse from there. 

<br />
<br />
<h2>Conclusion</h2>

In conclusion, I created a honeypot using Microsoft Azure cloud, where I could also collect the logs. After inputting the logs in the SIEM, I was able to view in more detail the security events. Firewalls are critical in cybersecurity because without them, threat actors were able to continuously try to infiltrate the honeypot. Noticeably, the tactics that the threat actors used also became obvious and helped shed further light on the need for security controls, such as changing default usernames and passwords and using password complexity, as well as multifactor authentication. 


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
