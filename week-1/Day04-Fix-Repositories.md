2025-10-30 — Day 4: Repository Fix, Source Validation & Safe Exit Automation
🎯 Goal

Repair broken sources.list configuration, resolve APT repository conflicts (file:/run/live/medium warnings), perform a full system upgrade on persistent Kali, and establish a verified safe shutdown process.

⚙️ Environment
Component	Details
Host Device	HP Laptop
BIOS Mode	UEFI (Secure Boot disabled)
USB Drive	SanDisk 32 GB — Kali Live with 16 GB persistence
Kali Version	kali-linux-2025.3-live-amd64.iso
Boot Mode	Live system (persistence, amd64)
Mount Points Verified	/dev/sdc1 = live medium, /dev/sdc2 = persistence, no internal drives mounted ✅
🧩 What I Did
1️⃣ Verified persistence mount
df -h


Confirmed /dev/sdc2 mounted under /run/live/persistence/sdc2 with 11 GB free space.

2️⃣ Fixed APT repository conflicts

Issue:
Warning: Conflicting distribution: file:/run/live/medium kali-last-snapshot

Cause:
Live snapshot entry in /etc/apt/sources.list conflicting with rolling repo.

Fix:

sudo nano /etc/apt/sources.list


Replaced contents with:

deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware
deb-src http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware


✅ Removed all file:/run/live/medium entries
✅ Saved (Ctrl + O) and exited (Ctrl + X)

3️⃣ Updated and verified repositories
sudo apt clean
sudo apt update


Output:
Hit:1 http://http.kali.org/kali kali-rolling InRelease
504 packages can be upgraded. ✅

4️⃣ Performed full upgrade
sudo apt full-upgrade -y


Download size: ~972 MB

Used ~4.6 GB of persistence

502 upgraded, 31 newly installed

Ignored harmless dpkg: directory not empty warnings

5️⃣ Verified no APT or drive conflicts
ps aux | grep apt
lsblk


Output confirmed:

No active apt processes ✅

Only /dev/sdc1 & /dev/sdc2 mounted ✅

6️⃣ Clean shutdown (safe power off)
sudo umount /run/live/persistence/sdc2
sudo poweroff


✅ System powered off safely with persistence data intact.

🧰 Commands Used
Command	Purpose
df -h	Check persistence partition usage
sudo nano /etc/apt/sources.list	Fix APT repo configuration
sudo apt clean && sudo apt update	Refresh package sources
sudo apt full-upgrade -y	Update entire system
`ps aux	grep apt`
lsblk	Check mounted drives
sudo umount /run/live/persistence/sdc2	Unmount persistence safely
sudo poweroff	Safe system shutdown
⚙️ Safe Exit Automation

Created a reusable safe shutdown script:

echo -e '#!/bin/bash\nsudo umount /run/live/persistence/sdc2\nsudo poweroff' | sudo tee /usr/local/bin/safe-exit
sudo chmod +x /usr/local/bin/safe-exit


Now you can type:

safe-exit


✅ Automatically unmounts persistence and powers off safely.

🧩 Problems & Fixes
Problem	Cause	Fix
file:/run/live/medium conflict	Old live snapshot entry	Edited /etc/apt/sources.list
Malformed line in sources.list	Typo (eeb → deb)	Corrected manually
Unable to fetch archives	Weak mirror	Switched to main http.kali.org mirror
dpkg warning: directory not empty	Harmless post-upgrade	Ignored
Persistence shrinking	Cache files filling space	Ran sudo apt clean
📘 Takeaways

✅ Correct repo configuration:

deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware


✅ Always verify:

ps aux | grep apt


before shutdown — ensures no background updates.

✅ /dev/sdc1 & /dev/sdc2 = your USB; safe to power off when only those are mounted.

✅ Use safe-exit for consistent, corruption-free shutdowns.

✅ Persistence confirmed stable for future sessions.

✅ Status Summary
Check	Result
APT Repositories	Fixed & Updated
Persistence	Stable & Mounted
Internal Drives	Unmounted ✅
Safe Shutdown	Verified ✅
Windows Integrity	Unaffected ✅
