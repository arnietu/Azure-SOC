# Building a SOC + Honeynet in Azure (Live Traffic)
![image](https://github.com/user-attachments/assets/5ccd8f31-aa78-4a23-adf6-d4c36c4c2ace)


## Introduction

In this project, I set up a mini honeynet in Azure and configured it to send log data from various resources into a Log Analytics workspace. Microsoft Sentinel then uses this data to create attack maps, trigger alerts, and generate incidents. I initially measured security metrics in an unsecured environment over a 24-hour period. After applying security controls to strengthen the environment, I measured the metrics again for another 24 hours. Below, I present the results of these metrics. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![image](https://github.com/user-attachments/assets/2aca2b31-1af6-4480-b11d-4f5d23aa44f8)


## Architecture After Hardening / Security Controls
![image](https://github.com/user-attachments/assets/593cbefb-4f23-48cd-8ca2-9eae6390ca7f)


The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were initially deployed and exposed to the internet. The Virtual Machines had their Network Security Groups and built-in firewalls completely open, and all other resources were deployed with public endpoints accessible from the internet—no private endpoints were used.

For the "AFTER" metrics, Network Security Groups were secured by restricting traffic to only my admin workstation, while all other resources were safeguarded by their built-in firewalls and protected using Private Endpoints.

## Attack Maps Before Hardening / Security Controls

![image](https://github.com/user-attachments/assets/304df2f1-2d03-491e-868a-7287eb49fe41)
![image](https://github.com/user-attachments/assets/c4d04c23-f083-4b0c-97d9-c870312d48f4)
![image](https://github.com/user-attachments/assets/5f98a6d9-a3ca-46e5-ac49-4ee1390d91c9)

## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 8/15/2024 9:19:36
Stop Time 8/16/2024 9:19:36

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 36842
| Syslog                   | 12378
| SecurityAlert            | 1
| SecurityIncident         | 321
| AzureNetworkAnalytics_CL | 1732

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 8/17/2024 22:29:21
Stop Time	8/18/2024 22:29:21 

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 0
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was set up in Microsoft Azure, and logs were collected into a Log Analytics workspace. Microsoft Sentinel was used to trigger alerts and create incidents based on these logs. Metrics were recorded in the insecure environment before applying security controls and again after implementing them. The results showed a significant reduction in security events and incidents, highlighting the effectiveness of the applied controls.

However, it's important to note that if the network resources had been actively used by regular users, it is possible that more security events and alerts might have been generated during the 24-hour period following the application of the security measures.
