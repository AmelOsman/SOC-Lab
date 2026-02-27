# Screenshot & Documentation Standards

## Objective

Define standardized screenshot and documentation practices for the SOC Lab repository.

This ensures:
- Professional presentation
- Clear validation evidence
- Reproducibility
- Recruiter-friendly documentation

---

## General Screenshot Rules

1. Every screenshot must prove something.
2. Every screenshot must include a short explanation.
3. Screenshots must not expose:
   - Real public IP addresses
   - Passwords
   - Sensitive credentials
   - Personal system details

---

## Required Screenshot Types (Phase 1)

### Infrastructure Validation

- UTM VM configuration (CPU, RAM, Disk)
- NIC configuration (Internal + NAT for SIEM)
- Internal network selection confirmation

### Domain Controller

- Static IP configuration
- AD DS installed
- Domain visible (soclab.local)
- Test users created

### Endpoint Validation

- Windows 11 domain joined
- Sysmon service running
- Event Viewer showing Sysmon logs

### Linux Endpoint

- Static IP confirmation (`ip a`)
- Syslog forwarding configuration
- Test log generation

### Attacker Validation

- Nmap scan results
- Metasploit module execution (if applicable)

### SIEM Validation

- Security Onion dashboard
- Alert triggered from scan
- Elastic log entry indexed

---

## Screenshot Naming Convention

Store screenshots in:

`/01_SOC-Foundation/Screenshots/`

Name format:

Phase-Component-Description.png

Examples:

P1-UTM-VMConfig.png  
P1-DC-StaticIP.png  
P1-WS11-SysmonInstalled.png  
P1-Kali-NmapScan.png  
P1-SIEM-AlertTriggered.png  

---

## Screenshot Markdown Formatting

When embedding screenshots in documentation:

Use:

```markdown
![Description](../Screenshots/P1-DC-StaticIP.png)
