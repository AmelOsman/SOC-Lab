# Kali Linux Attacker Configuration Guide (Phase 1)

## Objective

Deploy Kali Linux as the attacker machine used to simulate reconnaissance and exploitation activity against monitored hosts in the SOC lab.

This machine generates detectable activity for validation and alert tuning.

---

## VM Specifications

CPU: 2–4 cores  
RAM: 4–8 GB  
Disk: 40–60 GB  
Network Adapter: Internal (Lab Network)

---

## Step 1 – Install Kali Linux

1. Create new VM in UTM
2. Attach Kali ISO
3. Select Graphical Install
4. Complete setup
5. Set root or user password
6. Confirm system boots

---

## Step 2 – Configure Static IP Address

Edit network configuration:

```
sudo nano /etc/network/interfaces
```

Add:

```
auto eth0
iface eth0 inet static
address 192.168.100.50
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

## Step 3 – Confirm Installed Tools

Kali comes preinstalled with:

- nmap
- Metasploit Framework
- Netcat
- Burp Suite
- Hydra

Verify:

```
which nmap
which msfconsole
```

---

## Step 4 – Reconnaissance Test

Run TCP SYN scan against Windows endpoint:

```
nmap -sS 192.168.100.20
```

Run service version detection:

```
nmap -sV 192.168.100.20
```

Expected Result:
- Security Onion generates alerts
- Sysmon logs network connection events

---

## Step 5 – Basic Metasploit Test (Optional)

Start Metasploit:

```
msfconsole
```

Search for exploit:

```
search vsftpd
```

(Used later in Metasploitable testing)

---

## Validation Checklist

- Static IP configured
- Can ping Domain Controller
- Can ping Windows 11 endpoint
- Nmap scan generates alert in Security Onion
- Logs visible in Elastic

---

## Skills Demonstrated

- Attacker infrastructure setup
- Static IP configuration (Linux)
- Network reconnaissance
- Detection validation
- SIEM alert verification
