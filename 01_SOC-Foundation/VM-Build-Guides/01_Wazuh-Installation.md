# Wazuh Installation Guide (Phase 1)

## Objective

Deploy **Wazuh SIEM** on an Ubuntu 24.04 virtual machine to function as the centralized security monitoring platform for the Phase 1 SOC lab environment.

Wazuh is an open-source security platform used for threat detection, log analysis, intrusion detection, vulnerability monitoring, and compliance auditing.

Wazuh provides:

- Security Information and Event Management (SIEM)
- Intrusion detection
- File integrity monitoring
- Log analysis
- Security configuration assessment

## Lab Environment

| Component               | Configuration                       |
|-------------------------|-------------------------------------|
| Host System             | Apple Silicon Mac                   |
| Virtualization Platform | UTM                                 |
| VM Mode                 | Emulation                           |
| Guest OS                | Ubuntu 24.04 Desktop                |
| SIEM Platform           | Wazuh 4.7 (see Step 11 for latest)  |
| RAM                     | 8 GB                                |
| CPU                     | 4 Cores                             |
| Disk                    | 100 GB                              |

> **Note:** Because this lab was completed on **Apple Silicon**, the Ubuntu virtual machine was created using **UTM Emulation Mode** instead of virtualization.

## Lab Architecture

