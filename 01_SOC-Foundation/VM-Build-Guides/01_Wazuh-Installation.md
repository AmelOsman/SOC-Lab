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

| Component | Configuration |
|-----------|--------------|
| Host System | Apple Silicon Mac |
| Virtualization Platform | UTM |
| VM Mode | Emulation |
| Guest OS | Ubuntu 24.04 Desktop |
| SIEM Platform | Wazuh 4.7 |
| RAM | 8 GB |
| CPU | 4 Cores |
| Disk | 100 GB |

**Note**

Because this lab was completed on **Apple Silicon**, the Ubuntu virtual machine was created using **UTM Emulation Mode** instead of virtualization.

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

![Ubuntu Download Page](screenshots/01_ubuntu_download_page.png)

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

![UTM Create VM](screenshots/02_utm_create_vm.png)

![UTM Emulation Mode](screenshots/03_utm_emulation_mode.png)

![UTM Select Linux OS](screenshots/04_utm_select_linux_os.png)

Configure the VM hardware settings:

```text
RAM: 8192 MB
CPU: 4 cores
Disk: 100 GB
Architecture: x86_64
```

![UTM Hardware Configuration](screenshots/05_utm_hardware_configuration.png)

Attach the Ubuntu ISO file.

![UTM Boot ISO Selection](screenshots/06_utm_boot_iso_selection.png)

Configure storage.

![UTM Storage Configuration](screenshots/07_utm_storage_configuration.png)

Configure shared directory settings if needed.

![UTM Shared Directory Setup](screenshots/08_utm_shared_directory_setup.png)

Review and confirm the VM summary before starting.

![UTM VM Summary](screenshots/09_utm_vm_summary.png)

### 3. Boot Ubuntu Installer

Start the virtual machine.

![Ubuntu Boot Screen](screenshots/10_ubuntu_boot_screen.png)

When the Ubuntu GRUB boot menu appears, select:

```text
Try or Install Ubuntu
```

![Ubuntu GRUB Boot Menu](screenshots/11_ubuntu_grub_boot_menu.png)

### 4. Configure Ubuntu Installation

Follow the Ubuntu installation wizard.

**Language:**

```text
English
```

![Language Selection](screenshots/12_ubuntu_language_selection.png)

**Accessibility:**

Configure accessibility settings as needed, or leave as default.

![Accessibility Settings](screenshots/13_ubuntu_accessibility_settings.png)

**Keyboard:**

```text
English (US)
```

![Keyboard Layout Selection](screenshots/14_ubuntu_keyboard_layout_selection.png)

**Network:**

```text
Use Wired Connection
```

![Network Connection Setup](screenshots/15_ubuntu_network_connection_setup.png)

**Installation Type:**

```text
Install Ubuntu
```

![Install Ubuntu Option](screenshots/16_ubuntu_install_ubuntu_option.png)

**Installation Mode:**

```text
Interactive Installation
```

![Interactive Installation Selection](screenshots/17_ubuntu_interactive_installation_selection.png)

**Application Selection:**

```text
Default Selection
```

![Default Application Selection](screenshots/18_ubuntu_default_application_selection.png)

**Proprietary Software:**

Choose whether to install proprietary drivers and media codecs.

![Proprietary Software Options](screenshots/19_ubuntu_proprietary_software_options.png)

**Disk Setup:**

```text
Erase Disk and Install Ubuntu
```

![Disk Setup – Erase Disk](screenshots/20_ubuntu_disk_setup_erase_disk.png)

### 5. Create Ubuntu User

Create a user account.

Example configuration used in the lab:

```text
Username: shadowbox
Computer Name: wazuh-server
Password: ********
```

![Create User Account](screenshots/21_ubuntu_create_user_account.png)

Select the correct time zone.

Example:

```text
America / Los Angeles
```

![Timezone Selection](screenshots/22_ubuntu_timezone_selection.png)

Review the installation settings before proceeding.

![Review Installation Settings](screenshots/23_ubuntu_review_installation_settings.png)

### 6. Complete Ubuntu Installation

Ubuntu will begin copying files and installing the operating system.

![Ubuntu Installation Progress](screenshots/24_ubuntu_installation_progress.png)

When installation finishes:

