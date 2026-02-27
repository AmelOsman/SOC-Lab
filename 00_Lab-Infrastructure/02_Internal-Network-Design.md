# UTM Network Model (Lab Infrastructure)

## Objective

Define the baseline UTM networking model used across all phases of the SOC Lab.

This document is **phase-agnostic** and describes the safe default network approach for building isolated cybersecurity labs on macOS.

---

## Design Principles

- **Isolation first:** Lab traffic stays inside UTM’s Internal Network
- **No exposure:** Bridged networking is not used
- **Controlled internet access:** NAT is used only when updates or packages are required
- **Reproducible:** Same network model across phases, with phase-specific diagrams stored separately

---

## Network Types Used

### Internal Network (Primary)
Used for:
- VM-to-VM communication inside the lab
- Attack simulation traffic (Kali → targets)
- Log forwarding to Security Onion
- Domain services communication (AD / DNS)

Security benefit:
- Traffic is isolated from your real LAN
- Prevents accidental scanning or pivoting into home/enterprise network

### NAT (Secondary / Temporary)
Used for:
- OS updates
- Package installs (apt, Windows updates)
- Downloading tools/agents when needed

Usage standard:
- Enable NAT only when required
- Disable NAT afterward for maximum isolation

### Bridged Networking (Not Used)
Bridged mode is NOT used in this lab.

Reason:
- Bridged networking can place VMs directly on your real network
- This increases risk and breaks isolation assumptions

---

## Standard NIC Strategy

### Security Onion (2 NICs)
- NIC 1: Internal Network (SOC-LAB)
- NIC 2: NAT (temporary internet access)

### All Other VMs (1 NIC)
- NIC 1: Internal Network (SOC-LAB)

This ensures:
- Security Onion can update when needed
- The lab remains isolated by default

---

## Phase-Based Network Diagrams

Phase-specific diagrams are stored separately (and will expand as the lab evolves):

`/00_Lab-Infrastructure/Network-Diagrams/`

- Phase-1-Network-Diagram
- Phase-2-Network-Diagram
- Phase-3-Network-Diagram
- Phase-4-Network-Diagram

---

## Security Note (Public Repository)

Any IP ranges referenced in this repository use RFC1918 private ranges (e.g., 192.168.x.x) and exist only inside the isolated UTM lab.

No public IPs, credentials, or sensitive environment data are published.

---

## Outcome

A standardized UTM network model that remains consistent across phases while allowing each phase to define its own architecture diagram as complexity increases.
