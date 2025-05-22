<h1>Building a SOC + Honeynet in Azure</h1>

![image](https://github.com/user-attachments/assets/67e3a6c6-32ac-4a49-a132-21f276e18a54)


<h2>Introduction</h2>

In this project, I deployed a mini honeynet in Azure, collecting log data from various sources into a Log Analytics workspace. Microsoft Sentinel was then used to create attack maps, alerts, and incidents. To demonstrate the effectiveness of security controls, I measured key metrics in an insecure environment, applied security hardening measures, and re-measured the metrics after 24 hours:

 - SecurityEvent (Windows Event Logs)
 - Syslog (Linux Event Logs)
 - SecurityAlert (Log Analytics Alerts Triggered)
 - SecurityIncident (Incidents created by Sentinel)
 - AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

<h2>Architecture Before Hardening / Security Controls</h2>

![image](https://github.com/user-attachments/assets/7392ac54-7073-4fc4-8af9-93747b1da106)


The architecture of the mini honeynet in Azure consists of the following components:

 - Virtual Network (VNet)
 - Network Security Group (NSG)
 - Virtual Machines (2 windows, 1 linux)
 - Log Analytics Workspace
 - Azure Key Vault
 - Azure Storage Account
 - Microsoft Sentinel

For the "BEFORE" metrics, resources were deployed with open Network Security Groups, built-in firewalls, and public endpoints, exposing them to the internet.

For the "AFTER" metrics, security was enhanced by restricting Network Security Groups to allow only admin workstation traffic, and activating built-in firewalls and Private Endpoints for all resources.

<h2>Attack Maps Before Hardening / Security Controls</h2>

<h4>NSG Allowed Inbound Malicious Flows</h4>

![image](https://github.com/user-attachments/assets/aa49ae69-be4e-44cf-a55f-38ea0fb76b39)

<h4>Linux Syslog Auth Failures</h4>

![image](https://github.com/user-attachments/assets/06c6a3ce-e9bd-4400-9464-29d13cc7449a)

<h4>Windows RDP/SMB Auth Failures</h4>

![image](https://github.com/user-attachments/assets/63ef6936-9f86-400b-a878-069caf8129f7)

<h4>MSSQL-Auth-Fail</h4>

![image](https://github.com/user-attachments/assets/0cc141a2-a4f9-456f-b528-815bdb7607e0)

<h2>Metrics Before Hardening / Security Controls</h2>

The following table shows the metrics we measured in our insecure environment for 24 hours: Start Time 2024-11-13 17:12:43 Stop Time 2024-11-14 17:12:43

![image](https://github.com/user-attachments/assets/bd5a32ed-dfe0-421f-99f7-9e98b2bcc2d4)

<h2>Architecture After Hardening / Security Controls</h2>

![image](https://github.com/user-attachments/assets/7ca15a24-5d79-44b2-bd68-6ae088ce0d7b)

<h2>Attack Maps Before Hardening / Security Controls</h2>

All map queries actually returned no results due to no instances of malicious activity for the 24-hour period after hardening.

<h2>Metrics After Hardening / Security Controls</h2>

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls: Start Time 2024-11-14 19:42:17 Stop Time 2024-11-15T19:42:17

![Screenshot (49)](https://github.com/user-attachments/assets/d08eaef9-78ec-41dc-a4ca-8367c6864215)

<h2>Conclusion</h2>

This project demonstrated the value of security controls in a cloud-based environment. A mini honeynet was built in Microsoft Azure, and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents. Key findings included a significant reduction in security events and incidents after applying security controls, underscoring their importance.

In a scenario where the network resources were heavily utilised by regular users, it's likely that the implementation of security controls would have resulted in an even greater number of security events and alerts being triggered during the 24-hour period.
