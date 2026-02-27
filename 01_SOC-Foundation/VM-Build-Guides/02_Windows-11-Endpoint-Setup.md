# Windows 11 Endpoint Configuration Guide (Phase 1)

## Objective

Deploy Windows 11 as a monitored enterprise workstation in the Phase 1 SOC lab.  
Install Sysmon and forward logs to Security Onion for detection validation.

---

## VM Specifications

CPU: 2–4 cores  
RAM: 8 GB recommended  
Disk: 60–100 GB  
Network Adapter: Internal (Lab Network)

---

## Step 1 – Install Windows 11

1. Create new VM in UTM
2. Attach Windows 11 ISO
3. Complete installation
4. Set local Administrator password
5. Confirm system boots successfully

---

## Step 2 – Configure Static IP Address

Open:

Control Panel → Network and Internet → Network Connections

Right-click Ethernet → Properties → IPv4

Set:

IP Address: 192.168.100.20  
Subnet Mask: 255.255.255.0  
Default Gateway: 192.168.100.1  
DNS Server: 192.168.100.10  (Domain Controller IP)

Confirm connectivity:

```
ping 192.168.100.10
```

---

## Step 3 – Join Domain

1. Open System → Rename this PC (Advanced)
2. Click Change
3. Select Domain
4. Enter:

```
soclab.local
```

5. Provide Domain Administrator credentials
6. Reboot

Validate:

```
whoami
```

Should display domain account.

---

## Step 4 – Install Sysmon

Download Sysmon from Microsoft Sysinternals:

https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

Extract zip.

Open Command Prompt as Administrator.

Install with basic config:

```
sysmon -accepteula -i
```

Confirm installation:

```
Get-Service sysmon
```

---

## Step 5 – Verify Log Generation

Open Event Viewer:

Applications and Services Logs → Microsoft → Windows → Sysmon → Operational

Confirm events such as:

Event ID 1 – Process Creation  
Event ID 3 – Network Connection  

---

## Step 6 – Validate Log Ingestion in Security Onion

From Kali:

```
nmap -sS 192.168.100.20
```

In Security Onion:

1. Open Alerts
2. Confirm scan detection
3. Verify logs indexed in Elastic

---

## Validation Checklist

- Static IP configured
- Domain joined
- Sysmon installed
- Logs visible in Event Viewer
- Events visible in Security Onion
- Alert triggered from test scan

---

## Troubleshooting

Cannot join domain:
Confirm DNS is pointing to 192.168.100.10

No logs in Security Onion:
Verify Elastic Agent installed and running

No alerts:
Confirm Windows host is on monitored network segment

---

## Skills Demonstrated

- Windows enterprise configuration
- Static IP networking
- Active Directory domain joining
- Sysmon deployment
- Endpoint log validation
- Detection verification workflow
