# **Digital Forensics Final Report: Analysis of Host 147.32.84.165 Compromise**

## **1. Executive Summary**: This report details the findings of a network traffic analysis concerning the host 147.32.84.165. Analysis confirms the host was successfully compromised and utilized as a node in a sophisticated multi-stage botnet attack. The activity observed is consistent with Conficker-style malware and involves command-and-control (C2) communications, the delivery of multiple malicious payloads (Trojan malware), and the establishment of persistent, interactive remote access (RDP).

*Key Findings:  Description*

Infected Host: 147.32.84.165 (Confirmed victim/bot)

Primary Malware: Conficker-style Trojan/Botnet 

Attack Methodology: Multi-Stage C2, Payload Delivery, Data Exfiltration, and Interactive 

Identified C2 Servers: 94.63.149.152, 60.190.223.75, 91.220.0.52, 209.173.182.133

Remote Control (RDP) 

Time Frame of Activity: August 15, 2011 (Multiple events observed)


## **2. Scope and Data Sources**:

Objective: Identify attacker's IP address(es), attack methodology, and the extent of the host compromise.

Time Frame	Activity: analyzed on August 15, 2011.

Data Sources: Network traffic capture (botnet-capture-20110815-fast-flux.pcap from the CTU13 dataset), parsed logs (conn.log, http.log, files.log), and external threat intelligence reports (VirusTotal)

Tools Used: Zeek (for log generation and analysis), Wireshark (for packet-level inspection and file carving), Kali Linux (for hash calculation), and VirusTotal (for malware identification).

## **3. Analysis of Malicious IP Addresses and Methodology**:
The investigation identified four distinct external IP addresses communicating with the victim host (147.32.84.165), each performing a specific function in the attack chain.

**3.1. Initial Compromise and Payload Delivery (94.63.149.152)**:

Evidence: The host contacted this IP twice via HTTP GET requests for the suspicious resource /rus.php from the domain ii.ebatmoyhuy.com.

Malware Delivery: The server responded with a large message (25791 bytes) and delivered a file named /gc.exe.


Status: A file associated with this activity was rated malicious by 57/70 VirusTotal vendors, confirming this IP as an initial C2 server for Trojan malware activity.

**3.2. Primary C2 Beaconing and Delivery (60.190.223.75)**

Evidence: The infected host continuously initiated low-volume HTTP beaconing to this IP every few minutes, contacting suspicious domains like 88.perfectexe.com:88 and w.nucleardiscover.com:888.

Payloads: This IP delivered files with a MIME type of application/x-dosexec (Windows executable) in response to a request for /bd.jpg?t=... and for the file /p/out/kp.exe.

Malware Confirmation: The file kp.exe was extracted, hashed, and confirmed by 45/48 VirusTotal vendors as Trojan malware.

Status: C2 Communication and confirmed Malware Delivery.

**3.3. Long-Term C2 and Data Exfiltration (91.220.0.52)**

Evidence: The host engaged in consistent beaconing activity (small-sized requests) to this IP on port 80 at steady 30-31 second intervals.

Payload Delivery: This IP was observed responding with large byte sizes (e.g., 200,000+ bytes), indicating multiple downloads of a component or command delivery.

Status: Confirmed C2 Communication, potentially maintaining a persistent connection for the trojan malware.

**3.4. Interactive Remote Access (209.173.182.133)**

Evidence: This external IP initiated repeated connections to the victim host on TCP port 3389 (RDP) at a highly automated and steady interval of 5-6 seconds.

Inference: This indicates the attacker is leveraging the previously installed malware to open a backdoor or enable the RDP service, allowing them to gain hands-on-keyboard access to the compromised machine. The frequent connections with a RSTR (Reset) state suggest the attacker is rapidly cycling interactive sessions to evade detection.

Status: Interactive Remote Access and C2 Communication.

## **4. Broader Botnet Activity (Based on Log Summaries)**
Analysis of the full network capture confirmed that the compromise extended beyond basic C2 and was consistent with large-scale botnet operations:


IRC C2: High volume of connections on port 6667 (IRC standard) suggests an established C2 communication path using the IRC protocol.


Custom C2: 676 connections to port 65500 suggest a dedicated, custom C2 channel.


Spam/Exfiltration: Over 13,000 connections on port 25 and 587 (SMTP ports) strongly suggest the host was used to send spam, phishing, or exfiltrate data via email.


Conficker DGA: The extremely high volume of connections to the local DNS server suggests the malware is performing rapid Domain Resolution using a Domain Generation Algorithm (DGA), which is a signature of Conficker-style botnet activity. * Worm Propagation: The presence of connections on SMB/NTLM/DCE_RPC ports suggests the malware is attempting worm propagation to infect other hosts on the local network.

## **5. Conclusions and Next Steps**
The evidence overwhelmingly demonstrates that the host 147.32.84.165 is severely compromised and is actively participating in a sophisticated, multi-protocol botnet. The attack escalated from an initial malware delivery to persistent, interactive remote control by the threat actor.

Recommendations:

Immediate Isolation: The host 147.32.84.165 must be immediately isolated from the network to prevent further data loss and lateral movement.

Block External IPs: Block all identified malicious IP addresses: 94.63.149.152, 60.190.223.75, 91.220.0.52, and 209.173.182.133.

Incident Response: Conduct a full deep-dive forensic analysis of the isolated host's memory and disk image to identify  installed malicious files, and compromised user accounts.

Perimeter Hardening: Review and tighten outbound firewall policies to prevent unusual protocols (like RDP, IRC, and custom ports) and high-volume email traffic from internal hosts.

Further security: Develop custom security signatures (e.g., IDS/IPS or WAF rules) to detect future activity related to the identified domains (ii.ebatmoyhuy.com) and resources (/rus.php, /p/out/kp.exe).
