# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/6jp3IxJ.png)

## Introduction

Welcome to an exciting project where we delve into the world of cybersecurity! In this endeavor, I have constructed a captivating mini honeynet within the Azure platform. This cutting-edge infrastructure allows us to collect log data from diverse resources and channel it into a dynamic Log Analytics workspace. Subsequently, we leverage the power of Microsoft Sentinel to create awe-inspiring attack maps, initiate alerts, and generate detailed incidents.

## Objective

Our primary goal is to deploy intentionally vulnerable virtual machines within Azure's robust infrastructure, strategically attracting and studying cyber attacks. Through this initiative, we gain invaluable insights into attackers' tactics and techniques, all while showcasing our proficiency in effectively responding and resolving identified issues.

Now, let's focus on our primary objective: measuring security metrics within an insecure environment over a concise 24-hour period. But the excitement doesn't end there! We go a step further by implementing robust security controls to fortify the environment, leading us into another thrilling 24 hours. Get ready to be enthralled by the outstanding results that await as we present the following captivating metrics:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

Prepare to be amazed as we uncover intriguing discoveries and advancements in our quest to enhance cybersecurity. Together, let's embark on this professional journey, driven by a commitment to safeguarding the digital landscape.

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/7ZaD7ej.png)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/To6V6XO.png)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![NSG Allowed Inbound Malicious Flows](https://imgur.com/ZjjOyHf.png)<br>
![Linux Syslog Auth Failures](https://imgur.com/mvn6dSt.png)<br>
![Windows RDP/SMB Auth Failures](https://imgur.com/65qCW96.png)<br>

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2023-05-08T00:47:48
Stop Time 2023-05-09T00:47:48

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 74681
| Syslog                   | 978
| SecurityAlert            | 9
| SecurityIncident         | 417
| AzureNetworkAnalytics_CL | 1374

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2023-05-10T03:56:35
Stop Time	2023-05-11T03:56:35

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 11847
| Syslog                   | 7
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

I'm delighted to share the summary of a recent project I completed, where a mini honeynet was built using Microsoft Azure. We meticulously integrated log sources into a Log Analytics workspace and employed Microsoft Sentinel to facilitate real-time alerts and incident creation.

We paid close attention to our metrics, both before and after applying our security controls in the initial insecure environment. What stood out significantly was the substantial reduction in security events and incidents after these controls were put into action. It's a testament to their effectiveness.

However, an interesting observation was that if the network resources were frequently accessed by regular users, we could have potentially seen an uptick in security events and alerts in the first day after implementing the security controls.

These insights could be valuable for future cybersecurity strategies.
