# Phase 1 – SOC Foundation

## Overview

This phase establishes a foundational Security Operations Center (SOC) lab built using UTM on macOS. The objective is to deploy a centralized SIEM platform, simulate attack activity, and analyze generated alerts within a structured multi-VM environment.

## Virtual Machine Roles

| Role | Operating System | Purpose |
|------|------------------|----------|
| 🛡 SOC / SIEM | Security Onion | Centralized log collection, alerting, and investigation |
| 🏗 Infrastructure | Windows Server 2025 | Enterprise services and Active Directory foundation |
| 🖥 Endpoint 1 | Windows 11 | Primary enterprise workstation |
| 🖥 Endpoint 2 | Ubuntu 22.04 | Linux endpoint monitoring |
| 🔴 Attacker | Kali Linux | Attack simulation (Nmap, Metasploit) |
| 🧨 Vulnerable Target | Metasploitable 2 | Exploitation testing target |
| 📋 Documentation | Notion / Spreadsheet | Incident tracking and investigation workflow |

## Objectives

- Deploy Security Onion in Evaluation Mode
- Configure dual NIC architecture
- Validate log ingestion from endpoints
- Simulate reconnaissance and exploitation
- Analyze SIEM alerts
- Document findings in structured incident reports

## Skills Demonstrated

- SIEM deployment and configuration
- Enterprise VM architecture planning
- Network segmentation
- Attack simulation
- Alert analysis
- Incident documentation
- MITRE ATT&CK mapping

## Environment Architecture

Security Onion is configured with:

- NIC 1: Management / Internet
- NIC 2: Internal Monitoring Network

All endpoints reside on the internal network to ensure monitored traffic visibility.

## Attack Simulations

- Nmap port scanning
- Service enumeration
- Metasploit exploitation testing
- Alert validation in Security Onion


## Repository Structure

- VM build guides are located in `01_SOC-Foundation/VM-Build-Guides`
- Attack simulations are documented in `01_SOC-Foundation/Attack-Simulations`
- Incident reports are stored in `01_SOC-Foundation/Incident-Reports`
- Supporting screenshots are located in `01_SOC-Foundation/Screenshots`

## Next Phase

Phase 2 expands this lab into a full enterprise environment including domain-joined endpoints, credential attacks, lateral movement detection, and detection engineering.

This phase establishes the technical foundation for enterprise-level detection engineering and blue team operations.
