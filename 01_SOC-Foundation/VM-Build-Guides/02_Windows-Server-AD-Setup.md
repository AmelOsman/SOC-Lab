# Windows Server 2025 Active Directory Setup Guide (Phase 1)

## Objective

Deploy Windows Server 2025 as the Primary Domain Controller (DC) for the Phase 1 SOC lab environment. Configure Active Directory Domain Services (AD DS), create test users, join endpoints to the domain, and validate log visibility in Security Onion.


## VM Specifications

CPU: 2–4 cores
RAM: 8 GB minimum
Disk: 60–100 GB
Network Adapter: Internal (Lab Network)


## Step 1 – Install Windows Server 2025

1. Create new VM in UTM
2. Attach Windows Server 2025 ISO
3. Select Windows Server 2025 Standard (Desktop Experience)
4. Set Administrator password
5. Complete installation


## Step 2 – Configure Static IP Address

Open:
Control Panel → Network and Internet → Network Connections

Right-click Ethernet → Properties → IPv4

Set:
IP Address: 192.168.100.10
Subnet Mask: 255.255.255.0
Default Gateway: 192.168.100.1
Preferred DNS: 127.0.0.1

Confirm:
ipconfig /all

---

## Step 3 – Install Active Directory Domain Services (AD DS)

Open:
Server Manager → Add Roles and Features

Select:
- Active Directory Domain Services
- DNS Server (if prompted)

Install and reboot if required.

---

## Step 4 – Promote to Domain Controller

Click:
Promote this server to a domain controller

Select:
Add a new forest

Root domain name:
soclab.local

Set Directory Services Restore Mode (DSRM) password.

Click Install.
Server will reboot automatically.

---

## Step 5 – Verify Domain Controller

Open:
Active Directory Users and Computers

Confirm:
- Domain soclab.local exists
- Default Users and Computers containers present

Run:
dcdiag

---

## Step 6 – Create Test Users

Inside:
Active Directory Users and Computers → Users

Create:
analyst1 (Standard user)
itadmin (Domain Admin test account)

Uncheck:
User must change password at next logon

---

## Step 7 – Join Windows 11 to Domain

On Windows 11 VM:

1. Set DNS server to 192.168.100.10
2. Open System → Rename this PC (advanced)
3. Click Change
4. Select Domain
5. Enter: soclab.local
6. Authenticate with domain admin
7. Reboot

Log in as:
soclab\analyst1

---

## Step 8 – Log Ingestion Validation

Validate in Security Onion:
- Windows security logs visible
- Logon events 4624 / 4625
- User creation event 4720
- Domain activity recorded

---

## Test Activity

From Kali:
nmap -sS 192.168.100.10

From Windows 11:
- Log in and out multiple times
- Attempt incorrect password
- Create test file

Confirm:
- Alert appears in Security Onion
- Event indexed in Elastic

---

## Troubleshooting

Cannot join domain:
Confirm DNS points to 192.168.100.10

No logs visible:
Verify agent installed and running

AD install fails:
Ensure static IP configured first

No alerts:
Confirm correct network segment

---

## Skills Demonstrated

- Windows Server deployment
- Active Directory configuration
- Domain management
- Static IP networking
- Endpoint domain joining
- Log ingestion validation
- SIEM verification workflow
