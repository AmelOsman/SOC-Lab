# Lab Infrastructure – UTM Virtualization Setup

## Overview

This section documents the foundational infrastructure used to build the multi-phase SOC lab environment.

All virtual machines in this repository are deployed using UTM on macOS.

This infrastructure layer includes:

- UTM installation on macOS
- Internal lab network creation
- VM configuration standards
- Resource allocation guidelines

This ensures consistency, scalability, and reproducibility of the lab environment.

---

## Network Architecture

All virtual machines are deployed inside an isolated Internal Network within UTM.

Network Model:

- Internal Network: Used for all lab communication and attack simulation
- NAT (Temporary Only): Used for OS updates and package installations
- Bridged Mode: Not used (to prevent exposure to host LAN)

This design ensures:
- Safe attack simulation
- Controlled segmentation
- No risk to home or enterprise network

## Why This Matters

Before deploying enterprise security tools, infrastructure must be:

- Properly segmented
- Resource balanced
- Standardized
- Documented

This folder establishes that baseline.
