### 1.Executive Summary

**Goal**: analyzing IP activity and HTTP anomalies related to a suspected web/C2C attack

**Key Findings**: Multiple malicious IP addresses were identified conducting unusual HTTP POST requests characteristic of a command-and-control (C2) channel

### 2.Scope and Data sources

**Time Frame**: 

**Data Sources**: http.log, conn.log

### 3.Methodology

**Tools Used**: Zeek

**Criteria for unusual:**

### 4.Analysis of Malicious IP addresses

60.190.223.75 

Scanning/Reconnaisance: requests for files like /list.php, /phpMyAdmin, and .env, to find common administration pages, configuration files,etc. that might have weak access controls, repeated requests for /bDjpt/, /wp-includes/, and specifically files like /list.php and /index.php with various query strings (?id=..., ?key=...).

Exploitation attempt: Long, random strings in query parameters, which are indicative of a malicious payload trying to masquerade itself. Trying to access host w.nucleardiscover.com:888, rated malicious by 3 out of 63 vendors on VirusTotal, from infected server 147.32.84.165.

Status: C2 communication

### 5.1. Command and Control (C2) Activity
**Common Endpoint**: The specific path targeted (e.g., /images/upload.php or a non-existent path like /admin/heartbeat).

**HTTP Method**: Focus on unusual methods, typically POST or PUT used for data exfiltration or command delivery.

**Request Payload Analysis**:

**Size**: Note abnormally small or large payloads.

**Encoding**: Describe how the data was concealed (e.g., Base64 encoded payload, Custom XOR encryption).

**Examples**: Include a redacted, sanitized example of a malicious request and the corresponding server response (use a Markdown code block for clarity).

5.2. Reconnaissance/Scanning Activity
Focus: Detail any IPs primarily engaged in directory scanning or testing common vulnerabilities.

Indicators: High volume of 404 (Not Found) errors, rapid attempts to access /wp-admin/, /phpmyadmin/, etc.

6. Conclusions and Next Steps
Summary of Evidence: Reiterate the most compelling evidence (e.g., "The pattern of requests from 192.0.2.1 strongly aligns with a C2 beaconing operation.").

Recommendations: Suggest further steps for the investigation (e.g., Isolate the victim host, Block all identified malicious IPs, Develop WAF rules to detect the described payload pattern).
