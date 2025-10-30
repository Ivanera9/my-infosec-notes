# 2025-10-29 — Day 3: Safe Shutdowns, Persistence Health & Fixing APT Locks

**Goal:**  
Learn safe shutdown practices in Kali Live Persistence mode, understand file service errors, handle interrupted updates, and maintain persistence integrity without damaging Windows partitions.

---

## ⚙️ Environment

| Component | Details |
|------------|----------|
| **Host Device** | HP Laptop |
| **BIOS Mode** | UEFI (Secure Boot disabled) |
| **USB Drive** | SanDisk 32 GB — Kali Live with 10 GB persistence |
| **Kali Version** | `kali-linux-2025.3-live-amd64.iso` |
| **Boot Mode** | Live system (persistence, amd64) |
| **Mount Points Checked** | Verified no internal Windows drive mounts before shutdown ✅ |

---

## 🧩 What I Did

1. **Rebooted Kali in persistence mode** after rebuilding the USB with Rufus.  
   - Ensured persistence partition recognized with:
     ```bash
     df -h
     ```
   - Verified `/dev/sdc2` mounted as persistence.

2. **Encountered multiple `file_000000... not found in file service` messages.**
   - Root cause: the system tried to access missing or corrupted live files (common in aged or heavily rewritten USBs).
   - Solution: rebuilt the ISO onto a clean USB with persistence.

3. **Ran system updates:**
   ```bash
   sudo apt update && sudo apt full-upgrade -y
Progress reached ~98% before network interruption.

Forced shutdown using sudo poweroff caused Windows to display “Fixing C: stage” next boot — indicating incomplete unmount.

Learned safe shutdown procedure:

Always close APT and unmount drives before poweroff:

bash
Copy code
sudo killall apt apt-get
sudo umount /media/kali/*
sudo poweroff
If APT blocks shutdown:

bash
Copy code
sudo systemctl poweroff -i
Verified system integrity on next boot:

No file corruption in persistence.

No Windows drive affected.

Rebooted safely into Kali persistence again — ✅ working as expected.

🧰 Commands / Tools Used
Command	Purpose
df -h	Check persistence partition mount
`ps aux	grep apt`
sudo killall apt apt-get	Stop blocked apt operations
sudo systemctl poweroff -i	Force poweroff ignoring inhibitors
sudo poweroff	Normal safe shutdown
sudo apt update && sudo apt full-upgrade	Full system update
sudo apt autoremove	Clean up unused packages after updates

🧩 Problems & Fixes
Problem	Cause	Fix
file_000000... not found in file service	Corrupted or incomplete USB boot sector	Rebuilt USB using Rufus in DD mode
Windows showing “Fixing C: stage”	Forced shutdown while C: mounted	Always unmount or ensure no mounts before poweroff
APT blocking shutdown	Background updates still running	Killed apt processes before shutdown
“No mount point specified”	No drives mounted	Safe to power off ✅
Persistence data lost	Booted without persistence mode	Rebooted via “Live system (persistence, amd64)”

📘 Takeaways
Always disable Secure Boot before launching Kali Live.

Never force power off while updates or APT are active.

“No mount point specified” = safe to shut down — no Windows drives mounted.

Persistence must be selected at boot — otherwise data won’t save.

Regularly clean and rebuild USB drives if recurring “file_000000…” errors appear.

Safe shutdown command to remember:

bash
Copy code
sudo killall apt apt-get; sudo umount /media/kali/*; sudo poweroff
