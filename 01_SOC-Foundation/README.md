# Phase 1 – SOC Foundation

## Overview

Phase 1 establishes a foundational Security Operations Center (SOC) lab built in UTM on macOS. The purpose of this phase is to deploy a centralized Wazuh SIEM, simulate attacker activity, and analyze generated alerts across a structured multi-VM environment. This lab provides hands-on practice with endpoint visibility, log collection, alert analysis, and basic detection workflows.

## Virtual Machine Roles

| Role | Operating System | Purpose |
|------|------------------|----------|
| 🛡 SOC / SIEM | Ubuntu Desktop with Wazuh | Centralized log collection, alerting, and investigation |
| 🏗 Infrastructure | Windows Server 2025 | Enterprise services and Active Directory foundation |
| 🖥 Endpoint 1 | Windows 11 | Primary enterprise workstation with Sysmon and Wazuh agent |
| 🖥 Endpoint 2 | Ubuntu 22.04 | Linux endpoint for log monitoring and agent-based visibility |
| 🔴 Attacker | Kali Linux | Attack simulation using reconnaissance and exploitation tools |
| 🧨 Vulnerable Target | Metasploitable 2 | Intentionally vulnerable target for testing detections |
| 📋 Documentation | Notion / Spreadsheet | Alert tracking, investigation notes, and incident workflow documentation |

## Objectives

- Deploy Wazuh as the centralized SIEM platform
- Build and configure the Phase 1 multi-VM SOC lab in UTM
- Install Sysmon on Windows 11 for enhanced endpoint telemetry
- Connect Windows and Linux endpoints to Wazuh
- Validate log ingestion and alert generation
- Simulate reconnaissance and exploitation activity
- Analyze alerts and document findings in structured incident reports

## Skills Demonstrated

- Wazuh deployment and configuration
- Multi-VM SOC lab architecture
- Endpoint monitoring and telemetry collection
- Sysmon installation and Windows event visibility
- Linux log monitoring
- Attack simulation and basic adversary emulation
- Alert investigation and validation
- Incident documentation
- MITRE ATT&CK mapping

## Environment Architecture

Wazuh is deployed on an Ubuntu Desktop virtual machine and serves as the central monitoring platform for the lab. Windows and Linux endpoints are configured to forward relevant telemetry to Wazuh for analysis and alerting.

The Phase 1 environment includes:

- A central Wazuh server for visibility and alert analysis
- A Windows 11 endpoint configured with Sysmon and the Wazuh agent
- An Ubuntu 22.04 endpoint for Linux monitoring
- A Windows Server 2025 system for infrastructure testing
- A Kali Linux attacker VM for reconnaissance and exploitation
- A Metasploitable 2 target for vulnerable service testing

All systems are placed within the lab environment to support controlled monitoring, attack simulation, and alert generation.

## Attack Simulations

- Nmap port scanning
- Service enumeration
- Metasploit exploitation testing
- Alert validation in Wazuh

## Repository Structure

- VM build guides are located in `01_SOC-Foundation/VM-Build-Guides`
- Attack simulations are documented in `01_SOC-Foundation/Attack-Simulations`
- Incident reports are stored in `01_SOC-Foundation/Incident-Reports`
- Supporting screenshots are located in `01_SOC-Foundation/Screenshots`

## Next Phase

Phase 2 expands this lab into a more advanced enterprise detection environment with domain-connected systems, credential attack scenarios, lateral movement detection, and deeper detection engineering workflows.

This phase builds the foundation for enterprise-level SOC operations, blue team analysis, and detection engineering practice.
