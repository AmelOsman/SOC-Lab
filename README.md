# SOC Lab – Multi-Phase Enterprise Detection Engineering Environment

## Overview

This repository documents the design and progressive build-out of a multi-phase Security Operations Center (SOC) lab built using UTM on macOS.

The objective is to simulate enterprise-scale monitoring, detection engineering, incident response, and purple team operations across increasingly complex environments.

Each phase builds upon the previous one — progressing from foundational log visibility to enterprise automation, threat intelligence integration, and detection engineering at scale.

---

# 🟢 Phase 1 – Beginner SOC Foundation  
**Goal:** Understanding log flow and basic endpoint visibility.

## Virtual Machines

| Role | Operating System | Purpose |
|------|------------------|----------|
| 🛡 SOC/SIEM | Security Onion | Evaluation Mode. Log ingestion from all hosts |
| 🏗 Infra | Windows Server 2025 | Domain Controller (Desktop Experience) |
| 🖥 Endpoint 1 | Windows 11 | Sysmon installed. Log forwarding to SIEM |
| 🖥 Endpoint 2 | Ubuntu 22.04 | Syslog monitoring |
| 🔴 Attacker | Kali Linux | Nmap, Metasploit, manual exploitation |
| 🧨 Target | Metasploitable 2 | Vulnerable Linux host |
| 📋 Docs | Notion / Spreadsheet | Alert documentation & investigation tracking |

## Deliverables

- Log flow diagram (host → SIEM visibility)
- One completed incident report (e.g., Nmap scan)
- Sysmon Event ID reference sheet (self-built)

---

# 🟡 Phase 2 – Intermediate Enterprise SOC  
**Goal:** Active Directory attacks, lateral movement, telemetry enrichment.

## Virtual Machines

| Role | Operating System | Purpose |
|------|------------------|----------|
| 🛡 SOC/SIEM | Security Onion | Elastic Agent for Windows nodes |
| 🏗 Infra 1 | Windows Server 2025 | Primary Domain Controller |
| 🏗 Infra 2 | Windows Server 2025 | Member Server (SQL/Print simulation) |
| 🖥 Endpoint 1 | Windows 11 | Standard user workstation |
| 🖥 Endpoint 2 | Windows 11 | Admin/IT workstation |
| 🖥 Endpoint 3 | Windows 7 | Legacy detection gap comparison |
| 🖥 Endpoint 4 | Ubuntu 22.04 | Syslog forwarding |
| 🔴 Attacker | Kali Linux | BloodHound, SharpHound, Impacket |
| 🧨 Target | Metasploitable 3 | Modern vulnerable target |
| 📦 Log Aggregation | Graylog / WEF | Independent log forwarding architecture |
| 📋 Management | TheHive | Case management per attack scenario |

## Deliverables

- Full lateral movement scenario documented (compromise → pivot → detection)
- BloodHound attack path analysis with defensive explanation
- False positive tuning write-up
- MITRE ATT&CK mapping for 3+ attacks

---

# 🔵 Phase 3 – Advanced SOC / Security Engineering  
**Goal:** Network segmentation, DFIR, detection engineering, telemetry comparison.

## Virtual Machines & Components

| Role | Technology | Purpose |
|------|------------|----------|
| 🛡 SOC/SIEM | Security Onion + Splunk (Free) / Elastic | Parallel stack comparison |
| 🌐 Perimeter | pfSense | Firewall + log forwarding |
| 📦 Log Collector | Ubuntu Server | Dedicated rsyslog aggregator |
| 🏗 Infra | Windows Server 2025 x3 | DC, Certificate Authority, File Server |
| 🖥 Endpoints | Windows 11 x3 | Velociraptor DFIR agents |
| 🖥 Legacy | Windows Server 2008 R2 | Detection gap analysis |
| 🖥 App Server | Ubuntu Server | Docker (Juice Shop + DVWA) |
| 🔴 Attacker | Kali Linux | Web exploitation & pivoting |
| 🧨 Targets | DVWA + OWASP BWA | Web vulnerability testing |

## Deliverables

- Custom detection rule (Elastic or Splunk) with MITRE mapping
- DFIR investigation using Velociraptor
- False positive tuning write-up (web signature)
- Network segmentation diagram
- Certificate abuse attack walkthrough (ESC1/ESC8)

---

# 🟣 Phase 4 – Elite / Purple Team Simulation  
**Goal:** Automation, threat intelligence, detection engineering at enterprise scale.

## Infrastructure Components

| Role | Technology | Purpose |
|------|------------|----------|
| 🛡 SOC/SIEM | Security Onion | Central aggregation & alerting |
| 🛡 EDR/HIDS | Wazuh Manager | Endpoint monitoring & FIM |
| 🛡 SOAR | Shuffle | Automated response playbooks |
| 🛡 Threat Intel | MISP | IOC synchronization |
| 🌐 Network | pfSense x2 | Perimeter + internal segmentation |
| 🏗 Infra | Windows Server 2025 x4 | DCs + App + Database |
| 🖥 Endpoints | Windows 11 x3–5 | Mixed hardening levels |
| 🖥 Legacy | Windows Server 2008 R2 | Realistic attack surface |
| 🖥 Linux | Ubuntu Desktop + Server | Mixed environment |
| 🔴 Attacker | Kali Linux | Manual red team operations |
| 🔴 Validation | Atomic Red Team | Scripted ATT&CK TTP execution |
| 🗺 Coverage | ATT&CK Navigator | Detection coverage mapping |

## Deliverables

- Full repeatable incident scenario (credential attack → lateral movement → exfiltration → detection → case management → timeline → lessons learned)
- SOAR automation write-up
- ATT&CK Navigator coverage map
- False positive tuning documentation (2+ automated rules)
- Detection engineering report (version-controlled rules)
- Final portfolio summary tying all phases together

---

# Skills Demonstrated

- Enterprise SIEM deployment
- Active Directory attack detection
- Detection engineering & tuning
- DFIR investigations
- Network segmentation architecture
- Firewall telemetry analysis
- Web attack detection
- Purple team simulation
- SOAR automation
- Threat intelligence integration
- MITRE ATT&CK coverage mapping
- Structured incident documentation

---

## Purpose

This lab represents a structured progression from foundational SOC analysis to enterprise-level detection engineering and purple team capability.

It is designed to demonstrate practical, hands-on readiness for enterprise and federal cybersecurity roles.