```text
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

## Installation Steps

### 1. Download Ubuntu ISO

Download the Ubuntu Desktop ISO.

Example file used in this lab:

```text
ubuntu-24.04.4-desktop-amd64.iso
```

![Ubuntu Download](installation-screenshots/wazuh/01_ubuntu_download_page.png)

### 2. Create Virtual Machine in UTM

Open **UTM** and create a new virtual machine.

Select:

```text
Emulate
```

Then choose:

```text
Linux
```

Attach the Ubuntu ISO file.

VM configuration used for this lab:

```text
RAM: 8192 MB
CPU: 4 cores
Disk: 100 GB
Architecture: x86_64
```

![UTM Create VM](installation-screenshots/wazuh/02_utm_create_vm.png)

![UTM Emulation Mode](installation-screenshots/wazuh/03_utm_emulation_mode.png)

![UTM Select Linux OS](installation-screenshots/wazuh/04_utm_select_linux_os.png)

![UTM Hardware Configuration](installation-screenshots/wazuh/05_utm_hardware_configuration.png)

![UTM Boot ISO Selection](installation-screenshots/wazuh/06_utm_boot_iso_selection.png)

![UTM Storage Configuration](installation-screenshots/wazuh/07_utm_storage_configuration.png)

![UTM Shared Directory Setup](installation-screenshots/wazuh/08_utm_shared_directory_setup.png)

![UTM VM Summary](installation-screenshots/wazuh/09_utm_vm_summary.png)

### 3. Boot Ubuntu Installer

Start the virtual machine.

When the Ubuntu boot menu appears, select:

```text
Try or Install Ubuntu
```

![Ubuntu Boot Screen](installation-screenshots/wazuh/10_ubuntu_boot_screen.png)

![Ubuntu GRUB Boot Menu](installation-screenshots/wazuh/11_ubuntu_grub_boot_menu.png)

### 4. Configure Ubuntu Installation

Follow the Ubuntu installation wizard.

Recommended selections:

Language:

```text
English
```

Keyboard:

```text
English (US)
```

Network:

```text
Use Wired Connection
```

Installation type:

```text
Install Ubuntu
```

Installation mode:

```text
Interactive Installation
```

Application selection:

```text
Default Selection
```

Disk setup:

```text
Erase Disk and Install Ubuntu
```

![Ubuntu Language Selection](installation-screenshots/wazuh/12_ubuntu_language_selection.png)

![Ubuntu Accessibility Settings](installation-screenshots/wazuh/13_ubuntu_accessibility_settings.png)

![Ubuntu Keyboard Layout Selection](installation-screenshots/wazuh/14_ubuntu_keyboard_layout_selection.png)

![Ubuntu Network Connection Setup](installation-screenshots/wazuh/15_ubuntu_network_connection_setup.png)

![Ubuntu Install Option](installation-screenshots/wazuh/16_ubuntu_install_ubuntu_option.png)

![Ubuntu Interactive Installation Selection](installation-screenshots/wazuh/17_ubuntu_interactive_installation_selection.png)

![Ubuntu Default Application Selection](installation-screenshots/wazuh/18_ubuntu_default_application_selection.png)

![Ubuntu Proprietary Software Options](installation-screenshots/wazuh/19_ubuntu_proprietary_software_options.png)

![Ubuntu Disk Setup Erase Disk](installation-screenshots/wazuh/20_ubuntu_disk_setup_erase_disk.png)

### 5. Create Ubuntu User

Create a user account.

Example configuration used in the lab:

```text
Username: shadowbox
Computer Name: wazuh-server
Password: ********
```

Select the correct time zone.

Example:

```text
America / Los Angeles
```

![Ubuntu Create User Account](installation-screenshots/wazuh/21_ubuntu_create_user_account.png)

![Ubuntu Timezone Selection](installation-screenshots/wazuh/22_ubuntu_timezone_selection.png)

### 6. Review Installation Settings and Complete Ubuntu Installation

Review the installation summary before proceeding.

Ubuntu will then begin copying files and installing the operating system.

When installation finishes:

- Select **Restart Now**
- Remove the installation medium when prompted
- Press **Enter** to reboot

![Ubuntu Review Installation Settings](installation-screenshots/wazuh/23_ubuntu_review_installation_settings.png)

![Ubuntu Installation Progress](installation-screenshots/wazuh/24_ubuntu_installation_progress.png)

![Ubuntu Installation Complete Restart](installation-screenshots/wazuh/25_ubuntu_installation_complete_restart.png)

![Ubuntu Remove Installation Medium](installation-screenshots/wazuh/26_ubuntu_remove_installation_medium.png)

![Ubuntu Login Screen](installation-screenshots/wazuh/27_ubuntu_login_screen.png)

### 7. Log Into Ubuntu

After the system reboots, log into Ubuntu using the user account created earlier.

Once logged in, complete the first-boot welcome screen.

![Ubuntu Desktop Welcome](installation-screenshots/wazuh/28_ubuntu_first_boot_welcome.png)

### 8. Configure a Static IP Address

Before installing Wazuh, assign a static IP address to the VM. A DHCP-assigned address can change on reboot, which would break access to the Wazuh dashboard.

Open **Settings → Network**, select the active wired connection, and assign a static IPv4 address.

Example configuration:

```text
Address:  192.168.64.15
Netmask:  255.255.255.0
Gateway:  192.168.64.1
DNS:      8.8.8.8
```

> **Note:** Use an address outside your router's DHCP range to avoid conflicts. The correct gateway and subnet will depend on your UTM network configuration.

After saving, restart the network manager to apply the change immediately:

```bash
sudo systemctl restart NetworkManager
```

Verify the new address is active before proceeding:

```bash
ip a
```

### 9. Update the System

Open a terminal and update the system.

```bash
sudo apt update && sudo apt upgrade -y
```

This updates package repositories and installs the latest system updates.

![Ubuntu Terminal Open Update System](installation-screenshots/wazuh/29_ubuntu_terminal_open_update_system.png)

![Ubuntu System Update Command](installation-screenshots/wazuh/30_ubuntu_system_update_command.png)

### 10. Verify curl Is Installed

`curl` is required to download the Wazuh installer. Ubuntu 24.04 Desktop typically includes it by default. Verify it is available, and install it if not.

```bash
curl --version || sudo apt install curl -y
```

![Install Curl Dependency](installation-screenshots/wazuh/31_install_curl_dependency.png)

### 11. Download the Wazuh Installer

Download the official Wazuh installation script.

> **Note:** The URL below references Wazuh **4.7**, which was the version used in this lab. Check the [official Wazuh documentation](https://documentation.wazuh.com/current/installation-guide/index.html) for the latest version and update the URL accordingly before running the command.

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

![Download Wazuh Install Script](installation-screenshots/wazuh/32_download_wazuh_install_script.png)

### 12. Make the Installer Executable and Run It

Give the script execution permissions, then run the Wazuh all-in-one installer.

```bash
chmod +x wazuh-install.sh
sudo ./wazuh-install.sh -a
```

This installs:

- Wazuh Manager
- Wazuh Indexer
- Filebeat
- Wazuh Dashboard

If Ubuntu 24.04 triggers a compatibility warning, rerun the installer using:

```bash
sudo ./wazuh-install.sh -a -i
```

This bypasses the operating system compatibility check.

![Run Wazuh Install Script](installation-screenshots/wazuh/34_run_wazuh_install_script.png)

![Wazuh Installation Start](installation-screenshots/wazuh/35_wazuh_installation_start.png)

### 13. Save Dashboard Credentials

At the end of installation, the terminal displays dashboard credentials.

Example output:

```text
User: admin
Password: <generated password>
```

Save the password — it is required to access the Wazuh dashboard and cannot be recovered after closing the terminal.

![Wazuh Installation Complete Credentials](installation-screenshots/wazuh/36_wazuh_installation_complete_credentials.png)

### 14. Confirm Firewall Status

Ubuntu 24.04 Desktop ships with `ufw` inactive by default. If `ufw` has been enabled, ensure the following ports are open so the dashboard and agents can communicate:

```bash
sudo ufw allow 443/tcp    # Wazuh Dashboard (HTTPS)
sudo ufw allow 1514/tcp   # Wazuh agent communication
sudo ufw allow 1515/tcp   # Wazuh agent enrollment
sudo ufw reload
```

To check the current firewall status:

```bash
sudo ufw status
```

### 15. Find the Server IP Address

Run:

```bash
ip a
```

Locate the active network interface and confirm the static IPv4 address assigned in Step 8 is active.

Example:

```text
192.168.64.15
```

![Check System IP Address](installation-screenshots/wazuh/37_check_system_ip_address.png)

### 16. Access the Wazuh Dashboard

Open a browser and navigate to:

```text
https://<server-ip>
```

Example:

```text
https://192.168.64.15
```

Because Wazuh uses a self-signed certificate, the browser may display a security warning.

Select:

```text
Advanced → Proceed
```

![Access Wazuh Dashboard URL](installation-screenshots/wazuh/38_access_wazuh_dashboard_url.png)

### 17. Log Into Wazuh

Enter the credentials generated during installation.

```text
Username: admin
Password: <generated password>
```

![Wazuh Login Page](installation-screenshots/wazuh/39_wazuh_login_page.png)

### 18. Verify Dashboard Access

After successful authentication, the Wazuh dashboard loads and displays the monitoring interface.

The dashboard will show:

```text
Total Agents: 0
```

This is expected — no endpoints have been connected yet. Agents will be added in a later phase.

![Wazuh Dashboard Overview](installation-screenshots/wazuh/40_wazuh_dashboard_overview.png)

## Result

The Wazuh SIEM platform has been successfully deployed with the following components installed and running:

| Component       | Role                                           |
|-----------------|------------------------------------------------|
| Wazuh Manager   | Processes and analyzes security events         |
| Wazuh Indexer   | Stores security logs and indexed events        |
| Filebeat        | Forwards logs to the indexer                   |
| Wazuh Dashboard | Web interface for monitoring and analysis      |

The dashboard modules available include Security Events, Integrity Monitoring, Policy Monitoring, System Auditing, and Security Configuration Assessment.

Future steps include:

- Installing Wazuh agents
- Connecting endpoints to the manager
- Generating security alerts
- Monitoring logs and security events
