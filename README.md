<h1>Simulated LIVE Cyber Threat Monitoring with Azure</h1>

<h2>Description</h2>
<p align="center">
In this project, I created a basic home Security Operations Center (SOC) in the cloud using a Microsoft Azure subscription. I deployed a virtual machine (VM) to act as a honeypot, intentionally opening it up to the public internet to attract cyber attacks. I then configured log forwarding to a central repository, connected it to a Security Information and Event Management (SIEM) system (Microsoft Sentinel), and used a geographic dataset to create a live map visualizing the locations of the attackers
<br />
<br />

<img src="HoneyPot Project.png" height="40%" width="60%" alt="Disk Sanitization Steps"/>
<br />
<br />

<h2>What I learned</h2>

- Cloud Infrastructure Provisioning: Setting up Azure Resource Groups, Virtual Networks, Subnets, and deploying Windows 10 Virtual Machines.

- Firewall Configuration: Managing cloud firewalls via Azure Network Security Groups (NSG) and disabling internal host firewalls (Windows Defender) to intentionally expose a system to the internet.

- Log Management & SIEM Integration: Establishing a Log Analytics Workspace as a central repository and configuring Microsoft Sentinel to ingest logs.

- Data Collection Rules: Using the Azure Monitor Agent to automatically forward Windows security events (specifically Event ID 4625: Failed Logon) from the honeypot to the SIEM.

- Log Analysis & Querying: Utilizing Kusto Query Language (KQL) to filter, parse, and extract meaningful data from raw security logs.

- Data Enrichment & Threat Intelligence: Importing customized watch lists to translate attacker IP addresses into geolocation data (country, city, latitude, longitude).

- Data Visualization: Creating a customized Sentinel Workbook to plot live attack data onto an interactive global map.

<h2>Technology Used </h2>

- Windows 10 (22H1)
- Microsoft Azure 
- Microsoft Sentinel (SIEM)
- Azure Virtual Machines
- Azure Log Analytics Workspace
- Microsoft Remote Desktop Connection
- Microsoft Defender for Cloud
- PowerShell
- Kusto Query Language (KQL)

<h2>Step-by Step Implementation</h2>

1. Set up the Cloud Environment:<br>
Created an Azure Resource Group to logically group all the components (virtual networks, VMs, etc.) for the SOC lab.

2. Deploy the Honeypot Virtual Machine: <br>
Provisioned a new Virtual Network and Subnet inside the Resource Group then
deployed a Windows 10 Virtual Machine onto the subnet with an fake name (e.g., "corpnet-East1") so attackers wouldn't realize it was a honeypot.

3. Disable Firewalls and Expose the VM: <br>
Navigated to the VM's Network Security Group (the cloud firewall) and deleted the default inbound rules.<br>
Created a new highly permissive inbound rule that allowed all traffic from any source, on any port, using any protocol to reach the VM.
Used Remote Desktop Protocol (RDP) to connect to the VM and opened wf.msc to completely disable the internal Windows Defender Firewall across all network profiles then pinged the VM from my local machine to verify it was fully discoverable on the public internet.

4. Create the SIEM & Log Repository:<br>
Created a Log Analytics Workspace in Azure to act as the central log repository then provisioned an instance of Microsoft Sentinel and attached it to the Log Analytics Workspace.

5. Configure Log Forwarding: <br>
In Microsoft Sentinel, installed the "Windows Security Events via Azure Monitor Agent" data connector.
Created a Data Collection Rule for the honeypot VM, which installed the Azure Monitor Agent extension on the machine.
Configured the rule to collect all security events and forward them to the Log Analytics Workspace.

6. Enrich Logs with Geolocation Data: <br>
Generated intentional failed RDP logons to observe Windows Event ID 4625 (failed logon) populating inside the Log Analytics Workspace.
Because standard Windows logs do not include geographic data, I downloaded a summarized GeoIP dataset containing network blocks, coordinates, cities, and countries and imported this spreadsheet into Microsoft Sentinel as a custom "Watchlist".

7. Build the Interactive Attack Map: <br>
Created a new Workbook inside Microsoft Sentinel to serve as the visualization dashboard. Wrote a custom KQL query that filtered for Event ID 4625, extracted the attacker's IP address, and cross-referenced it with the imported GeoIP Watchlist to resolve the latitude, longitude, and country of origin.
Configured the Workbook to output the query results onto an interactive heat map, automatically scaling the visual indicators based on the frequency of attacks originating from specific locations.

<h2>Observations</h2>

<p align="center">
  <br/>
<img src="Threat Activity Heat Map.png" height="50%" width="90%" alt="Disk Sanitization Steps"/>
<br />

The heat map highlights a few clear hotspots, with most of the activity coming from places like the Netherlands, Chile, the United States, and Brazil. Seeing so many events appear so quickly and from all over the world shows how much of this traffic is driven by automated scanners and bots that constantly sweep the internet. It’s a strong reminder that anything exposed to the public web gets noticed fast, even when it isn’t a real target. 

<br />
<h2>Conclusion</h2>

Building this cloud SOC was a fantastic, eye-opening experience that highlighted just how quickly threat actors discover and target vulnerable devices on the public internet. By intentionally stripping away the firewalls on my virtual machine, I was able to observe real-world brute-force attempts almost immediately, capturing thousands of failed logons in a surprisingly short amount of time.
Beyond just watching the attacks roll in, this project gave me practical, hands-on experience routing raw security logs through Azure's infrastructure and into a centralized SIEM. It was incredibly rewarding to take a massive database of raw security events and write the KQL queries necessary to map them against threat intelligence data, ultimately transforming meaningless IP addresses into a live, visual heat map of global attacks.
Ultimately, this project serves as a strong foundation for a cloud security environment. While this current setup focuses heavily on log ingestion, data enrichment, and visualization, a natural next step would be to build upon this framework by configuring automated analytic rules, generating alerts, and establishing a full incident response pipeline to actively mitigate these threats.


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
