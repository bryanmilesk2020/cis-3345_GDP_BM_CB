# cis-3345_GDP_CB_BM

## Case Title: Network Analysis over a compromised system, an investigation into C2C behavior
### Objective: 
Investigate and uncover the attack. By using a PCAP dataset, investigators will utilize tools and learning gained from the CIS course to find the attacker. Investigators will be able to determine how the attack took place, as well as how the attacker infilitrated the system. Furthermore, investigators will use the tools to support their claims and verify their evidence to confirm there is indeed malicious behavior present within the system. 

## Forensic Toolkit
### Kali Linux VM
The VM was utulized to host our simulation, where we imported the PCAP and conducted log-based forensic review.
### Zeek
Zeek was used to for botnet network traffic analysis where we uncovered the IP addresses of the attacker and infected machines, C2 channels used in the attack, malware propagation, and evidence exfiltration. 
### Wireshark
Wire shark was used to extract files from pcap file and save suspicious intact files to calculate its hash​.
### Virus Total
Virus Total was used to identify any malicious files by searching their hashes ​

## Summary
1. Project Overview

This repository documents the network forensics investigation into the compromise of an internal host (147.32.84.165) that was utilized as a node in a sophisticated, multi-stage Command and Control (C2) botnet operation.

The analysis focuses on identifying malicious communication patterns, confirming malware delivery, and mapping the entire kill chain from initial infection to interactive remote control by the threat actor.

2. Key Findings
   
The investigation confirms a full compromise by Conficker-style Trojan malware, culminating in sustained RDP-based control.

| Team member  | Story Points | Total Contribution |
| ------------- | ------------- | ------------- |
| Bryan Mileski  | 6  | 60% |
| Caylan Barnes  | 4  | 40% |
| Team Total | 10 | 100% |
