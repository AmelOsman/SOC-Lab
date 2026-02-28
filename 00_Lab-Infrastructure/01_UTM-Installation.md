# UTM Installation Guide (macOS)

## Objective

Install UTM on macOS to serve as the virtualization platform for the SOC Lab environment.

This document ensures the lab environment is reproducible and standardized.

## System Requirements

- macOS (Apple Silicon or Intel)
- Minimum 16 GB RAM recommended
- Minimum 200 GB free disk space
- Administrative privileges

## Step 1 — Download UTM

1. Navigate to: https://mac.getutm.app
2. Download the latest version for macOS
3. Open the downloaded `.dmg` file
4. Drag UTM into the Applications folder

## Step 2 — Grant Permissions

1. Open **System Settings**
2. Navigate to:
   Privacy & Security → Full Disk Access
3. Ensure UTM has permission (if prompted)

## Step 3 — Initial Launch

1. Open UTM from Applications
2. Allow any macOS security prompts
3. Confirm UTM launches successfully

## Step 4 — Networking Standards for SOC Lab

All virtual machines will follow these network rules:

- Internal Network: Used for lab communication and attack simulation
- NAT Adapter: Used only when internet access is required
- Bridged Mode: NOT used (prevents exposure to host network)

This ensures:
- Safe attack simulation
- Network segmentation
- No exposure to home or enterprise LAN

## Validation

Confirm:
- UTM launches without error
- You can create a new virtual machine
- Internal network option is available

## Outcome

UTM is successfully installed and ready to host the multi-VM SOC lab environment.

This serves as the virtualization foundation for all subsequent lab phases.
