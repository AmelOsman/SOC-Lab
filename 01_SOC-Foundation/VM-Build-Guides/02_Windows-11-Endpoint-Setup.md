# Windows 11 Endpoint — Installation Guide

**Lab:** SOC Home Lab — Phase 1  
**Role:** Monitored Enterprise Workstation  
**Path:** `SOC-Lab / 01_SOC-Foundation / VM-Build-Guides`

---

## Table of Contents

- [VM Specifications](#vm-specifications)
- [Step 1 — Download the Windows 11 ARM64 ISO](#step-1--download-the-windows-11-arm64-iso)
- [Step 2 — Create a New VM in UTM](#step-2--create-a-new-vm-in-utm)
- [Step 3 — Select the Operating System](#step-3--select-the-operating-system)
- [Step 4 — Configure the Windows Image](#step-4--configure-the-windows-image)
- [Step 5 — Set Hardware Resources](#step-5--set-hardware-resources)
- [Step 6 — Configure Storage](#step-6--configure-storage)
- [Step 7 — Shared Directory (Optional)](#step-7--shared-directory-optional)
- [Step 8 — Review the Summary](#step-8--review-the-summary)
- [Step 9 — Start the VM](#step-9--start-the-vm)
- [Step 10 — Windows Setup Wizard](#step-10--windows-setup-wizard)
- [Step 11 — Installation Progress](#step-11--installation-progress)
- [Step 12 — Eject the ISO & Complete OOBE Setup](#step-12--eject-the-iso--complete-oobe-setup)
- [Step 13 — Install UTM Guest Tools](#step-13--install-utm-guest-tools)
- [Tips & Troubleshooting](#tips--troubleshooting)

---

## VM Specifications

| Setting | Value |
|---|---|
| Architecture | ARM64 (aarch64) |
| Engine | QEMU |
| RAM | 4 GB minimum — 8 GB recommended |
| CPU Cores | 4 minimum |
| Storage | 64 GiB |
| Display | VGA |
| SPICE Tools | Installed |
| Operating System | Windows 11 Pro |

---

## Step 1 — Download the Windows 11 ARM64 ISO

Browse the UTM gallery at [mac.getutm.app/gallery](https://mac.getutm.app/gallery) and locate the Windows 11 entry.

![UTM Gallery](installation-screenshots/windows11-endpoint/01-utm-gallery-browse.png)

Click on the Windows 11 tile to view its details.

![Windows 11 UTM Gallery Detail](installation-screenshots/windows11-endpoint/02-utm-gallery-windows11-detail.png)

Click **Guide** to open the UTM documentation for Windows installation.

![UTM Docs — Obtain Windows](installation-screenshots/windows11-endpoint/03-utm-docs-obtain-windows.png)

Go to the Microsoft website and download the **Windows 11 Disk Image (ISO) for Arm-based PCs**.

![Microsoft Download Page](installation-screenshots/windows11-endpoint/04-microsoft-download-windows11-arm64.png)

Confirm `Win11_25H2_English_Arm64.iso` is in your Downloads folder.

![Downloads Folder](installation-screenshots/windows11-endpoint/05-downloads-windows11-iso.png)

---

## Step 2 — Create a New VM in UTM

Open UTM and click **+** to create a new virtual machine. Select **Virtualize** — this is faster and runs the native ARM64 architecture.

> ⚠️ Do not select **Emulate** — this is slower and used only for non-native architectures.

![UTM Start — Virtualize vs Emulate](installation-screenshots/windows11-endpoint/06-utm-start-virtualize-emulate.png)

---

## Step 3 — Select the Operating System

On the Operating System screen, select **Windows**.

![UTM Select Operating System](installation-screenshots/windows11-endpoint/07-utm-select-operating-system.png)

---

## Step 4 — Configure the Windows Image

- Check **Install Windows 10 or higher**
- Under Boot ISO Image, click **Browse...** and select `Win11_25H2_English_Arm64.iso`
- Ensure **Install drivers and SPICE tools** is checked
- Click **Continue**

![UTM Windows Image — ISO and SPICE](installation-screenshots/windows11-endpoint/09-utm-windows-image-iso-spice.png)

---

## Step 5 — Set Hardware Resources

| Setting | Recommended |
|---|---|
| Memory | 4096 MiB minimum — 8192 MiB recommended |
| CPU Cores | 4 minimum |

> 💡 Do not allocate more than half of your Mac's total RAM or CPU cores.

![UTM Hardware — Memory and CPU](installation-screenshots/windows11-endpoint/08-utm-hardware-memory-cpu.png)

Click **Continue**.

---

## Step 6 — Configure Storage

Set the virtual disk size to **64 GiB** (default). Click **Continue**.

> 💡 Windows 11 requires at least 20 GB. 64 GB or more is recommended for comfortable use.

![UTM Storage — 64 GiB](installation-screenshots/windows11-endpoint/10-utm-storage-64gb.png)

---

## Step 7 — Shared Directory (Optional)

Optionally link a folder on your Mac to make it accessible inside the Windows VM. Click **Browse...** to select one, or leave it blank and click **Continue** to skip.

![UTM Shared Directory](installation-screenshots/windows11-endpoint/11-utm-shared-directory.png)

---

## Step 8 — Review the Summary

Review all settings before saving. Rename the VM if desired, then click **Save**.

| Setting | Value |
|---|---|
| Name | Windows 11 |
| Engine | QEMU |
| Architecture | ARM64 (aarch64) |
| System | QEMU 10.0 ARM Virtual Machine |
| RAM | 4 GB |
| CPU | 4 Cores |
| Storage | 64 GiB |
| Operating System | Windows |

![UTM Summary](installation-screenshots/windows11-endpoint/12-utm-summary-review.png)

---

## Step 9 — Start the VM

Select the Windows 11 VM in the UTM sidebar and click the **Play (▶)** button.

> 💡 The screen may stay black for 30–60 seconds while the virtual hardware initializes — this is normal.

![UTM VM Ready — Play Button](installation-screenshots/windows11-endpoint/13-utm-vm-ready-play.png)

---

## Step 10 — Windows Setup Wizard

### Language & Keyboard

Select your **Language to install** and **Time and currency format**, then click **Next**.

![Windows Setup — Language](installation-screenshots/windows11-endpoint/14-windows-setup-language.png)

Confirm your **Keyboard or input method** (e.g. US), then click **Next**.

![Windows Setup — Keyboard](installation-screenshots/windows11-endpoint/15-windows-setup-keyboard.png)

### Product Key

Enter your 25-character Windows product key, or click **I don't have a product key** to skip and activate later.

![Windows Setup — Product Key](installation-screenshots/windows11-endpoint/16-windows-setup-product-key.png)

### Select Windows Edition

Select **Windows 11 Pro** — recommended for virtualization.

![Windows Setup — Select Edition](installation-screenshots/windows11-endpoint/17-windows-setup-select-edition.png)

### License Terms

Read the license terms and click **Accept**.

![Windows Setup — License Terms](installation-screenshots/windows11-endpoint/18-windows-setup-license-terms.png)

### Select Installation Location

Select **Disk 0 Unallocated Space** (64.0 GB) and click **Next**.

> ⚠️ Do not manually create or format partitions. Let Windows handle partition creation automatically.

![Windows Setup — Select Disk](installation-screenshots/windows11-endpoint/19-windows-setup-select-disk.png)

---

## Step 11 — Installation Progress

Windows will begin copying and installing files to the virtual disk.

![Windows Installing — 45%](installation-screenshots/windows11-endpoint/20-windows-installing-45-percent.png)

After the first restart, a black screen will appear showing **Installing 0% — Please keep your computer on.**

> ⚠️ Do NOT close UTM or shut down your Mac during installation. The process takes 10–20 minutes. Windows will restart 2–3 times automatically.

![Windows Restart — Installing 0%](installation-screenshots/windows11-endpoint/21-windows-restart-installing-0-percent.png)

---

## Step 12 — Eject the ISO & Complete OOBE Setup

### Eject the Windows ISO

Once installation finishes and the VM restarts, eject the Windows ISO from the UTM toolbar.

1. Click the **CD/DVD** drive icon in the UTM toolbar
2. Click **Eject** next to `Win11_25H2_English_Arm64.iso`

> 💡 Leave the UTM Guest Tools ISO mounted — you will need it in Step 13.

![UTM — Eject ISO](installation-screenshots/windows11-endpoint/22-utm-eject-iso.png)

### Out-of-Box Experience (OOBE)

Windows will boot to the Windows logo screen before launching the OOBE wizard.

![Windows Boot Logo](installation-screenshots/windows11-endpoint/23-windows-boot-logo.png)

**Country or Region** — Confirm your country is selected and click **Yes**.

![OOBE — Country Region](installation-screenshots/windows11-endpoint/24-oobe-country-region.png)

**Keyboard Layout** — Confirm your keyboard layout (e.g. US) and click **Yes**.

![OOBE — Keyboard Layout](installation-screenshots/windows11-endpoint/25-oobe-keyboard-layout.png)

**Second Keyboard Layout** — Click **Skip** unless you need an additional layout.

![OOBE — Second Keyboard Skip](installation-screenshots/windows11-endpoint/26-oobe-second-keyboard-skip.png)

Windows will show a loading screen while finishing configuration.

![OOBE — Good Things Coming](installation-screenshots/windows11-endpoint/27-oobe-loading-good-things.png)

> 💡 You may also be prompted to sign in with a Microsoft account, set a PIN, and configure privacy settings.

---

## Step 13 — Install UTM Guest Tools

Once the Windows 11 desktop appears, install the **UTM Guest Tools** to enable dynamic window resizing, clipboard sharing, and improved display performance.

![Windows 11 Desktop — First Boot](installation-screenshots/windows11-endpoint/28-windows11-desktop-first-boot.png)

### Open File Explorer

Click the **File Explorer** icon in the taskbar.

![Windows 11 Desktop — Taskbar](installation-screenshots/windows11-endpoint/29-windows11-desktop-taskbar.png)

Click **This PC** in the sidebar. You will see three drives listed under Devices and drives:

| Drive | Description |
|---|---|
| Local Disk (C:) | Windows installation drive (~63 GB) |
| CD Drive (D:) UTM Guest Tools | SPICE/Guest Tools disc (121 MB) |
| CD Drive (E:) | Windows installation ISO (6.79 GB) |

![File Explorer — This PC](installation-screenshots/windows11-endpoint/30-file-explorer-this-pc-drives.png)

### Run the Installer

Double-click **CD Drive (D:) UTM Guest Tools** to open it, then double-click `utm-guest-tools-0.1.271` to launch the installer.

![File Explorer — UTM Guest Tools Contents](installation-screenshots/windows11-endpoint/31-file-explorer-utm-guest-tools-contents.png)

### Complete the Wizard

Click **Next >** on the Welcome screen.

![UTM Guest Tools — Welcome](installation-screenshots/windows11-endpoint/32-utm-guest-tools-installer-welcome.png)

Read the License Agreement and click **I Agree**.

![UTM Guest Tools — License](installation-screenshots/windows11-endpoint/33-utm-guest-tools-installer-license.png)

Wait for the installation progress bar to complete.

![UTM Guest Tools — Progress](installation-screenshots/windows11-endpoint/34-utm-guest-tools-installer-progress.png)

Click **Finish** to complete the installation.

![UTM Guest Tools — Complete](installation-screenshots/windows11-endpoint/35-utm-guest-tools-installer-complete.png)

### Eject the UTM Guest Tools ISO

Now that the Guest Tools are installed, eject the UTM Guest Tools ISO from the UTM toolbar to clean up the mounted drives.

1. Click the **CD/DVD** drive icon in the UTM toolbar
2. Click **Eject** next to `utm-guest-tools-latest.iso`

> 💡 After ejecting, the CD/DVD entry will show as `none`, confirming it has been removed.

![UTM — Eject Guest Tools ISO](installation-screenshots/windows11-endpoint/36-utm-eject-guest-tools.png)

---

## ✅ Windows 11 is now fully installed and ready to use!

---

## Tips & Troubleshooting

| Issue | Solution |
|---|---|
| No product key | Click **I don't have a product key** during setup to activate later |
| Black screen on boot | Restart the VM — do not press any keys on subsequent restarts |
| SPICE tools not installed | Run `utm-guest-tools-0.1.271` from CD Drive (D:) inside Windows |
| Networking not working | In UTM VM settings, verify the Network adapter is set to Shared Network (NAT) |
| Poor performance | Increase RAM to 8 GB and CPU cores to 6+ in VM settings if your Mac supports it |

---

> For more help, visit [docs.getutm.app/guides/windows](https://docs.getutm.app/guides/windows)
