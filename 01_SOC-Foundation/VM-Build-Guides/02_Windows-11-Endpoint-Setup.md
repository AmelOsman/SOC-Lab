# 💻 Windows 11 Endpoint — Installation Guide

> **Lab:** SOC Home Lab — Phase 1  
> **Role:** Monitored Enterprise Workstation  
> **Path:** `SOC-Lab / 01_SOC-Foundation / VM-Build-Guides`

---

## VM Specifications

| Setting | Value |
|---|---|
| CPU Cores | 2–4 cores |
| RAM | 8 GB recommended |
| Disk | 60–100 GB |
| Network Adapter | Internal — Lab Network |
| Engine | QEMU / UTM Emulate (x86_64) |
| OS | Windows 11 Pro |

---

## Step 1 — Download the Windows 11 ISO

1. Navigate to the Microsoft download page:
   - **Apple Silicon:** https://www.microsoft.com/en-us/software-download/windows11arm64
   - **Intel Mac:** https://www.microsoft.com/en-us/software-download/windows11

2. From the **Select Download** dropdown choose **Windows 11 (multi-edition ISO for Arm64)** for Apple Silicon, or the standard x64 ISO for Intel Macs.

![Microsoft ISO download selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/01_microsoft_iso_download_selection.png)

3. Select language **English (United States)** and click **Confirm**.

![Language selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/02_microsoft_language_selection.png)

4. Click **Download Now** (or **64-bit Download** for x64).

![Download button](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/03_microsoft_download_button.png)

> ⚠️ Download links are valid for **24 hours** only. If expired, return to the download page and repeat the selection.

5. Monitor the download progress in your browser. The file will be named `Win11_25H2_English_x64.iso` (~7.2 GB).

![ISO downloading](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/04_browser_iso_downloading.png)

---

## Step 2 — Create the VM in UTM

### 2.1 Choose Virtualisation Mode

1. Launch **UTM** and click **+** (or **File > New**).
2. In the **Start** dialog choose your mode:

| Mode | When to use |
|---|---|
| **Virtualize** | Apple Silicon + Arm64 ISO, or any Intel Mac |
| **Emulate** | Apple Silicon + x64 ISO |

![UTM Start dialog](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/05_utm_start_virtualize_emulate.png)

### 2.2 Select Operating System

Select **Windows** from the Operating System screen.

![UTM OS selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/06_utm_os_selection_windows.png)

### 2.3 Configure Boot ISO and Drivers

1. Ensure **Install Windows 10 or higher** is checked.
2. Click **Browse** and select the ISO you downloaded.
3. Leave **Install drivers and SPICE tools** checked.

![UTM Windows ISO and SPICE tools](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/07_utm_windows_iso_spice_tools.png)

Click **Continue**.

### 2.4 Configure Hardware

| Setting | Value |
|---|---|
| Machine | Intel ICH9 based PC (2009, x86_64) |
| Memory | 4096–8192 MiB |
| CPU Cores | 4 |

![UTM Hardware screen](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/08_utm_hardware_ich9_4gb_4cores.png)

Click **Continue**.

> ⚠️ 4 GB RAM meets the minimum but Windows 11 may be sluggish. Increase to 8 GB if your Mac has sufficient memory available.

### 2.5 Storage

Set the drive size to **64 GiB** and click **Continue**.

![UTM Storage](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/09_utm_storage_64gb.png)

### 2.6 Shared Directory

Leave the path empty and click **Continue**.

![UTM Shared Directory](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/10_utm_shared_directory.png)

### 2.7 Summary

Confirm the configuration, name the VM **Windows 11**, and click **Save**.

| Field | Value |
|---|---|
| Engine | QEMU |
| Architecture | x86_64 |
| RAM | 4 GB |
| CPU | 4 Cores |
| Storage | 64 GB |

![UTM Summary](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/11_utm_summary_windows11.png)

### 2.8 Start the VM

Select the **Windows 11** VM in the UTM sidebar and click **Play (▶)**.

![UTM play button](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/12_utm_main_window_play_button.png)

---

## Step 3 — Windows Setup Wizard

### 3.1 Language and Keyboard

Set Language and Time/currency to **English (United States)**. Click **Next**.

![Language settings](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/13_win_setup_language_settings.png)

Confirm **US** keyboard layout. Click **Next**.

![Keyboard settings](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/14_win_setup_keyboard_settings.png)

### 3.2 Product Key

Click **"I don't have a product key"** to skip activation.

![Product key](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/15_win_setup_product_key.png)

> ℹ️ Windows can be activated later via **Settings > System > Activation**.

### 3.3 Select Edition

The full edition list will appear.

![Edition list](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/16_win_setup_select_image_editions_list.png)

Select **Windows 11 Pro** and click **Next**.

![Windows 11 Pro selected](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/17_win_setup_select_image_pro_selected.png)

### 3.4 Licence Terms

Windows will briefly load before showing the licence agreement.

![Getting ready](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/18_win_setup_getting_ready.png)

Click **Accept**.

![Licence terms](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/19_win_setup_licence_terms.png)

### 3.5 Select Installation Drive

Select **Disk 0 Unallocated Space (64.0 GB)** and click **Next**.

![Disk selection](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/20_win_setup_disk_selection_64gb.png)

### 3.6 Installation in Progress

Windows will copy and expand files. The VM will restart **2–3 times** automatically.

![Installing](https://raw.githubusercontent.com/AmelOsman/SOC-Lab/main/01_SOC-Foundation/VM-Build-Guides/installation-screenshots/windows11-endpoint/21_win_setup_installing_6_percent.png)

> ⏱️ Allow **15–30 minutes**. Do not interact with the VM during automatic restarts.

---

*Installation continues in the next section — OOBE setup, static IP, domain join, and Sysmon deployment.*
