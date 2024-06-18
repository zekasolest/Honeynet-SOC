# Building a SOC + Honeynet in Azure (Live Traffic)
![Screenshot 2024-06-17 at 5 48 06 PM](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/76f412a5-a45c-49e8-9f4d-d424896b83ee)






## Introduction

In this project, I built a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Screenshot 2024-06-18 at 8 39 21 AM](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/a508ba74-6332-480d-ac95-c218ef4527d2)


## Architecture After Hardening / Security Controls
![AAHSC](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/a889906d-c136-48e2-89cf-a4c223f05179)



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
![Screenshot 2024-06-13 at 1 31 24 PM](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/85fadbd5-c810-4bcd-bf6b-18aeb6fe51d6)
![Screenshot 2024-06-13 at 1 32 40 PM](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/ca264aa1-3c18-4663-9a83-90beb16781b7)
![Screenshot 2024-06-13 at 1 33 48 PM](https://github.com/zekasolest/Honeynet-SOC/assets/36097391/0a2c773c-85f0-4f99-95ae-65e5aab9f5de)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-06-12 19:51:36
Stop Time 2024-06-13 19:51:36

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 16010
| Syslog                   | 3210
| SecurityAlert            | 3
| SecurityIncident         | 241
| AzureNetworkAnalytics_CL | 1984


## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-06-16 19:48:52
Stop Time	2024-06-17 19:48:52

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7577
| Syslog                   | 1
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