- Select **Restart Now**
- Remove the installation medium when prompted
- Press **Enter** to reboot

![Installation Complete – Restart](screenshots/25_ubuntu_installation_complete_restart.png)

![Remove Installation Media](screenshots/26_ubuntu_remove_installation_media.png)

### 7. Log Into Ubuntu

After the system reboots, log into Ubuntu using the user account created earlier.

![Ubuntu Login Screen](screenshots/27_ubuntu_login_screen.png)

![Ubuntu First Boot Welcome](screenshots/28_ubuntu_first_boot_welcome.png)

### 8. Update the System

Open a terminal and update the system.

```bash
sudo apt update && sudo apt upgrade -y
```

This updates package repositories and installs the latest system updates.

![Open Terminal – Update System](screenshots/29_ubuntu_terminal_open_update_system.png)

![System Update Command](screenshots/30_ubuntu_system_update_command.png)

### 9. Install Curl

Curl is required to download the Wazuh installer.

```bash
sudo apt install curl -y
```

![Install Curl Dependency](screenshots/31_install_curl_dependency.png)

### 10. Download the Wazuh Installer

Download the official Wazuh installation script.

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
```

![Download Wazuh Install Script](screenshots/32_download_wazuh_install_script.png)

### 11. Make the Installer Executable

Give the script execution permissions.

```bash
chmod +x wazuh-install.sh
```

![Make Wazuh Script Executable](screenshots/33_make_wazuh_script_executable.png)

### 12. Run the Wazuh Installer

Run the Wazuh all-in-one installer.

```bash
sudo ./wazuh-install.sh -a
```

This installs:

- Wazuh Manager
- Wazuh Indexer
- Filebeat
- Wazuh Dashboard

![Run Wazuh Install Script](screenshots/34_run_wazuh_install_script.png)

![Wazuh Installation Start](screenshots/35_wazuh_installation_start.png)

### 13. Handle Ubuntu Compatibility Warning

If Ubuntu 24.04 triggers a compatibility warning, run the installer again using:

```bash
sudo ./wazuh-install.sh -a -i
```

This bypasses the operating system compatibility check.

### 14. Save Dashboard Credentials

At the end of installation, the terminal displays dashboard credentials.

Example output:

```text
User: admin
Password: <generated password>
```

Save the password because it is required to access the Wazuh dashboard.

![Wazuh Installation Complete – Credentials](screenshots/36_wazuh_installation_complete_credentials.png)

### 15. Find the Server IP Address

Run:

```bash
ip a
```

Locate the active network interface and identify the assigned IPv4 address.

Example:

```text
192.168.64.15
```

![Check System IP Address](screenshots/37_check_system_ip_address.png)

### 16. Access the Wazuh Dashboard

Open a browser and navigate to:

```text
https://<server-ip>
```

Example:

```text
https://192.168.64.15
```

Because Wazuh uses a self-signed certificate, the browser may display a warning.

Select:

```text
Advanced → Proceed
```

![Access Wazuh Dashboard URL](screenshots/38_access_wazuh_dashboard_url.png)

### 17. Log Into Wazuh

Enter the credentials generated during installation.

```text
Username: admin
Password: <generated password>
```

![Wazuh Login Page](screenshots/39_wazuh_login_page.png)

The Wazuh dashboard will load after successful authentication.

![Wazuh Dashboard Overview](screenshots/40_wazuh_dashboard_overview.png)

## Wazuh Components Installed

The Wazuh installation script deploys the following components:

- **Wazuh Manager** – Processes and analyzes security events
- **Wazuh Indexer** – Stores security logs and indexed events
- **Filebeat** – Forwards logs to the indexer
- **Wazuh Dashboard** – Provides the web interface for monitoring and analysis

## Verification

A successful installation displays the Wazuh dashboard modules, including:

- Security Events
- Integrity Monitoring
- Policy Monitoring
- System Auditing
- Security Configuration Assessment

Initially the dashboard will show:

```text
Total Agents: 0
```

This is expected until monitored endpoints are added to the Wazuh manager.

## Result

The Wazuh SIEM platform has been successfully deployed and is ready to monitor endpoints within the SOC lab environment.

Future steps include:

- Installing Wazuh agents
- Connecting endpoints to the manager
- Generating security alerts
- Monitoring logs and security events
