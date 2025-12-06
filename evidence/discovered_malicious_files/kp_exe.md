Executable name: kp.exe
Host: shabi.coolnuff.com:2012
Time it was requested: 2011-08-15T14:14:09-0500
SHA256 hash: 96831f92f82f6719dd47d9d03edf4e688dfb0c0754bc4c7a24edf123dc05e7bf

![Hashing_on_linux_terminal](cis3345_GDP_BM_CB\case_notes\screenshots\hashing-on-terminal-1.png)
Caption: Generating SHA256 hash on kp.exe, an executable being requested by 147.32.84.165 from 60.190.223.175

![VirusTotal_results](cis3345_GDP_BM_CB\case_notes\screenshots\virustotal1.png)
Caption: Output of hash from VirusTotal showing that the executable is a trojan malware.

Summary: In file "60.190.223.175-traffic-http-log.txt", an executable that was requested by 147.32.84.165 was found. 
After this was found, the pcap file containing all the traffic was opened on WireShark. Extracted files were filtered for
and /p/out/kp.exe was located and saved to the file system. On the linux terminal, a SHA256 hash was generated on the 
executable file. The hash was then copied and pasted on VirusTotal. It was discovered to be rated malicious by 45 out of 48
vendors and was labeled as a trojan virus.
