DanaBot Network Forensics Investigation

Platform: CyberDefenders
Category: Network Forensics / Malware Analysis
Tools: Wireshark, Windows CMD, VirusTotal
Status: Completed lab investigation

1. Investigation Objective

Investigate network traffic associated with DanaBot malware to identify the initial access IP, malicious files, execution process, and subsequent malware components.

2. Findings

Question	Finding
Attacker IP	62.173.142.148
Initial malicious file	allegato_708.js
Initial file SHA-256	See evidence notes
Execution process	wscript.exe
Second-stage file type	DLL (.dll)

3. File Hash Analysis

The SHA-256 hash of the initial payload was calculated using Windows CertUtil.

Command:

certutil -hashfile js.payload.txt SHA256

Second-stage file

Filename: WndResizerApp.exe

SHA-256:

2597322a49a6252445ca4c8d713320b238113b3b8fd8a2d6fc1088a5934cee0e

File size: 11.37 MB

VirusTotal result: 57/71 security vendors flagged the file as malicious.

File identification: Win32 DLL / PE32 executable.

4. Execution Analysis

The identified execution process was:

wscript.exe

Windows Script Host can execute JavaScript files. This is relevant to the observed initial JavaScript payload.

5. Threat Intelligence

VirusTotal identified the second-stage file with the following characteristics:

* Popular threat label: trojan.danabot/krypt
* Threat categories: Trojan, Banker, Spyware
* Family labels: Danabot, Krypt, Password

These are third-party threat-intelligence classifications, not independent proof of every behavior.

6. Investigation Methodology

1. Downloaded the CyberDefenders lab evidence.
2. Inspected the provided network traffic in Wireshark.
3. Identified suspicious network indicators.
4. Identified the initial malicious JavaScript file.
5. Calculated its SHA-256 hash using CertUtil.
6. Identified the execution process.
7. Investigated the second-stage file.
8. Checked its hash and reputation using VirusTotal.

7. Conclusion

The investigation identified a multi-stage malware infection involving a JavaScript payload and Windows Script Host execution.

The second-stage file was identified as a Win32 DLL and received significant malicious detections from VirusTotal.

Further analysis of the complete network traffic and malware behavior would be required to establish the full attack chain.

8. Recommendations

* Monitor suspicious use of wscript.exe.
* Investigate unexpected JavaScript execution.
* Monitor outbound connections to suspicious IP addresses.
* Use endpoint detection to identify suspicious DLL loading.
* Block confirmed malicious indicators according to organizational procedures.
* Preserve relevant logs and network evidence.

9. References

* CyberDefenders — DanaBot Network Forensics
* Wireshark
* Microsoft CertUtil
* VirusTotal

Disclaimer: Educational investigation performed using a cybersecurity training lab.
