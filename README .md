<div align="center">

```
╔══════════════════════════════════════════════════════════════╗
║   ████████╗ █████╗ ██████╗  █████╗ ███╗   ██╗               ║
║      ██╔══╝██╔══██╗██╔══██╗██╔══██╗████╗  ██║               ║
║      ██║   ███████║██████╔╝███████║██╔██╗ ██║               ║
║      ██║   ██╔══██║██╔═══╝ ██╔══██║██║╚██╗██║               ║
║      ██║   ██║  ██║██║     ██║  ██║██║ ╚████║               ║
║      ╚═╝   ╚═╝  ╚═╝╚═╝     ╚═╝  ╚═╝╚═╝  ╚═══╝   S A T Y A  ║
╚══════════════════════════════════════════════════════════════╝
```

### `> SOC Analyst in Training · Threat Hunter · Defender`

[![LinkedIn](https://img.shields.io/badge/LinkedIn-tapansb1-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/tapansb1/)
[![Email](https://img.shields.io/badge/Email-tapansatyabhogadi%40gmail.com-EA4335?style=flat-square&logo=gmail)](mailto:tapansatyabhogadi@gmail.com)
![Status](https://img.shields.io/badge/Status-Actively_Seeking_Tier--1_SOC_Role-22c55e?style=flat-square)

</div>

---

## `$ whoami`

Final-year B.Tech IT student graduating **June 2026**, with hands-on SOC experience built from the ground up.

```yaml
internship:  CFSS India SOC Lab  (~160 supervised lab hours)
certifications: 5 earned  |  1 in progress (CEH)
lab_environment: VirtualBox · Splunk SIEM · Windows 10 · Kali Linux
detection_rules_written: 4 SPL rules  →  7 MITRE ATT&CK techniques mapped
attack_scenarios_executed: 4
cves_exploited: 3 (vsftpd, Samba, UnrealIRCd)
framework: NIST SP 800-61r2 (Incident Response)
```

> I don't just study cybersecurity — I build labs, break things, and document how to fix them.

---

## `$ ls ./skills`

### 🛡️ Defensive / Blue Team

| Skill | Context |
|---|---|
| SIEM Implementation & Log Ingestion | SOC Lab — Splunk Enterprise 9.x + Universal Forwarder |
| SPL Query Writing & Alert Tuning | 4 detection rules, tuned across 3 iterations |
| Network Attack Detection | SYN Flood (~700 pkt/sec), Port Scanning |
| Threat Hunting & MITRE ATT&CK Mapping | 7 techniques mapped across T1 tactics |
| Incident Response (NIST SP 800-61r2) | Full IR lifecycle: Detection → Recovery |

### ⚔️ Offensive / Red Team

| Skill | Context |
|---|---|
| Penetration Testing | Metasploitable 2 lab — 3 critical CVEs exploited |
| Vulnerability Assessment | 6 findings documented with CVSS scores + remediation |
| CVE Exploitation | Metasploit 6.x — root shells via vsftpd, Samba, UnrealIRCd |

---

## `$ ls ./tools`

<div align="center">

**Network & Analysis**

![Wireshark](https://img.shields.io/badge/Wireshark-1679A7?style=flat-square&logo=Wireshark&logoColor=white)
![Nmap](https://img.shields.io/badge/Nmap-214478?style=flat-square)
![hping3](https://img.shields.io/badge/hping3-333333?style=flat-square)

**SIEM & Threat Intelligence**

![Splunk](https://img.shields.io/badge/Splunk-000000?style=flat-square&logo=Splunk&logoColor=white)
![VirusTotal](https://img.shields.io/badge/VirusTotal-3949AB?style=flat-square)
![CyberChef](https://img.shields.io/badge/CyberChef-4CAF50?style=flat-square)

**Endpoint Visibility**

![Sysmon](https://img.shields.io/badge/Sysmon-0078D4?style=flat-square&logo=Windows&logoColor=white)
![Windows Event Logs](https://img.shields.io/badge/Windows_Event_Logs-0078D4?style=flat-square&logo=Microsoft&logoColor=white)

**Offensive Security**

![Metasploit](https://img.shields.io/badge/Metasploit-2596CD?style=flat-square)
![Burp Suite](https://img.shields.io/badge/Burp_Suite-FF6633?style=flat-square&logo=PortSwigger&logoColor=white)
![Nessus](https://img.shields.io/badge/Nessus-00B0D8?style=flat-square)
![Kali Linux](https://img.shields.io/badge/Kali_Linux-557C94?style=flat-square&logo=Kali-Linux&logoColor=white)

**Infrastructure**

![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?style=flat-square&logo=VirtualBox&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=flat-square&logo=Ubuntu&logoColor=white)
![Windows](https://img.shields.io/badge/Windows_10%2F11-0078D4?style=flat-square&logo=Microsoft&logoColor=white)

</div>

---

## `$ cat ./projects`

### 🔷 SOC Lab — CFSS India Internship
`Jan–Feb 2026  ·  ~160 hrs  ·  VirtualBox · Splunk · Windows 10`

A structured 4-task internship replicating enterprise SOC workflows in an isolated lab. Every artefact documented.

<details>
<summary><b>Task 1 — SIEM & Log Ingestion</b></summary>

- Deployed **Splunk Enterprise 9.x** + Universal Forwarder on Windows 10 VM
- Configured `inputs.conf` to ingest **4 log sources**: Security, System, Application, Sysmon
- Validated Event IDs **4624, 4625, 4688** and Sysmon EID 1 via SPL queries

</details>

<details>
<summary><b>Task 2 — Network Attack Detection</b></summary>

- Simulated **Nmap SYN scan** and **hping3 SYN flood** (port 445)
- Captured ~700 SYN packets/sec with **Wireshark 4.x**
- Distinguished flood vs. scan patterns using targeted display filters

</details>

<details>
<summary><b>Task 3 — Threat Hunting & Alert Rules</b></summary>

- Wrote **4 SPL detection rules**: brute-force login, new service creation, scheduled task abuse, suspicious PowerShell
- Tuned brute-force threshold across **3 iterations** to reduce false positives
- Mapped **7 MITRE ATT&CK techniques** across T1059, T1053, T1110 and others
- Decoded Base64 PowerShell payload via **CyberChef** → verified clean on VirusTotal (0/70)

</details>

<details>
<summary><b>Task 4 — Incident Response (NIST SP 800-61r2)</b></summary>

- Executed full IR lifecycle for a simulated EID 4688 malware scenario
- **Isolation achieved in 8 minutes** → Containment → Eradication → Recovery
- **60-minute post-recovery monitoring** window with no re-infection
- Authored **Phishing IR Playbook** (8 steps, P1–P4 severity matrix, IOC tracking table)
- Built **3-panel Splunk dashboard** with 30-day event window

</details>

📁 [View artifacts → SPL queries · IR playbook · MITRE mapping · dashboard JSON](./soc-lab-cfss)

---

### 🔷 Penetration Testing Lab — Metasploitable 2
`2025–2026  ·  VirtualBox · Metasploit 6.x · Kali Linux`

Isolated ethical hacking lab with a focus on offensive techniques and building equivalent defensive detection.

| CVE | Service | Impact | Outcome |
|-----|---------|--------|---------|
| CVE-2011-2523 | vsftpd 2.3.4 | Backdoor | Root shell |
| CVE-2007-2447 | Samba usermap_script | RCE | Root shell |
| CVE-2010-2075 | UnrealIRCd | Backdoor | Root shell |

- Reconnaissance via Nmap SYN scan → **9 open services** enumerated
- **6 findings** documented: CVE reference, CVSS score, exploitation steps, remediation
- Backdoor exploit activity mapped to **Sysmon network connection events** → fed into Splunk detection rules from SOC lab

📁 [View vulnerability report](https://github.com/tapansatya/penetration-testing-lab)

---

## `$ cat ./certifications`

| Certification | Issuer | Year |
|---|---|---|
| ✅ Certified SOC Analyst | CFSS India | Feb 2026 |
| ✅ CCNA: Cisco Certified Network Associate | Cisco | 2025 |
| ✅ CNSP: Certified Network Security Practitioner | Security Blue Team | 2025 |
| ✅ Advanced Ethical Hacking | CCST | 2025 |
| ✅ Cyber Security Analyst | HackTheBox Academy | 2025 |
| ✅ Virtual Cyber Security | Forage | 2023 |
| 🔄 CEH: Certified Ethical Hacker | EC-Council | In Progress |

---

## `$ ping tapan`

```
PING tapan — awaiting response...

  📧  tapansatyabhogadi@gmail.com
  🔗  linkedin.com/in/tapansb1/

[Reply accepted. Average response time: < 24 hrs]
```

---

<div align="center">
  <sub>Built with curiosity · Secured by practice · Documented for impact</sub>
</div>
