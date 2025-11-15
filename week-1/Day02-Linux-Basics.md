Day 2: Booting into Kali Linux Live + Persistence Setup

**Goal:**  
Successfully boot into the Kali Linux Live environment (GUI), confirm system hardware compatibility, and configure USB persistence to retain data and settings between reboots.

---

## ⚙️ Environment

| Component | Details |
|------------|----------|
| **Host Device** | HP Laptop (same as Day 1) |
| **BIOS Mode** | UEFI (Secure Boot disabled, Legacy Support disabled) |
| **USB Drive** | SanDisk 32 GB (configured with Rufus 4.x) |
| **ISO Used** | `kali-linux-2025.3-live-amd64.iso` |
| **Persistence Size** | 4 GB (set via Rufus slider) |
| **Boot Key Sequence** | `ESC → F9 → select USB Hard Drive (UEFI) – SanDisk` |

---

## 🧩 What I Did

1. **Rebuilt USB** using Rufus with the correct Live ISO:
   - Partition Scheme: `MBR`
   - Target System: `BIOS (or UEFI-CSM)`
   - Write Mode: `DD mode` (for reliability)
   - Enabled persistence (~4 GB)

2. **Fixed boot error:**  
   - Disabled Secure Boot in BIOS to fix `Verification failed: (0x1A) Security violation`.

3. **Booted successfully** into the Kali boot menu and selected:  
   → `Live system (amd64)` to confirm GUI loads.

4. **Verified hardware functionality:**
   - Wi-Fi, keyboard, display, and sound all working ✅

5. **Checked persistence partition:**
   ```bash
   df -h
Confirmed /dev/sdc2 mounted as persistence.

6. Created a test file:

echo "test persistence" > /home/kali/Desktop/persistence-test.txt


File appeared on Desktop ✅

7. Rebooted using persistence mode:
Selected Live system (persistence, amd64)
→ file still present ✅

🧰 Commands / Tools Used
df -h                # check mounted persistence
ls /home/kali/Desktop
sudo poweroff        # safe shutdown


BIOS Navigation: ESC → F10 → System Configuration → Boot Options
Kali Boot Menu: Live system with USB persistence

🧩 Problems & Fixes
Problem	Cause	Fix
Security violation (0x1A)	Secure Boot still enabled	Disabled Secure Boot in BIOS
File not saving after reboot	Booted without persistence mode	Rebooted via “Live system with USB persistence”
ls: cannot access '/home/kali/Desktop'	Wrong case in path (Desktop ≠ desktop)	Corrected command to /home/kali/Desktop
Mistyped 1s instead of ls	Typo (1 vs l)	Re-entered correct command
📘 Takeaways

Always disable Secure Boot before booting unsigned Linux distros like Kali.

Persistence mode must be manually selected at boot — plain Live mode won’t save changes.

Linux is case-sensitive: Desktop ≠ desktop.

Always shut down properly using sudo poweroff to avoid persistence corruption.

A persistent USB makes Kali fully portable — works on any machine with Secure Boot off.
