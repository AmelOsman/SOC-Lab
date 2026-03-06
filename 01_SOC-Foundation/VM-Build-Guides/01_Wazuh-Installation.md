# Wazuh Installation Guide (Phase 1)

## Objective
Deploy **Wazuh SIEM** on an Ubuntu 24.04 virtual machine to serve as the centralized SIEM platform for the Phase 1 SOC lab environment.

Wazuh provides:

- Security Information and Event Management (SIEM)
- Intrusion detection
- File integrity monitoring
- Log analysis
- Security configuration assessment

# Lab Environment

| Component | Value |
|---|---|
| Host System | Apple Silicon Mac |
| Virtualization Software | UTM |
| Virtualization Mode | Emulation |
| Guest OS | Ubuntu 24.04 Desktop |
| SIEM Platform | Wazuh |
| RAM | 8 GB |
| CPU | 4 Cores |
| Disk | 100 GB |

**Note**

Because this lab was completed on **Apple Silicon**, the Ubuntu VM was created using **UTM Emulation Mode** instead of virtualization.

# Lab Architecture

```
Apple Silicon Mac
      │
      ▼
UTM Virtual Machine (Emulated)
      │
      ▼
Ubuntu 24.04 Desktop
      │
      ▼
Wazuh Manager + Indexer + Dashboard
      │
      ▼
Wazuh Web Interface
```

# Installation Steps

# 1. Download Ubuntu ISO

Download the Ubuntu Desktop ISO.

Example file used in this lab:

```
ubuntu-24.04.4-desktop-amd64.iso
```

📸 **Screenshot to add**

```
screenshots/ubuntu_download_page.png
```

Add screenshot in GitHub:

```
![Ubuntu Download](screenshots/ubuntu_download_page.png)
```

# 2. Create Virtual Machine in UTM

Open **UTM** and select:

```
Create New Virtual Machine
```

Select:

```
Emulate
```

Then choose:

```
Linux
```

Attach the Ubuntu ISO file.

VM configuration used for this lab:

```
RAM: 8192 MB
CPU: 4 cores
Disk: 100 GB
Architecture: x86_64
```

📸 **Screenshots to add**

```
screenshots/utm_create_vm.png
screenshots/utm_emulate_mode.png
screenshots/utm_vm_settings.png
```

Insert them in GitHub:

```
![UTM Create VM](screenshots/utm_create_vm.png)

![UTM Emulation Mode](screenshots/utm_emulate_mode.png)

![UTM VM Settings](screenshots/utm_vm_settings.png)
```

# 3. Boot Ubuntu Installer

Start the virtual machine.

When the Ubuntu boot menu appears select:

```
Try or Install Ubuntu
```

📸 **Screenshot to add**

```
screenshots/ubuntu_boot_menu.png
```

Insert:

```
![Ubuntu Boot Menu](screenshots/ubuntu_boot_menu.png)
```

# 4. Configure Ubuntu Installation

Follow the Ubuntu installation wizard.

Recommended selections:

Language

```
English
```

Keyboard

```
English (US)
```

Network

```
Use Wired Connection
```

Installation type

```
Install Ubuntu
```

Installation mode

```
Interactive Installation
```

Application selection

```
Default Selection
```

Disk setup

```
Erase Disk and Install Ubuntu
```

📸 **Screenshots to add**

```
screenshots/language_selection.png
screenshots/keyboard_layout.png
screenshots/network_connection.png
screenshots/disk_setup.png
```

Insert:

```
![Language Selection](screenshots/language_selection.png)

![Keyboard Layout](screenshots/keyboard_layout.png)

![Network Connection](screenshots/network_connection.png)

![Disk Setup](screenshots/disk_setup.png)
```

# 5. Create Ubuntu User

Create a user account.

Example configuration used in the lab:

```
Username: shadowbox
Computer Name: wazuh-server
Password: ********
```

Select the correct timezone.

Example:

```
America / Los Angeles
```

📸 **Screenshots to add**

```
screenshots/create_user.png
screenshots/timezone_selection.png
```

Insert:

```
![Create User](screenshots/create_user.png)

![Timezone Selection](screenshots/timezone_selection.png)
```

# 6. Complete Ubuntu Installation

Ubuntu will begin copying files and installing the system.

When installation finishes:

Select

```
Restart Now
```

Remove the installation medium when prompted.

