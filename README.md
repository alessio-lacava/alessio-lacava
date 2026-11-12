# Hi, I'm Alessio 👋
### Aspiring SOC Analyst | Cyber Security Specialist

🇮🇹 [Versione italiana](README.it.md)

I recently completed an Intensive Professional Master Program in **Cyber Security & Ethical Hacking** and looking for my first role as a **SOC Analyst / Junior Security Analyst**. Here you'll find my personal labs, team projects (Buildweeks) and coursework exercises.

📫 **Contact:** [LinkedIn](https://www.linkedin.com/in/alessio-lacava/)

---

## 🔬 Home Labs & Personal Projects

Self-directed projects to deepen my skills in Incident Response, Threat Hunting and Threat Intelligence.

### 🛡️ Detection Lab (Splunk, Sysmon & OpenSSH) [PDF](https://github.com/acidrabbit86/acidrabbit86/blob/main/Splunk-Sysmon-Detection-Lab.pdf)
An isolated lab to observe Windows endpoint telemetry with **Sysmon** (Event ID 1 for processes, 3 for network connections, 13 for registry changes), forwarded to **Splunk Enterprise** via **Universal Forwarder** (port 9997). For each scenario I simulated the attack and wrote the detection rule:

1. **SSH Brute Force:** attack with **Hydra** from Kali Linux against a test user; field extraction from OpenSSH logs using `rex` and a scheduled alert with a cron schedule.
2. **Suspicious PowerShell:** detection of anomalous command lines (`ExecutionPolicy Bypass`, `DownloadString`) via Sysmon Event ID 1.
3. **Persistence via Registry Run Key:** monitoring of `CurrentVersion\Run` (Sysmon Event ID 13), mapped to **MITRE ATT&CK T1547.001**.

### 📄 Threat Brief: FortiBleed Campaign [PDF](https://github.com/acidrabbit86/acidrabbit86/blob/main/FortiBleed-Threat-Brief.pdf)
Analysis of the compromise campaign targeting internet-exposed **Fortinet FortiGate** firewalls and SSL VPN gateways: attack chain (credential stuffing and infostealer dumps, exfiltration of user databases with legacy SHA-256 hashes, offline GPU cracking with Hashcat, administrator account lockout), **MITRE ATT&CK** mapping, detection indicators (anomalous accounts such as `forticloud-sync`, `support_fortinet`, `adminsslvpn`) and mitigations recommended by the FBI and Fortinet (restricting administrative access, disabling legacy hashes, phishing-resistant MFA).

### 🎯 CTI Report: The Gentlemen Ransomware (Storm-2697) [PDF](https://github.com/acidrabbit86/acidrabbit86/blob/main/The-Gentlemen-Ransomware-CTI.pdf)
Threat Intelligence report on the double-extortion RaaS group **The Gentlemen** (ArmCorp): analysis of the Go-based encryptor, the **GentleKiller** EDR-killing framework (BYOVD via vulnerable drivers such as `ThrottleBlood.sys`) and the worm-like lateral movement module. Includes a custom **YARA rule**, IoCs and Active Directory hardening strategies (SYSVOL protection, blocking vulnerable drivers with HVCI/WDAC).

---

## 🚀 Team Projects (Buildweek)

| Project | What I did | Tools | Repo |
| :--- | :--- | :--- | :--- |
| **Buildweek 1**<br>Network Architecture & Perimeter Defense | Designed a 6-floor corporate network (120 hosts) with per-floor segmentation, a DMZ for critical services and a perimeter firewall with 3 IDS/IPS modules | Cisco Packet Tracer, pfSense, Python | [View repo](https://github.com/acidrabbit86/Epicode---Buildweek-1) |
| **Buildweek 2**<br>Penetration Testing & Vulnerability Assessment | Web exploitation (SQLi, XSS), attacks on LLMs (prompt injection), infrastructure exploitation on Linux and Windows targets, 3 CTF challenges | Metasploit, SQLi, XSS, CTF | [View repo](https://github.com/acidrabbit86/Epicode---Buildweek-2) |
| **Buildweek 3**<br>SOC Analysis, Incident Response & Forensics | Malware analysis in sandbox, PCAP forensics, threat hunting (SQLi, DNS exfiltration, unauthorized `root` access, data theft via FTP) and SPL queries for SSH brute force | Security Onion, Kibana, Sguil, Wireshark, Splunk, ANY.RUN | [View repo](https://github.com/acidrabbit86/Epicode---Buildweek-3) |

---

## 🛠️ Tech Stack

- **Systems & VMs:** Kali Linux, FLARE-VM, Security Onion, Windows Server 2022, Windows 10, pfSense, Cisco CyberOps Workstation
- **SIEM & Monitoring:** Splunk Enterprise (SPL), Kibana, Sguil, Sysmon, Event Viewer
- **Network & Forensics:** Wireshark, tcpdump, ProcMon, FakeNet-NG, HashMyFiles, Cisco Packet Tracer
- **Malware Analysis:** ANY.RUN, VirusTotal
- **Pentesting:** Metasploit, Nmap, Masscan, Nessus, Hydra
- **Cracking & Reverse Engineering:** Hashcat, John the Ripper, CrackStation, Immunity Debugger, Mona.py
- **Active Directory:** AD DS, GPO, NTFS ACLs
- **Languages:** Python (including Google Gemini API), Bash, PowerShell, SQL, SPL, YARA

---

## 📚 Exercises by Course Unit

All weekly labs are in the **[EpicodeCyberSec-Esercizi](https://github.com/acidrabbit86/EpicodeCyberSec-Esercizi)** repository (documents are in Italian).

<details>
<summary><b>🔷 UNIT 1: Network Fundamentals, Programming & Security</b></summary>

- **W1 · Network Design:** SME network across 3 floors with 4 dedicated VLANs.
- **W2 · Python & AI:** Cyber Security virtual assistant using the Google Gemini API (`Agent_AI_Prova.py`).
- **W3 · Network Security:** advanced firewall rules and traffic inspection.
- **W4:** corresponds to Buildweek 1.
</details>

<details>
<summary><b>🔶 UNIT 2: Penetration Testing, Vulnerability Assessment & Exploitation</b></summary>

- **W5 · Reconnaissance:** port scanning and vulnerability assessment with Nmap and Nessus on Metasploitable.
- **W6 · Web Security:** XSS and SQLi on DVWA, dictionary attacks with Hydra on SSH/FTP, full blackbox penetration test.
- **W7 · Exploitation:** Metasploit (Java RMI, Vsftpd backdoor) and Meterpreter payloads on Windows 10.
- **W8:** corresponds to Buildweek 2.
</details>

<details>
<summary><b>🛡️ UNIT 3: Malware Analysis, Digital Forensics & Incident Response</b></summary>

- **W9 · Malware & Forensics:** FLARE-VM, static/dynamic analysis (WarzoneRAT, Trojan/Rozena, WannaCry) and a Network Forensics Report on a TCP SYN port scan.
- **W10 · Linux, Splunk & Active Directory:** DAC permissions on Linux, log indexing in Splunk, an Active Directory domain on Windows Server 2022 with OUs, NTFS ACLs and GPO hardening.
- **W11 · Protocols, Sandbox & Database Forensics:** TCP 3-way handshake and DNS in Wireshark, PowerShell threat hunting, infection chain in ANY.RUN and PCAP forensics of a SQL Injection attack on MySQL. [View the weekly project](https://github.com/acidrabbit86/EpicodeCyberSec-Esercizi/blob/4d61d9c372e47a066e2dec23806f59c41b529a1d/UNIT_3/S11/L5-weekly/Progetto%20Settimanale%20S11L5.pdf)
- **W12:** corresponds to Buildweek 3.
</details>
