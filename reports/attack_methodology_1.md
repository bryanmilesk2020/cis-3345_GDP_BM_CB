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

60.190.223.75 - Scanning/Reconnaisance (requests for files like /list.php, /phpMyAdmin, and .env, to find common admnistration pages, configuration files,etc. that might have weak access controls, repeated requests for /bDjpt/, /wp-includes/, and specifically files like /list.php and /index.php with various query strings (?id=..., ?key=...)).