Press **Enter** to reboot.

📸 **Screenshots to add**

```
screenshots/install_progress.png
screenshots/remove_install_media.png
```

Insert:

```
![Installation Progress](screenshots/install_progress.png)

![Remove Install Media](screenshots/remove_install_media.png)
```

# 7. Log Into Ubuntu

After the system reboots, log into Ubuntu using the user account created earlier.

📸 **Screenshots to add**

```
screenshots/ubuntu_login.png
screenshots/ubuntu_desktop.png
```

Insert:

```
![Ubuntu Login](screenshots/ubuntu_login.png)

![Ubuntu Desktop](screenshots/ubuntu_desktop.png)
```

# 8. Update System

Open a terminal and update the system.

```bash
sudo apt update && sudo apt upgrade -y
```

📸 **Screenshot**

```
screenshots/system_update.png
```

Insert:

```
![System Update](screenshots/system_update.png)
```

# 9. Install Curl

Curl is required to download the Wazuh installer.

```bash
sudo apt install curl -y
```

📸 **Screenshot**

```
screenshots/install_curl.png
```

Insert:

```
![Install Curl](screenshots/install_curl.png)
```

# 10. Download Wazuh Installer

Download the official Wazuh installation script.

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

📸 **Screenshot**

```
screenshots/download_wazuh_script.png
```

Insert:

```
![Download Wazuh Script](screenshots/download_wazuh_script.png)
```

# 11. Make Installer Executable

```bash
chmod +x wazuh-install.sh
```

📸 **Screenshot**

```
screenshots/chmod_script.png
```

Insert:

```
![Make Script Executable](screenshots/chmod_script.png)
```

# 12. Run Wazuh Installer

Run the Wazuh all-in-one installer.

```bash
sudo ./wazuh-install.sh -a
```

This installs:

- Wazuh Manager
- Wazuh Indexer
- Filebeat
- Wazuh Dashboard

📸 **Screenshot**

```
screenshots/wazuh_install_running.png
```

Insert:

```
![Wazuh Installation](screenshots/wazuh_install_running.png)
```

# 13. Handle Ubuntu Compatibility Warning

If Ubuntu 24.04 triggers a compatibility warning, run the installer again using:

```bash
sudo ./wazuh-install.sh -a -i
```

This bypasses the OS compatibility check.

📸 **Screenshot**

```
screenshots/wazuh_compatibility_warning.png
```

Insert:

```
![Compatibility Warning](screenshots/wazuh_compatibility_warning.png)
```

# 14. Save Dashboard Credentials

At the end of installation the terminal displays dashboard credentials.

Example output:

```
User: admin
Password: <generated password>
```

Save the password.

📸 **Screenshot**

```
screenshots/wazuh_credentials.png
```

Insert:

```
![Wazuh Credentials](screenshots/wazuh_credentials.png)
```

# 15. Find Server IP Address

Run:

```bash
ip a
```

Locate the active network interface.

Example:

```
192.168.64.15
```

📸 **Screenshot**

```
screenshots/ip_address_command.png
```

Insert:

```
![IP Address](screenshots/ip_address_command.png)
```

# 16. Access Wazuh Dashboard

Open a browser and navigate to:

```
https://<server-ip>
```

Example:

```
https://192.168.64.15
```

If the browser warns about a certificate:

```
Advanced → Proceed
```

📸 **Screenshot**

```
screenshots/wazuh_login_page.png
```

Insert:

```
![Wazuh Login](screenshots/wazuh_login_page.png)
```

# 17. Log Into Wazuh

Enter the credentials generated during installation.

```
Username: admin
Password: <generated password>
```

The Wazuh dashboard will load.

📸 **Screenshot**

```
screenshots/wazuh_dashboard.png
```

Insert:

```
![Wazuh Dashboard](screenshots/wazuh_dashboard.png)
```

# Verification

Successful installation displays the Wazuh dashboard modules:

- Security Events
- Integrity Monitoring
- Policy Monitoring
- System Auditing
- Security Configuration Assessment

Initially the dashboard will show:

```
Total Agents: 0
```

This is expected until agents are added.

# Result

The Wazuh SIEM platform has been successfully deployed and is ready to monitor endpoints within the SOC lab environment.

Future steps include:

- Installing Wazuh agents
- Connecting endpoints
- Generating security alerts
- Monitoring logs and security events
