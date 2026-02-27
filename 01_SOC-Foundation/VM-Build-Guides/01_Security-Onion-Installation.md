# Security Onion Installation Guide (Phase 1)

## Objective
Deploy Security Onion in Evaluation Mode as the centralized SIEM platform for the Phase 1 SOC lab.

## VM Specifications

| Setting | Value |
|----------|--------|
| CPU | 4 cores minimum |
| RAM | 8–16 GB recommended |
| Disk | 200 GB |
| Network Adapter 1 | Internal (Lab Network) |
| Network Adapter 2 | NAT or Bridged (Internet access) |

## Installation Steps

### 1. Boot from ISO
- Attach Security Onion ISO in UTM
- Start VM
- Select **Install Security Onion**

### 2. Choose Deployment Mode
- Select: **Evaluation Mode**
- Accept default Elastic configuration

### 3. Network Configuration
- Assign:
  - Management NIC → DHCP (internet access)
  - Monitoring NIC → Internal lab network

### 4. Create Admin Account
- Set strong credentials
- Document them securely

## Post-Install Validation

### Access Web Interface
Navigate to:

https://
Login with created credentials.

---

## Log Ingestion Configuration

Phase 1 sources:
- Windows 11 (Sysmon)
- Ubuntu 22.04 (Syslog)
- Windows Server 2025
- Metasploitable 2

Validate:
- Logs visible in Elastic
- Alerts generating from test activity (Nmap scan)

---

## Validation Test

From Kali:

nmap -sS 
Confirm:
- Alert appears in Security Onion
- Event logged in Elastic

---

## Troubleshooting Notes

| Issue | Fix |
|-------|------|
| No logs appearing | Verify agent installed |
| No alerts triggering | Confirm correct NIC configuration |
| Web UI unreachable | Check firewall rules |

---

## Skills Demonstrated

- SIEM deployment
- Dual NIC configuration
- Log ingestion validation
- Basic attack detection
- Alert analysis workflow
