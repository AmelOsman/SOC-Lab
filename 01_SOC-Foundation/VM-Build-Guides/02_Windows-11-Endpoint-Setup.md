# Windows 11 Endpoint — Installation Guide

**Lab:** SOC Home Lab — Phase 1  
**Role:** Monitored Enterprise Workstation  
**Path:** `SOC-Lab / 01_SOC-Foundation / VM-Build-Guides`

---

## Table of Contents

- [VM Specifications](#vm-specifications)
- [Step 1 — Download the Windows 11 ISO](#step-1--download-the-windows-11-iso)
- [Step 2 — Create the VM in UTM](#step-2--create-the-vm-in-utm)
- [Step 3 — Windows Setup Wizard](#step-3--windows-setup-wizard)

---

## VM Specifications

| Setting | Value |
|---|---|
| CPU Cores | 2–4 |
| RAM | 8 GB recommended |
| Disk | 60–100 GB |
| Network Adapter | Internal — Lab Network |
| Engine | QEMU / UTM Emulate (x86_64) |
| OS | Windows 11 Pro |

---

## Step 1 — Download the Windows 11 ISO

### 1.1 Select the ISO

Go to the Microsoft download page for your Mac type:

- **Apple Silicon (M1/M2/M3/M4):** https://www.microsoft.com/en-us/software-download/windows11arm64
- **Intel Mac:** https://www.microsoft.com/en-us/software-download/windows11

From the **Select Download** dropdown, choose **Windows 11 (multi-edition ISO for Arm64)** for Apple Silicon, or the standard x64 ISO for Intel Macs. Click **Download Now**.

![Microsoft ISO download selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/01_microsoft_iso_download_selection.png)

### 1.2 Select Language

Select **English (United States)** from the language dropdown and click **Confirm**.

![Language selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/02_microsoft_language_selection.png)

### 1.3 Start the Download

Click **Download Now** (or **64-bit Download** for x64) to begin downloading the ISO.

![Download button](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/03_microsoft_download_button.png)

> **Note:** Download links expire after **24 hours**. If your link has expired, return to the download page and repeat the selection steps.

### 1.4 Wait for the Download to Complete

Monitor the progress in your browser downloads panel. The file will be named `Win11_25H2_English_x64.iso` and is approximately **7.2 GB**.

![ISO downloading](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/04_browser_iso_downloading.png)

---

## Step 2 — Create the VM in UTM

### 2.1 Choose a Virtualisation Mode

Open UTM and click **+** in the top-left corner (or go to **File > New**). In the **Start** dialog, select the appropriate mode for your setup:

| Mode | When to Use |
|---|---|
| **Virtualize** | Apple Silicon with Arm64 ISO, or any Intel Mac — faster performance |
| **Emulate** | Apple Silicon with x64 ISO — slower, but compatible with other CPU architectures |

![UTM Start dialog](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/05_utm_start_virtualize_emulate.png)

### 2.2 Select the Operating System

On the Operating System screen, select **Windows**.

![UTM OS selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/06_utm_os_selection_windows.png)

### 2.3 Configure the Boot ISO and Drivers

On the Windows configuration screen:

1. Ensure **Install Windows 10 or higher** is checked.
2. Click **Browse** next to Boot ISO Image and select the ISO file you downloaded.
3. Leave **Install drivers and SPICE tools** checked. This enables clipboard sharing and dynamic display resolution between macOS and the VM.

![UTM Windows ISO and SPICE tools](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/07_utm_windows_iso_spice_tools.png)

Click **Continue**.

### 2.4 Configure Hardware

On the Hardware screen, configure the following settings:

| Setting | Value |
|---|---|
| Machine | Intel ICH9 based PC (2009, x86_64) |
| Memory | 4096–8192 MiB |
| CPU Cores | 4 |

![UTM Hardware screen](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/08_utm_hardware_ich9_4gb_4cores.png)

Click **Continue**.

> **Note:** 4 GB of RAM meets the minimum requirement, but Windows 11 may run slowly. Increase to 8 GB if your Mac has sufficient memory to spare.

### 2.5 Configure Storage

Set the drive size to **64 GiB** and click **Continue**.

![UTM Storage](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/09_utm_storage_64gb.png)

### 2.6 Shared Directory

No shared directory is needed for this lab. Leave the path empty and click **Continue**.

![UTM Shared Directory](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/10_utm_shared_directory.png)

### 2.7 Review the Summary

Review the configuration summary. Name the VM **Windows 11** and click **Save**.

| Field | Value |
|---|---|
| Engine | QEMU |
| Architecture | x86_64 |
| RAM | 4 GB |
| CPU | 4 Cores |
| Storage | 64 GB |

![UTM Summary](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/11_utm_summary_windows11.png)

### 2.8 Start the VM

Select the **Windows 11** VM in the UTM sidebar and click **Play (▶)** to boot from the ISO.

![UTM play button](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/12_utm_main_window_play_button.png)

---

## Step 3 — Windows Setup Wizard

### 3.1 Language and Keyboard Settings

On the **Select language settings** screen, set both the install language and the time/currency format to **English (United States)**. Click **Next**.

![Language settings](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/13_win_setup_language_settings.png)

On the **Select keyboard settings** screen, confirm the **US** keyboard layout and click **Next**.

![Keyboard settings](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/14_win_setup_keyboard_settings.png)

### 3.2 Product Key

On the Product key screen, click **"I don't have a product key"** at the bottom of the screen to continue without activation.

![Product key](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/15_win_setup_product_key.png)

> **Note:** Windows can be activated later via **Settings > System > Activation**. The OS will function normally in an unactivated state for lab purposes.

### 3.3 Select the Windows Edition

The **Select Image** screen will display all available editions.

![Edition list](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/16_win_setup_select_image_editions_list.png)

Select **Windows 11 Pro** and click **Next**.

![Windows 11 Pro selected](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/17_win_setup_select_image_pro_selected.png)

### 3.4 Accept the Licence Terms

Windows will display a brief loading screen before presenting the licence agreement.

![Getting ready](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/18_win_setup_getting_ready.png)

Read the **Applicable notices and license terms** and click **Accept**.

![Licence terms](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/19_win_setup_licence_terms.png)

### 3.5 Select the Installation Drive

On the **Select location to install Windows 11** screen, select **Disk 0 Unallocated Space (64.0 GB)** and click **Next**. Windows will automatically create the required partitions.

![Disk selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/20_win_setup_disk_selection_64gb.png)

### 3.6 Installation in Progress

Windows will begin copying and expanding files. The VM will restart **2–3 times** automatically during this process.

![Installing](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/21_win_setup_installing_6_percent.png)

> **Note:** Allow **15–30 minutes** for the installation to complete. Do not click inside the VM or interrupt the process during automatic restarts.

---

*This guide continues in the next section — covering OOBE setup, static IP configuration, domain join, and Sysmon deployment.*
