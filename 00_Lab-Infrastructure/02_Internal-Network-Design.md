# Internal Network Design (SOC Lab)

## Objective

Define and standardize the internal network architecture used in the Phase 1 SOC lab.

This design ensures:
- Safe attack simulation
- Controlled segmentation
- Proper log visibility
- No exposure to the host or home network

---

## Network Model Overview

All virtual machines operate inside an isolated UTM Internal Network.

Security Onion has:
- 1x Internal Adapter (lab traffic monitoring)
- 1x NAT Adapter (internet access for updates only)

All other VMs use:
- Internal Adapter only

Bridged mode is NOT used.

---

## Logical Architecture Diagram

```
[ Internet ]
      |
   (NAT Adapter)
      |
---------------------
|  Security Onion  |
---------------------
      |
[ Internal Network Switch ]
   |       |       |       |        |
 Win11   Ubuntu   Kali   Metasploitable  Windows Server DC
```

---

## Network Segmentation Logic

### Security Onion
- Acts as centralized SIEM
- Monitors all internal lab traffic
- Receives logs from endpoints

### Windows Server 2025
- Domain Controller
- DNS for lab
- Static IP required

### Windows 11
- Domain joined endpoint
- Sysmon installed
- Forwards logs to Security Onion

### Ubuntu 22.04
- Linux endpoint
- Syslog forwarding configured

### Kali Linux
- Attacker machine
- Used for:
  - Nmap scans
  - Exploit testing
  - Lateral movement simulation

### Metasploitable 2
- Vulnerable Linux target
- Used for exploitation validation

---

## IP Addressing Standard

Recommended Static IP Range:

192.168.100.0/24

Example Assignments:

- Security Onion: 192.168.100.10
- Windows Server DC: 192.168.100.20
- Windows 11: 192.168.100.30
- Ubuntu: 192.168.100.40
- Kali: 192.168.100.50
- Metasploitable: 192.168.100.60

Gateway:
Not required (internal network only)

DNS:
Windows Server DC (192.168.100.20)

---

## Security Design Decisions

1. No Bridged Networking  
   Prevents lab traffic from reaching home LAN.

2. Security Onion as Monitoring Hub  
   All log visibility centralized.

3. Static IP Infrastructure  
   Required for:
   - Domain stability
   - DNS resolution
   - Log forwarding consistency

4. NAT Only Where Necessary  
   Reduces attack surface.

---

## Validation Checklist

Before moving to VM builds:

- Internal network created in UTM
- Security Onion configured with dual NICs
- All other VMs assigned internal adapter
- IP addressing plan documented

---

## Outcome

A properly segmented, enterprise-style lab network designed for:

- Detection engineering
- Attack simulation
- Log pipeline validation
- SOC workflow development

This architecture mirrors real-world SOC infrastructure segmentation.
