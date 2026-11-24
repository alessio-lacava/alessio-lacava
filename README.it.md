# Ciao, io sono Alessio 👋
### Aspirante SOC Analyst | Cyber Security Analyst | Junior IT Support

🇬🇧 [English version](README.md)

Ho recentemente completato un Master Intensivo in **Cyber Security & Ethical Hacking** e cerco il mio primo ruolo come **SOC Analyst / Junior Security Analyst**. Qui trovi i miei laboratori personali, i progetti di gruppo (Buildweek) e gli esercizi del percorso.

📫 **Contatti:** [LinkedIn](https://www.linkedin.com/in/alessio-lacava/)

---

## 🔬 Home Lab & Progetti Personali

Progetti realizzati in autonomia per approfondire Incident Response, Threat Hunting e Threat Intelligence.

### 🛡️ Detection Lab (Splunk, Sysmon & OpenSSH) [PDF](https://github.com/alessio-lacava/alessio-lacava/blob/main/Detection_Lab_Splunk_Sysmon.pdf)
Laboratorio isolato per osservare la telemetria endpoint Windows con **Sysmon** (Event ID 1 processi, 3 connessioni di rete, 13 modifiche al registro), inoltrata a **Splunk Enterprise** tramite **Universal Forwarder** (porta 9997). Per ogni scenario ho simulato l'attacco e scritto la regola di detection:

1. **Brute Force SSH:** attacco con **Hydra** da Kali Linux contro un utente di test; estrazione dei campi dai log OpenSSH con `rex` e alert schedulato con pianificazione cron.
2. **PowerShell sospetto:** rilevamento di command line anomale (`ExecutionPolicy Bypass`, `DownloadString`) tramite Sysmon Event ID 1.
3. **Persistenza via Registry Run Key:** monitoraggio di `CurrentVersion\Run` (Sysmon Event ID 13), mappato su **MITRE ATT&CK T1547.001**.

### 🚨 Security Misconfiguration & SIEM Detection Gap Analysis (Wazuh, Nginx & Git) [PDF](https://github.com/alessio-lacava/alessio-lacava/blob/main/OWASP_A02_Wazuh_Lab_Report.pdf)

Laboratorio Red/Blue Team in ambiente isolato (**Kali Linux** `10.0.2.15` contro **Ubuntu Server** `10.0.2.6` con **Nginx 1.28.3** e **Wazuh 4.10.5** all-in-one che legge direttamente `/var/log/nginx/access.log`) per analizzare **OWASP Top 10:2025 A02 (Security Misconfiguration)** e i gap di detection delle regole predefinite del SIEM:

1. **File esposti nella web root (`.env`, `config.bak`):** enumerazione con **Gobuster** (`common.txt` rispetto a `small.txt -x bak,txt,php`) e richieste dirette con `curl`, mostrando che le regole di default di Wazuh segnalano la ricognizione con `404` (`31516`, `31101`, correlazione `400`), mentre la regola `31108` (livello `0`) ignora le risposte `200 OK` sui file sensibili.
2. **Repository `.git` esposto e cronologia dei commit:** esposizione accidentale di `/var/www/html/.git` individuata con **Gobuster**, ricostruzione locale tramite **git-dumper** e ispezione con `git log -p` per recuperare una credenziale di database presente in un commit precedente anche dopo averla rimossa da `config.php`.
3. **Regola custom e remediation:** chiusura del gap sulle risposte `200 OK` con la regola custom `100100` (livello `12`, **MITRE ATT&CK T1083**) in `local_rules.xml` (~1–2 s di latenza), rimozione dei file esposti e hardening su Nginx (`autoindex off`, blocco delle estensioni sensibili).

### 📄 Threat Brief: FortiBleed Campaign [PDF](https://github.com/alessio-lacava/alessio-lacava/blob/main/FortiBleed-Threat-Brief.pdf)
Analisi della campagna di compromissione contro firewall e gateway VPN SSL **Fortinet FortiGate** esposti a internet: catena d'attacco (credential stuffing e dump di infostealer, esfiltrazione dei database utenti con hash SHA-256 legacy, cracking offline su GPU con Hashcat, account lockout degli amministratori), mappatura **MITRE ATT&CK**, indicatori di detection (account anomali come `forticloud-sync`, `support_fortinet`, `adminsslvpn`) e mitigazioni indicate da FBI e Fortinet (limitazione accesso amministrativo, disattivazione hash legacy, MFA resistente al phishing).

### 🎯 CTI Report: The Gentlemen Ransomware (Storm-2697) [PDF](https://github.com/alessio-lacava/alessio-lacava/blob/main/The-Gentlemen-Ransomware-CTI.pdf)
Report di Threat Intelligence sul gruppo RaaS **The Gentlemen** (ArmCorp), attivo con doppia estorsione: analisi del cifratore in Go, del framework EDR-killing **GentleKiller** (BYOVD tramite driver vulnerabili come `ThrottleBlood.sys`) e del modulo worm-like per il movimento laterale. Include una **regola YARA** personalizzata, gli IoC e strategie di hardening Active Directory (protezione SYSVOL, blocco driver vulnerabili con HVCI/WDAC).

---

## 🚀 Progetti di Gruppo (Buildweek)

| Progetto | Cosa ho fatto | Tools | Repo |
| :--- | :--- | :--- | :--- |
| **Buildweek 1**<br>Network Architecture & Perimeter Defense | Progettazione di una rete aziendale su 6 piani (120 host) con segmentazione per piano, DMZ per servizi critici e firewall perimetrale con 3 moduli IDS/IPS | Cisco Packet Tracer, pfSense, Python | [Vedi repo](https://github.com/acidrabbit86/Epicode---Buildweek-1) |
| **Buildweek 2**<br>Penetration Testing & Vulnerability Assessment | Exploitation web (SQLi, XSS), attacchi a LLM (prompt injection), exploitation di infrastruttura su target Linux e Windows, 3 sfide CTF | Metasploit, SQLi, XSS, CTF | [Vedi repo](https://github.com/acidrabbit86/Epicode---Buildweek-2) |
| **Buildweek 3**<br>SOC Analysis, Incident Response & Forensics | Analisi malware in sandbox, forensics di PCAP, threat hunting (SQLi, esfiltrazione DNS, accessi `root` non autorizzati, furto dati via FTP) e query SPL per brute force SSH | Security Onion, Kibana, Sguil, Wireshark, Splunk, ANY.RUN | [Vedi repo](https://github.com/acidrabbit86/Epicode---Buildweek-3) |

---

## 🛠️ Tech Stack

* **Sistemi & VM:** Kali Linux, FLARE-VM, Security Onion, Windows Server 2022, Windows 10, pfSense, Cisco CyberOps Workstation
* **SIEM & Monitoraggio:** Splunk Enterprise (SPL), Wazuh, Kibana, Sguil, Sysmon, Event Viewer
* **Rete & Forensics:** Wireshark, tcpdump, ProcMon, FakeNet-NG, HashMyFiles, Cisco Packet Tracer
* **Analisi Malware:** ANY.RUN, VirusTotal
* **Pentesting & Recon:** Metasploit, Nmap, Masscan, Nessus, Hydra, Gobuster, git-dumper
* **Cracking & Reverse Engineering:** Hashcat, John the Ripper, CrackStation, Immunity Debugger, Mona.py
* **Active Directory:** AD DS, GPO, NTFS ACLs
* **Linguaggi:** Python (inclusa Google Gemini API), Bash, PowerShell, SQL, SPL, YARA

---

## 📚 Esercizi per Unità Didattica

Tutti i laboratori settimanali sono nella repo **[EpicodeCyberSec-Esercizi](https://github.com/acidrabbit86/EpicodeCyberSec-Esercizi)**.

<details>
<summary><b>🔷 UNIT 1: Network Fundamentals, Programming & Security</b></summary>

- **S1 · Network Design:** rete PMI su 3 piani con 4 VLAN dedicate.
- **S2 · Python & AI:** assistente virtuale per la Cyber Security con Google Gemini API (`Agent_AI_Prova.py`).
- **S3 · Network Security:** regole avanzate di firewall e ispezione del traffico.
- **S4:** corrisponde alla Buildweek 1.
</details>

<details>
<summary><b>🔶 UNIT 2: Penetration Testing, Vulnerability Assessment & Exploitation</b></summary>

- **S5 · Reconnaissance:** port scanning e vulnerability assessment con Nmap e Nessus su Metasploitable.
- **S6 · Web Security:** XSS e SQLi su DVWA, attacchi a dizionario con Hydra su SSH/FTP, penetration test blackbox completo.
- **S7 · Exploitation:** Metasploit (Java RMI, backdoor Vsftpd) e payload Meterpreter su Windows 10.
- **S8:** corrisponde alla Buildweek 2.
</details>

<details>
<summary><b>🛡️ UNIT 3: Malware Analysis, Digital Forensics & Incident Response</b></summary>

- **S9 · Malware & Forensics:** FLARE-VM, analisi statica/dinamica (WarzoneRAT, Trojan/Rozena, WannaCry) e Network Forensics Report su un port scan TCP SYN.
- **S10 · Linux, Splunk & Active Directory:** permessi DAC su Linux, indicizzazione log su Splunk, dominio Active Directory su Windows Server 2022 con OU, ACL NTFS e hardening via GPO.
- **S11 · Protocolli, Sandbox & Database Forensics:** TCP 3-way handshake e DNS in Wireshark, PowerShell threat hunting, catena infettiva in ANY.RUN e forensics PCAP di un attacco SQL Injection su MySQL. [Vedi il progetto settimanale](https://github.com/acidrabbit86/EpicodeCyberSec-Esercizi/blob/4d61d9c372e47a066e2dec23806f59c41b529a1d/UNIT_3/S11/L5-weekly/Progetto%20Settimanale%20S11L5.pdf)
- **S12:** corrisponde alla Buildweek 3.
</details>
