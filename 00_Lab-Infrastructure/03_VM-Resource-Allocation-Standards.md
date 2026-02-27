# VM Resource Allocation Standards

## Objective

Define standardized CPU, RAM, disk, and naming conventions for all virtual machines in the SOC Lab.

This ensures:
- Consistency across phases
- Performance balance on macOS host
- Reproducibility
- Professional infrastructure documentation

---

## Host System Assumptions

Recommended Host Specs:
- 16–32 GB RAM
- Apple Silicon or modern Intel CPU
- Minimum 200 GB free disk space

Lab resource allocation must not exceed 70–80% of host capacity.

---

## Standard Resource Allocation

### Security Onion (SIEM)

CPU: 4 cores minimum  
RAM: 8–16 GB  
Disk: 200 GB  
NICs: 2 (Internal + NAT)

Reason:
- Elastic indexing requires memory
- SIEM workloads are heavier than endpoints

---

### Windows Server 2025 (Domain Controller)

CPU: 2–4 cores  
RAM: 8 GB  
Disk: 80–100 GB  
NICs: 1 (Internal)

Reason:
- AD and DNS services require stable memory
- Static IP mandatory

---

### Windows 11 Endpoint

CPU: 2–4 cores  
RAM: 8 GB  
Disk: 80–100 GB  
NICs: 1 (Internal)

Reason:
- Sysmon and logging processes require headroom
- Used for domain testing and telemetry

---

### Ubuntu 22.04 Endpoint

CPU: 2 cores  
RAM: 4 GB  
Disk: 40–60 GB  
NICs: 1 (Internal)

Reason:
- Lightweight log source
- Used for syslog forwarding validation

---

### Kali Linux (Attacker)

CPU: 2–4 cores  
RAM: 4–8 GB  
Disk: 60 GB  
NICs: 1 (Internal)

Reason:
- Supports scanning and exploitation tools
- Requires sufficient RAM for Metasploit

---

### Metasploitable 2

CPU: 1–2 cores  
RAM: 2 GB  
Disk: 20 GB  
NICs: 1 (Internal)

Reason:
- Lightweight vulnerable target
- Used for exploitation validation

---

## Naming Convention Standard

VM names follow this format:

PHASE-ROLE-OS

Examples:

P1-SIEM-SecurityOnion  
P1-DC-WinServer2025  
P1-WS01-Windows11  
P1-LNX01-Ubuntu  
P1-ATT-Kali  
P1-TGT-Metasploitable  

This ensures:
- Clear role identification
- Scalable naming for future phases
- Professional documentation standards

---

## Snapshot Strategy

Before major configuration steps:
- Take VM snapshot
- Label snapshot clearly (e.g., "Pre-Domain-Join")

Snapshots should be taken before:
- Domain promotion
- Agent installation
- Exploit testing
- Major updates

---

## Disk Management Strategy

- Use dynamically allocated disks
- Avoid pre-allocating full disk size unless necessary
- Monitor host disk usage regularly

---

## Performance Monitoring

If macOS becomes slow:
- Reduce running VM count
- Increase host swap space cautiously
- Avoid running all VMs simultaneously unless testing attack chain

---

## Outcome

A standardized and scalable resource allocation framework supporting multi-phase SOC lab growth without destabilizing the macOS host.
