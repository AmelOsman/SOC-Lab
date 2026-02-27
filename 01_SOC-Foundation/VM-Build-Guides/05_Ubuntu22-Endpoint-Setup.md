# Ubuntu 22.04 Endpoint Setup Guide (Phase 1)

## Objective

Deploy Ubuntu 22.04 as a Linux endpoint within the Phase 1 SOC lab and configure Syslog forwarding to Security Onion.

This system validates Linux log ingestion and cross-platform visibility.

---

## VM Specifications

CPU: 2 cores  
RAM: 4 GB  
Disk: 40 GB  
Network Adapter: Internal (Lab Network)

---

## Step 1 – Install Ubuntu 22.04

1. Create new VM in UTM
2. Attach Ubuntu 22.04 ISO
3. Select minimal installation
4. Create local user account
5. Complete installation

---

## Step 2 – Configure Static IP

Edit netplan configuration:

```
sudo nano /etc/netplan/01-netcfg.yaml
```

Example configuration:

```
network:
  version: 2
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.100.40/24
      gateway4: 192.168.100.1
      nameservers:
        addresses:
          - 192.168.100.10
```

Apply changes:

```
sudo netplan apply
```

Verify:

```
ip a
ping 192.168.100.10
```

---

## Step 3 – Configure Syslog Forwarding

Install rsyslog (if not installed):

```
sudo apt update
sudo apt install rsyslog -y
```

Edit rsyslog config:

```
sudo nano /etc/rsyslog.conf
```

Add to bottom:

```
*.* @192.168.100.10:514
```

Restart service:

```
sudo systemctl restart rsyslog
```

---

## Step 4 – Generate Test Logs

Create test log entries:

```
logger "Ubuntu test log entry"
```

Confirm in Security Onion:

- Log visible in Elastic
- Source IP = 192.168.100.40
- Event indexed properly

---

## Validation

Confirm:

- Logs searchable in Elastic
- No ingestion errors
- Source recognized correctly
- Event timestamp accurate

---

## Troubleshooting

No logs visible:
- Confirm Security Onion listening on port 514
- Verify correct IP address
- Confirm rsyslog service running
- Confirm firewall not blocking UDP 514

---

## Skills Demonstrated

- Linux endpoint deployment
- Static IP configuration (netplan)
- Syslog forwarding architecture
- Log ingestion validation
- Cross-platform telemetry monitoring
