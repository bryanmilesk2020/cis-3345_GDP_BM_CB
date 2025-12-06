### 1.Executive Summary

**Goal**: analyzing IP activity and HTTP anomalies related to a suspected web/C2C attack

**Key Findings**: Multiple malicious IP addresses were identified conducting unusual HTTP POST requests characteristic of a command-and-control (C2) channel

### 2.Scope and Data sources

**Time Frame**: 

**Data Sources**: http.log, conn.log

### 3.Methodology

**Tools Used**: Zeek, Wireshark, VirusTotal

**Criteria for unusual:**

### 4.Analysis of Malicious IP addresses

**60.190.223.75** 

Findings from conn.log: Repeatedly reached out by suspected infected host (147.32.84.65). Infected host contacted it every 
few minutes over http with small request sizes (100-500 bytes) which is indicative of beaconing, common in C2C activity. 60.190.223.75 responded with sometimes 25k+ bytes and even 50k+ bytes, signifying that the infected host downloaded something from 60.190.223.75. The history field in conn.log indicated abnormal TCP handshakes, which happens in malware activity.(source:/case_notes/60.190.223.75-traffic-conn-log.txt)

Findings from http.log: This IP is repeated sent GET requests by suspected infected host (147.32.84.65) to odd domains such as 88.perfectexe.com:88, w.nucleardiscover.com:888, and ru.coolnuff.com which could be a bot/malware trying to check in with its C2 server for new commands. In addition, there were two times where a GET request with status code "200" and a mime type of "application/x-dosexec" happened, indicating that the infected host successfully downloaded something from 88.perfectexe.com:88 on 60.190.223.75. In addition, all the URIs in the GET requests had long, random sequence of characters after the "c=" which could be an encrypted malicious payload given the suspicious circumstances surrounding it. The numerous ".php" extensions, paired with the suspicious circumstances, could be malicious payloads using common circumstances in web requests in order to "blend in" with the normal traffic and bypass any simple firewall rules or other security filters.*In this log, an entry with a uri called "/p/out/kp.exe" was requested from host "shabi.coolnuff.com:2012" via 60.190.223.75. Wireshark was used to isolate this entry and save the executable to the file system on kali linux. The executable was hashed (SHA256) on the linux terminal, the hash was then copied and pasted on VirusTotal. The executable was discovered to be a trojan malware, rated malicious by 45/48 vendors that rated it.* 

From files.log: suspected infected host attempted twice to get a resource with a mime_type of "application?x-dosexec" indicating it was trying to download something from 60.190.223.75.

Status: C2C communication, malware detected 

**91.220.0.52**

Findings from conn.log: 147.32.84.165 is the originator of all connections, and 91.220.0.52 was the destination for all 
connections. Most connections were done on port 80 which is for legitimate http traffic, nearly all connections were
established and finished as intended. There are a few connections where the 91.220.0.52 responds to 147.32.84.165 with
large byte sizes, potentially indicating that 147.32.84.165 was trying to download something. Most of connections happened
at regular intervals with short durations of a few seconds or less. These connections had requests of small size from originator and destination, which happens in C2C activity when beacon tries to send short messages trying to make its
presense known to the C2 server and wait for its next command. These connections, contrasting with the few connections
where the responder (91.220.0.52) responds with a large-sized response further supports C2 activity.

Findings from http.log: 147.32.84.165 repeatedly sent POST requests to 91.220.0.52 at steady 30-31 second intervals,
indicative of automated requests characteristic to C2C beaconing. 91.220.0.52 responds with plain text messages which
could potentially be instructions for what to do next for the infected host. In conjunction with the kp.exe executable,
174.32.84.165 probably downloaded the trojan malware, whose main objective could be to maintain a persistent C2C connection
with 91.220.0.52.

**94.163.149.152**

**173.192.170.88**

**94.63.150.53**

### 5.1. Command and Control (C2) Activity
**Common Endpoint**: The specific path targeted (e.g., /images/upload.php or a non-existent path like /admin/heartbeat).

**HTTP Method**: Focus on unusual methods, typically POST or PUT used for data exfiltration or command delivery.

**Request Payload Analysis**:

**Size**: Note abnormally small or large payloads.

**Encoding**: Describe how the data was concealed (e.g., Base64 encoded payload, Custom XOR encryption).

**Examples**: Include a redacted, sanitized example of a malicious request and the corresponding server response (use a Markdown code block for clarity).

### 5.2. Reconnaissance/Scanning Activity
**Focus**: Detail any IPs primarily engaged in directory scanning or testing common vulnerabilities.

**Indicators**: High volume of 404 (Not Found) errors, rapid attempts to access /wp-admin/, /phpmyadmin/, etc.

### 6. Conclusions and Next Steps
**Summary of Evidence**: Reiterate the most compelling evidence (e.g., "The pattern of requests from 192.0.2.1 strongly aligns with a C2 beaconing operation.").

**Recommendations**: Suggest further steps for the investigation (e.g., Isolate the victim host, Block all identified malicious IPs, Develop WAF rules to detect the described payload pattern).

-----------------------------------------------------------------------------------------------------------------------------------
Suspicious IP Analysis – Zeek HTTP Log Findings

IP Investigated: 94.63.149.152
Source (victim) host: 147.32.84.165

Findings:

Two HTTP GET requests were observed from the infected machine to the suspicious IP:

/rus.php

/gc.exe

The .php and .exe file types strongly suggest command delivery and malware download behavior — common in botnet C2 channels.

The MIME type was recorded as Download, confirming file-transfer activity.

The domain ii.ebatmoyhuy.com appears in both entries.
This domain is likely a DGA-generated malicious domain used for botnet C2 communication.

The /rus.php request returned HTTP 200, indicating successful server communication.

Both entries share the same UID, meaning they occurred within the same malicious session.

Conclusion:
94.63.149.152 is acting as a command-and-control (C2) server, delivering malware files and receiving requests from the infected host (147.32.84.165).
This activity is consistent with known botnet behavior (e.g., Conficker-style activity).

from IMG_6156.HEIC
147.32.84.165    94.63.149.152   /rus.php      GET    200   Download   C8pOS22Y0bsK5Iuyng    -        ii.ebatmoyhuy.com   CTHD3m4MIaRr7Ac1b8
147.32.84.165    94.63.149.152   /gc.exe       GET    -     Download   -                     -        ii.ebatmoyhuy.com   CTHD3m4MIaRr7Ac1b8
