# Azure Honeynet & SOC Project: Real-Time Cybersecurity Simulation

![Cloud Honeynet / SOC](https://user-images.githubusercontent.com/65828628/236935173-6cb5f050-376a-4396-97aa-c147d9297f52.gif)

## Overview

This project establishes a small-scale honeynet on Microsoft Azure designed to attract global cyber attackers. The objective is to demonstrate effective security practices, incident response tactics, and the impact of environment hardening. The methodology involves the intentional deployment of vulnerable virtual machines to entice attackers and the utilization of Microsoft Sentinel to create attack maps, alerts, and incidents. A comparative analysis of metrics before and after implementing security measures is provided based on incidents recorded during a 24-hour period.

## Azure Components Utilized

- Azure Virtual Network (VNet)
- Azure Network Security Group (NSG)
- Virtual Machines (2x Windows, 1x Linux)
- Log Analytics Workspace with Kusto Query Language (KQL) Queries
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel
- Microsoft Defender for Cloud

## Initial Architecture

In the "BEFORE" phase, all resources were initially deployed without security measures, resulting in their exposure to the public internet. Virtual Machines, storage accounts, and databases had open public endpoints, leading to the creation of the following attack maps:

### NSG Allowed Inbound Malicious Flows
![Attack Map - NSG Allowed Inbound Malicious Flows](https://i.imgur.com/M59Gxh4.png)

### Linux Syslog Auth Failures
![Attack Map - Linux Syslog Auth Failures](https://i.imgur.com/csd4FkF.png)

### Windows RDP/SMB Auth Failures
![Attack Map - Windows RDP/SMB Auth Failures](https://i.imgur.com/yDwdstr.png)

### MSSQL Failures
![Attack Map - MSSQL Failures](https://i.imgur.com/kGEBo2B.png)

## After Security Enhancements

In the "AFTER" phase, security measures were implemented based on incidents observed during the 24-hour "BEFORE" phase:

- **Network Security Groups (NSGs):** Access was restricted to specific IP addresses.
- **Built-in Firewalls:** Unauthorized access within virtual machines was denied.
- **Private Endpoints:** Public endpoints for sensitive resources were replaced, limiting access to the virtual network.

## Post-Security Attack Maps

After implementing security measures, no malicious activity was detected, leading to empty attack maps.

## Metrics - Before and After

### Before Hardening

| Metric                                   | Count |
| ---------------------------------------- | ----- |
| SecurityEvent (Windows VM)              | 4578  |
| Syslog (Linux VM)                        | 2125  |
| SecurityAlert (Microsoft Defender for Cloud) | 17  |
| SecurityIncident (Sentinel Incidents)    | 76  |
| NSG Inbound Malicious Flows Allowed      | 88  |

### After Hardening

| Metric                                   | Count |
| ---------------------------------------- | ----- |
| SecurityEvent (Windows VM)              | 78   |
| Syslog (Linux VM)                        | 27   |
| SecurityAlert (Microsoft Defender for Cloud) | 0  |
| SecurityIncident (Sentinel Incidents)    | 0   |
| NSG Inbound Malicious Flows Allowed      | 0   |

## Utilizing NIST 800-61r2 Guide

![NIST 800-61 Incident Handling Framework](https://i.imgur.com/uH71bJR.png)

NIST SP 800-61r2 guidelines for incident handling were followed, which involved the following steps:

### Preparation

- The Azure lab was set up to ingest logs into Log Analytics Workspace.
- Sentinel and Defender were configured, and alert rules were established.

### Detection & Analysis

- Malware compromising system integrity was detected.
- Alert ownership was assigned with "High" severity and "Active" status.
- Affected systems and users were identified.
- A full system scan with updated antivirus software was performed.
- Alert authenticity was verified as a "True Positive," and relevant personnel were notified.

### Containment, Eradication & Recovery

- Infected systems were quarantined, and, if necessary, shut down.
- Infected systems were remediated by restoring to a known clean state or by employing up-to-date antivirus solutions.

### Post-Incident Activity

- The incident was analyzed, root causes were determined, and response effectiveness was assessed.
- A report was disseminated to stakeholders.
- Corrective actions were implemented to address root causes.
- A lessons-learned review of the incident was conducted.

## Conclusion

This project established a mini honeynet on Microsoft Azure, integrated log sources into a Log Analytics workspace, and leveraged Microsoft Sentinel for alerting and incident handling. The significant reduction in security events and incidents after implementing security controls underscores their effectiveness in safeguarding the environment. It's important to note that in a heavily utilized environment, more security events and alerts may be generated post-security enhancements.
