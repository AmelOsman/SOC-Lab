# Phase 1 – SOC Foundation

## Executive Summary

Phase 1 establishes a foundational Security Operations Center (SOC) lab environment built on macOS using UTM virtualization.

The objective of this phase was to design, deploy, and validate a centralized SIEM architecture capable of ingesting, correlating, and alerting on multi-platform telemetry across a segmented internal lab network.

This environment simulates a small enterprise domain with both Windows and Linux systems, attacker simulation, and centralized detection engineering workflows.

---

## Architecture Overview

**SIEM Platform**
- Security Onion (Evaluation Mode)
- Elastic Stack backend
- Dual-NIC configuration (Internal + Internet)

**Infrastructure**
- Windows Server 2025 (Domain Controller)
- Active Directory Services
- Static IP architecture

**Endpoints**
- Windows 11 (Sysmon telemetry)
- Ubuntu 22.04 (Syslog forwarding)

**Adversary Simulation**
- Kali Linux (Nmap, Metasploit)
- Metasploitable 2 (Vulnerable Linux target)

---

## Detection Validation

Test scenario executed:

- Nmap SYN scan from Kali
- Logs ingested into Security Onion
- Alert generated
- Event validated in Elastic

This confirmed:
- Log flow integrity
- Alerting functionality
- Cross-platform visibility
- Network segmentation working correctly

---

## Skills Demonstrated

- SIEM deployment and configuration
- Active Directory setup
- Static IP network design
- Multi-platform log ingestion
- Endpoint telemetry configuration (Sysmon + Syslog)
- Offensive security simulation
- Alert validation workflow
- Detection engineering fundamentals

---

## Phase Outcome

A fully functional, multi-VM SOC lab capable of:

- Centralized log collection
- Attack detection
- Alert analysis
- Cross-platform telemetry monitoring
- Structured documentation for enterprise scaling

This phase provides the foundation for Phase 2 (Enterprise Detection Engineering & AD Attack Simulation).
