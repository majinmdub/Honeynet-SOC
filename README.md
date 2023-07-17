# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/6jp3IxJ.png)

## Introduction

It's a pleasure to welcome you to an intriguing project as we immerse ourselves in the expansive domain of cybersecurity. In this stimulating undertaking, I have meticulously crafted a captivating miniature honeynet utilizing the capabilities of the Azure platform. This state-of-the-art infrastructure facilitates the aggregation of log data from a variety of resources, which are subsequently funneled into an interactive Log Analytics workspace. From there, we harness the capabilities of Microsoft Sentinel, a leading-edge security tool, to construct visually compelling attack maps, activate relevant alerts, and generate comprehensive incident reports.

## Objective

Our main goal here is to set up some purposely vulnerable virtual machines within Azure's tough infrastructure. This is a bit like putting out bait to attract cyber-attacks. But instead of just stopping the attacks, we get to study them, learning how the attackers work and how we can handle and fix any issues they throw our way.

So, what's the big game plan? We'll be measuring security metrics within this not-so-secure environment for a solid 24 hours. But don't worry; we're not stopping the fun there! After that, we'll toughen things up by adding robust security controls, and then we're in for another exciting 24 hours. Get set for some amazing results as we dive into the following exciting metrics:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

Get ready for a rollercoaster ride as we dig into some fascinating finds and breakthroughs in our mission to beef up cybersecurity. So, let's jump into this adventure together, fueled by our shared dedication to making the digital world a safer place.

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/7ZaD7ej.png)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/To6V6XO.png)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 Windows, 1 Linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed and exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources were deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

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

I'm excited to give you a rundown of a recent project I wrapped up, where I built a mini honeynet using the power of Microsoft Azure. We were super careful about weaving together log sources into a Log Analytics workspace and used Microsoft Sentinel to help with real-time alerts and making incident reports.

We kept a sharp eye on our metrics, both before and after we beefed up our security in the initial not-so-secure environment. What really popped was the major drop in security events and incidents once we got those controls up and running. It just goes to show they really do their job.

However, an interesting observation was that if the network resources were frequently accessed by regular users, we could have potentially seen an uptick in security events and alerts in the first day after implementing the security controls.

These insights could be valuable for future cybersecurity strategies.
