# 👋 Hello, I'm Tapan Satya

<a href="https://www.linkedin.com/in/tapansb1/">
<img src="https://img.shields.io/badge/-LinkedIn-0072b1?&style=for-the-badge&logo=linkedin&logoColor=white" />
</a>
<a href="mailto:tapansatyabhogadi@gmail.com">
<img src="https://img.shields.io/badge/-Email-D14836?&style=for-the-badge&logo=gmail&logoColor=white" />
</a>

---

## 🧭 Objective

Final-year B.Tech IT student (graduating June 2026) with a **2-month supervised SOC internship** at CFSS India (~160 lab hours) and **5 certifications** including CCNA and CNSP. Built a VirtualBox SOC lab from scratch — configured Splunk SIEM, wrote 6 detection rules covering 7 MITRE ATT&CK techniques, executed 4 simulated attack scenarios, and authored an IR playbook following the NIST framework. Actively seeking a **Tier-1 SOC Analyst** role to apply structured training in a real environment.

---

## 🛠️ Skills & Projects

| Skill | Associated Project |
|-------|-------------------|
| SIEM Implementation & Log Ingestion | SOC Lab — CFSS Internship |
| SPL Query Writing & Alert Tuning | SOC Lab — CFSS Internship |
| Network Attack Detection (SYN Flood, Port Scan) | SOC Lab — CFSS Internship |
| Threat Hunting & MITRE ATT&CK Mapping | SOC Lab — CFSS Internship |
| Incident Response (NIST SP 800-61r2) | SOC Lab — CFSS Internship |
| Penetration Testing & CVE Exploitation | Pentest Lab — Metasploitable 2 |
| Vulnerability Assessment & Remediation | Pentest Lab — Metasploitable 2 |

---

## 🔧 Tools & Technologies

### 🌐 Network Monitoring & Analysis
<div>
<img src="https://img.shields.io/badge/-Wireshark-1679A7?&style=for-the-badge&logo=Wireshark&logoColor=white" />
<img src="https://img.shields.io/badge/-Nmap-214478?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-hping3-333333?&style=for-the-badge&logoColor=white" />
</div>

### 🖥️ Endpoint & Log Sources
<div>
<img src="https://img.shields.io/badge/-Sysmon-000000?&style=for-the-badge&logo=Windows&logoColor=white" />
<img src="https://img.shields.io/badge/-Windows_Event_Logs-0078D4?&style=for-the-badge&logo=Microsoft&logoColor=white" />
</div>

### 📊 SIEM & Threat Analysis
<div>
<img src="https://img.shields.io/badge/-Splunk-000000?&style=for-the-badge&logo=Splunk&logoColor=white" />
<img src="https://img.shields.io/badge/-VirusTotal-3949AB?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-CyberChef-4CAF50?&style=for-the-badge&logoColor=white" />
</div>

### ⚔️ Offensive Security
<div>
<img src="https://img.shields.io/badge/-Metasploit-2596CD?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-Burp_Suite-FF6633?&style=for-the-badge&logo=PortSwigger&logoColor=white" />
<img src="https://img.shields.io/badge/-Nessus-00B0D8?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-Kali_Linux-557C94?&style=for-the-badge&logo=Kali-Linux&logoColor=white" />
</div>

### ⚙️ Virtualisation & OS
<div>
<img src="https://img.shields.io/badge/-VirtualBox-183A61?&style=for-the-badge&logo=VirtualBox&logoColor=white" />
<img src="https://img.shields.io/badge/-Windows_10/11-0078D4?&style=for-the-badge&logo=Microsoft&logoColor=white" />
<img src="https://img.shields.io/badge/-Ubuntu-E95420?&style=for-the-badge&logo=Ubuntu&logoColor=white" />
</div>

---

## 🚀 Projects

### 🔍 SOC Lab — CFSS India Internship (Jan–Feb 2026) | ~160 hrs
> Structured 4-task internship simulating enterprise SOC operations on an isolated VirtualBox environment.

