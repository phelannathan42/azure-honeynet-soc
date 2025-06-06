
# Azure Honeynet: Realistic Cyber Attack Emulation with SOC Integration


## Overview

This project showcases a hands-on deployment of a honeynet within Microsoft Azure, crafted to simulate real-world cyber threats. The environment was monitored and analyzed using Microsoft Sentinel, highlighting my skills in cloud security, detection engineering, and incident response.

## Project Goal

The main goal was to set up purposely vulnerable virtual machines in an Azure cloud environment, allowing for real-time observation and analysis of live cyber attacks. This experience enhanced my understanding of attacker behavior and improved my incident handling and remediation skills.

## Tools, Frameworks, and Azure Services Used

- **Azure Networking**: Virtual Networks, NSGs
- **Compute**: Windows & Linux Virtual Machines
- **Logging & Monitoring**:
  - Azure Log Analytics (KQL Queries)
  - Microsoft Sentinel (SIEM)
- **Security Enhancements**:
  - Azure Key Vault
  - Azure Storage Accounts
  - Microsoft Defender for Cloud
- **Remote & Admin Access**: RDP, CLI, PowerShell
- **Compliance Standards**:
  - [NIST SP 800-53 Rev. 5](https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final)
  - [NIST SP 800-61 Rev. 2](https://www.nist.gov/privacy-framework/nist-sp-800-61)

## Step-by-Step Implementation

### 1. Honeynet Deployment
Multiple vulnerable VMs were deployed to emulate an unprotected environment—creating an ideal scenario to attract malicious traffic.

### 2. Data Collection & Threat Detection
Logs from each Azure component were forwarded to Log Analytics, and Sentinel was used to visualize attack maps, set up alerts, and generate incidents.

### 3. Baseline Analysis
The environment was monitored for 24 hours without defenses to gather baseline metrics around attacks and threats.

### 4. Remediation & Security Hardening
Security improvements were rolled out, including restricted firewall rules, private endpoints, and NSG lockdowns.

### 5. Post-Security Analysis
Another 24-hour observation followed to compare metrics and measure the effectiveness of the newly applied security posture.

## Architecture (Before Security Controls)
![Before](https://i.imgur.com/1tLjWY9.png)

> **Key Details**:  
All services had public exposure. NSGs and internal firewalls were open. No private access restrictions were implemented. This was done intentionally to attract attackers and capture telemetry on unauthorized access.

## Architecture (After Hardening)
![After](https://i.imgur.com/ch1cAMU.png)

> **Changes Made**:
- **NSGs**: Whitelisted only my IP; all other traffic was blocked.
- **Firewalls**: Enabled and tightly configured on each VM.
- **Private Endpoints**: Removed public exposure for key services like Storage and SQL DBs.

These updates significantly reduced the attack surface and enhanced overall security.

## Attack Visualizations (Before Securing)

> *Maps were built using [custom Sentinel KQL workbooks](https://github.com/AmiliaSalva/Cloud-SOC-Project-Resources/blob/main/MS%20Sentinel%20Maps%20(JSON)/linux-ssh-auth-fail.json)*

### Malicious Inbound Traffic (NSG open)
![NSG Attack Map](https://i.imgur.com/JeElX9R.png)

### Failed SSH Logins (Linux Server)
![Linux Failures](https://i.imgur.com/QW8PF0o.png)

### RDP/SMB Brute Force Attempts (Windows Server)
![Windows Failures](https://i.imgur.com/SETmQBl.png)

## Attack Visualizations (After Securing)

> Post-remediation map queries returned zero activity—confirming mitigation success.

## Security Metrics Comparison

### Before Hardening
**Timeframe**: May 2, 2023 – May 3, 2023

| Metric                            | Count  |
|-----------------------------------|--------|
| Windows VM Security Events        | 21,182 |
| Linux VM Syslog Entries           | 4,877  |
| Microsoft Defender Alerts         | 0      |
| Sentinel Incidents                | 343    |
| Malicious Inbound NSG Traffic     | 969    |

### After Hardening
**Timeframe**: March 18, 2023 – March 19, 2023

| Metric                            | Count  |
|-----------------------------------|--------|
| Windows VM Security Events        | 783    |
| Linux VM Syslog Entries           | 23     |
| Microsoft Defender Alerts         | 0      |
| Sentinel Incidents                | 0      |
| Malicious Inbound NSG Traffic     | 0      |

## Summary

This project simulated and then mitigated real-world cyber threats using Azure’s native tools. After collecting baseline data from an unsecured environment, security best practices were applied. The resulting drop in malicious events demonstrated the effectiveness of a properly secured cloud environment.

> If this system were actively used in production, post-hardening metrics would reflect some noise due to normal user behavior—but threat-related activity was eliminated.
