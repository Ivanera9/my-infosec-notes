 Create a Kali Live USB + BIOS Troubleshooting

Goal:
Set up a Kali Linux Live USB and boot it successfully on my HP laptop to begin learning Linux fundamentals and system boot concepts.

⚙️ Environment
Component      :	Details
Host Devic     :	HP Laptop (model hidden for privacy)
CPU            :	Intel Core i5-7200U @ 2.50 GHz (2 Cores / 4 Threads)
RAM            :	8 GB DDR4
Storage        :	238 GB SSD (AARVEX) + 932 GB HDD (TOSHIBA MQ04ABF100)
Graphics       :	Intel HD Graphics 620 (128 MB VRAM)
System Type    :	64-bit x64-based
Host OS        :	Windows 10 Home Single Language 22H2 (Build 19045.6456)
BIOS           :	HP InsydeH2O UEFI with Legacy Support
Virtualization :	Enabled (VT-x)
Target ISO     :	kali-2025.3-live-amd64.iso
Initial Mistake:	Downloaded kali-2025.3-installer-amd64.iso (no Live mode)
Boot Method    :	USB (Legacy mode, Secure Boot disabled)
USB Tool       :	Rufus 4.x on Windows
🧩 What I Did

Downloaded Kali ISO from Official Kali Downloads
.
Mistake: grabbed the installer version first instead of the live ISO.

Used Rufus on Windows to write the ISO to a 16 GB USB drive (default ISO mode first).
Booted laptop using ESC → F9 boot menu → selected USB device.

Encountered error:

Selected boot image did not authenticate


Learned about BIOS security options:

Entered BIOS via ESC → F10 → System Configuration → Boot Options

Disabled Secure Boot

Enabled Legacy Support (entered BIOS confirmation code)

Rebooted: installer menu only (no “Live” option) → realized ISO was installer build.

Re-downloaded correct image kali-2025.3-live-amd64.iso.

Planned rewrite of USB using Rufus in DD mode and verify checksum before boot.

🧰 Commands / Tools Used

Rufus GUI (Windows)

BIOS Navigation: ESC → F10 → System Configuration → Boot Options

ISO Verification:

# Linux/macOS
sha256sum kali-2025.3-live-amd64.iso

# Windows PowerShell
Get-FileHash -Algorithm SHA256 .\kali-2025.3-live-amd64.iso

Problems & Fixes
Problem	Cause	Fix
“Selected boot image did not authenticate”	Secure Boot blocked unsigned bootloader	Disabled Secure Boot in BIOS
Only installer menu (no Live mode)	Used installer ISO instead of Live image	Re-downloaded -live- version and rewrote USB in DD mode
📘 Takeaways

Always confirm the ISO filename includes -live- if you want a live session.

Secure Boot blocks unsigned bootloaders → disable it or enable Legacy mode.

Always verify ISO checksums before writing to USB.

Understanding BIOS options (UEFI vs Legacy) is essential for Linux installations.
Next: Boot into Kali Live session and capture a screenshot of the desktop.