- **Task 1 — SIEM & Log Ingestion:** Deployed Splunk Enterprise 9.x + Universal Forwarder on Windows 10 VM. Configured `inputs.conf` to forward 4 log sources (Security, System, Application, Sysmon). Validated Event IDs 4624, 4625, 4688, and Sysmon EID 1 via SPL.
- **Task 2 — Network Attack Detection:** Ran Nmap SYN scan and hping3 SYN flood. Captured with Wireshark 4.x — identified ~700 SYN/sec flood on port 445. Distinguished flood vs. scan patterns using display filters.
- **Task 3 — Threat Hunting & Alert Rules:** Wrote 4 SPL detection rules (brute-force, new service, scheduled task, suspicious PowerShell). Tuned brute-force threshold across 3 iterations. Mapped 7 MITRE ATT&CK techniques. Decoded Base64 PowerShell via CyberChef; verified with VirusTotal (0/70 detections).
- **Task 4 — Incident Response (NIST):** Executed full IR lifecycle for simulated malware scenario (EID 4688): Detection → Isolation (8 min) → Containment → Eradication → Recovery → 60-min post-recovery monitoring. Authored Phishing IR Playbook (8 steps, severity matrix P1–P4, IOC tracking). Built 3-panel Splunk dashboard (30-day window).

📁 [View artifacts: SPL queries, IR playbook, MITRE mapping, dashboard JSON](./soc-lab-cfss)

---

### 🎯 Penetration Testing Lab — Metasploitable 2 (2025–2026)
> Isolated VirtualBox lab for ethical hacking practice and defensive insight mapping.

- **Reconnaissance:** Nmap SYN scan — discovered 9 open services on Metasploitable 2.
- **Exploitation:** Exploited 3 Critical CVEs using Metasploit 6.x:
  - `CVE-2011-2523` — vsftpd 2.3.4 backdoor → root shell
  - `CVE-2007-2447` — Samba usermap_script RCE → root shell
  - `CVE-2010-2075` — UnrealIRCd backdoor → root shell
- **Remediation Documentation:** For each of 6 findings: CVE reference, CVSS score, exploitation steps, and specific remediation recommendations.
- **Defensive Mapping:** Backdoor exploits mapped to Sysmon network connection events and Splunk detection rules built in the SOC lab.

📁 [View lab vulnerability report](./pentest)

---

## 📜 Certifications

<div>
<img src="https://img.shields.io/badge/-Certified_SOC_Analyst-1F4E79?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-CCNA-1BA0D7?&style=for-the-badge&logo=Cisco&logoColor=white" />
<img src="https://img.shields.io/badge/-CNSP-2E7D32?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-Advanced_Ethical_Hacking-8B0000?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-Cyber_Security_Analyst_(HTB)-9FEF00?&style=for-the-badge&logo=HackTheBox&logoColor=black" />
<img src="https://img.shields.io/badge/-Virtual_Cyber_Security_(Forage)-00897B?&style=for-the-badge&logoColor=white" />
<img src="https://img.shields.io/badge/-CEH_(In_Progress)-FF6F00?&style=for-the-badge&logoColor=white" />
</div>

| Certification | Issuer | Year |
|--------------|--------|------|
| Certified SOC Analyst | CFSS India | Feb 2026 |
| CCNA: Cisco Certified Network Associate | Cisco | 2025 |
| CNSP: Certified Network Security Practitioner | Security Blue Team | 2025 |
| Advanced Ethical Hacking | CCST | 2025 |
| Cyber Security Analyst | HackTheBox Academy | 2025 |
| Virtual Cyber Security | Forage | 2023 |
| CEH: Certified Ethical Hacker | EC-Council | 🔄 In Progress |

---

## 📫 Contact
- 📧 Email: tapansatyabhogadi@gmail.com
- 🔗 LinkedIn: https://www.linkedin.com/in/tapansb1/
