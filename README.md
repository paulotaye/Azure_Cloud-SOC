
# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/user-attachments/assets/9cabda0f-adce-4add-a749-00be3ad75033)


## Introduction

In this project, I designed and implemented a mini honeynet within Azure. I configured various resources to ingest log sources into a Log Analytics workspace, which was then integrated with Microsoft Sentinel. This setup enabled the creation of attack maps, triggering of alerts, and incident management.

I conducted an initial security assessment by measuring key security metrics in the unsecured environment over a 24-hour period. After applying security controls to harden the environment, I performed a second round of measurements over another 24 hours. The results, which are presented below, highlights the impact of the security enhancements.

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Network Flows detected in the honeynet)

## Architecture Before Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/aBDwnKb.jpg)

## Architecture After Hardening / Security Controls
![Architecture Diagram](https://i.imgur.com/YQNa9Pp.jpg)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

**"BEFORE" Metrics:**<br>
Initially, all resources were deployed with exposure to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls left wide open, while all other resources were configured with public endpoints visible to the internet, with no utilization of Private Endpoints.

**"AFTER" Metrics:**<br>
For the "AFTER" metrics, the Network Security Groups were hardened by blocking all traffic except for connections from my admin workstation. Additionally, all other resources were secured using built-in firewalls and Private Endpoints.

## Attack Maps Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/807f8244-8c27-4323-a522-a69cd7e3aa90)<br>
![image](https://github.com/user-attachments/assets/9681aac8-207f-4c9e-9443-a4f0294cfc6b)<br>
![image](https://github.com/user-attachments/assets/d82cbc47-355e-4fc7-a55e-f04018ea2fa1)<br>

## Metrics Before Hardening / Security Controls

The table below presents the metrics collected over a 24-hour period in the unsecured environment:

Start Time: 2024-08-06n 17:18:19
End Time: 2024-08-07 17:18:32

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 36,908
| Syslog                   | 55
| SecurityAlert            | 1
| SecurityIncident         | 145
| AzureNetworkAnalytics_CL | 382

## Attack Maps Before Hardening / Security Controls

```All map queries returned no results, indicating that no instances of malicious activity were detected during the 24-hour period following the implementation of the hardening measures.```

## Metrics After Hardening / Security Controls

The table below presents the metrics collected over a 24-hour period, but after appling security controls to the environment:
Start Time: 2024-08-15 16:12:35
Stop Time:	2024-08-16 16:15:55

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 10,730
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was set up in Microsoft Azure, with log sources integrated into a Log Analytics workspace. Microsoft Sentinel was utilized to trigger alerts and generate incidents based on the ingested logs. Metrics were initially measured in the unsecured environment, followed by a second measurement after applying security controls. The significant reduction in security events and incidents post-hardening highlights the effectiveness of the implemented security measures.

It is important to note that if the network resources had been heavily utilized by regular users, it is likely that more security events and alerts would have been generated during the 24-hour period following the implementation of the security controls.
