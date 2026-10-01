# Windows-SOC-Threat-Detection-Incident-Investigation

# Objective
This project focuses on investigating and analyzing Windows authentication security events in a controlled virtualized environment. 
The goal is to develop practical SOC analyst skills by identifying suspicious authentication activity, correlating security events, documenting indicators of compromise, 
and mapping observed behavior to the MITRE ATT&CK framework. Using Kali Linux, I generated controlled authentication activity against a Windows 10 endpoint and 
investigated the resulting Windows Security Event Logs using Event Viewer.

# Skills Learned
- Windows Security Event Log analysis using Event Viewer.
- Authentication event investigation using Windows Event IDs 4624 and 4625.
- Event correlation using account names, source IP addresses, timestamps, and logon types.
- Indicator of Compromise (IOC) identification from authentication activity.
- Network authentication analysis and investigation of Logon Type 3 events.
- Incident timeline development to correlate multiple security events.
- MITRE ATT&CK mapping for simulated brute-force and password-guessing activity.
- SOC incident documentation and security investigation reporting.

# Tools Used
 - Windows 10 — monitored endpoint and security event logging.
 - Kali Linux — simulated attacker and investigation workstation.
 - VirtualBox — virtualized isolated lab environment.
 - Windows Event Viewer — Security Event Log analysis.
 - Windows Security Event Logs — authentication event investigation.
 - Nmap — network and SMB service verification.
 - SMBClient — controlled network authentication testing.
 - MITRE ATT&CK — attack technique classification and documentation

# Implementation steps

# 1. Verified network Connectivity 
Confirmed that there was communication between Kali linux and Windows endpoint:

<img width="341" height="170" alt="Screenshot 2026-09-27 200713" src="https://github.com/user-attachments/assets/331e9f8e-d5e1-4388-8416-dbb8356099a8" />

# 2. Windows Authentication Monitoring
Windows Event Viewer was used to monitor the Security log for authentication-related events:

<img width="302" height="219" alt="Screenshot 2026-09-27 193400" src="https://github.com/user-attachments/assets/a3cb7be7-5950-4615-a511-9cab61dd2427" />

# Event ID 4625 for failed logon: 

<img width="374" height="246" alt="Screenshot 2026-09-30 205714" src="https://github.com/user-attachments/assets/fd97c359-1f17-4af6-ace3-1cbf8e1f5ba3" />


# 3. Controlled Authentication Testing
Kali linux was used to generate controlled network authentication attempts against the Windows endpoint.

# Verify SMB Availability and Generate Authentication Failures:

<img width="369" height="325" alt="Screenshot 2026-09-30 202718" src="https://github.com/user-attachments/assets/cce84374-7e28-46e0-be03-a8c9787033a6" />

# 4. Authentication Event Investigation
After generating the controlled authentication attempts, Windows Event Viewer was used to investigate the resulting security events.

# Failed Authentication for Event ID 4625
Multiple failed authentication events were identified against the same account and source IP address:

<img width="290" height="80" alt="Screenshot 2026-09-27 203441" src="https://github.com/user-attachments/assets/55135840-1dcb-43e8-848f-570cdc0b4b4c" />


<img width="181" height="87" alt="Screenshot 2026-09-27 203827 - Copy" src="https://github.com/user-attachments/assets/703fbfe2-bd22-432f-bd93-ebc0cfd02666" />


<img width="265" height="70" alt="Screenshot 2026-09-27 202854 - Copy - Copy" src="https://github.com/user-attachments/assets/848e1ae7-e931-4a62-bcd3-86a327e71ff2" />


<img width="340" height="83" alt="Screenshot 2026-09-30 205448" src="https://github.com/user-attachments/assets/7de090e9-6e67-4c65-a213-750872075fb8" />


<img width="263" height="59" alt="Screenshot 2026-09-27 202834 - Copy - Copy" src="https://github.com/user-attachments/assets/499299e1-ab85-4fa4-967b-65420e520fd3" />

This shows the full timeline of events for when the attacker attempted to gain access to the Windows endpoint. 

# Successful Authentication for Event ID 4624

<img width="299" height="190" alt="Screenshot 2026-09-27 203735" src="https://github.com/user-attachments/assets/921651d6-02c6-47dc-abaf-a079125832cd" />

This was after the correct credentials was used. 
The failed and successful events were correlated using the account name, source IP address, logon type, and timestamps.

# 5. Indicators of Compromise
- Source IP = 192.168.56.104
- Target Account = socuser
- Failed Authentication = Event ID 4625
- Successful Authentication = Event ID 4624
- Logon Type = 3
- Failure Reason = bad password

The observed pattern consisted of multiple failed authentication attempts followed by a successful network authentication from the same source IP address.

# 6. MITRE ATT&CK Mapping
The observed authentication behavior was mapped to the following MITRE ATT&CK techniques:
# T1110 for Brute Force 
Repeated authentication attempts were simulated against the Windows socuser account.

# T1110.001 — Password Guessing
Incorrect passwords were intentionally used during the controlled authentication testing to simulate password-guessing behavior.

# Conclusion
This project demonstrated a structured approach to detecting, investigating, and documenting suspicious authentication activity within a controlled Windows environment. 
By using Kali Linux to generate controlled authentication attempts and analyzing Windows Security Event Logs, the investigation provided practical experience with event correlation, indicator identification, and incident analysis. 
Mapping the observed activity to the MITRE ATT&CK framework further demonstrated how security events can be connected to known attack techniques. 
Overall, this project strengthened my practical SOC analyst skills and reinforced the importance of continuous log monitoring, evidence-based investigation, and effective security documentation.


