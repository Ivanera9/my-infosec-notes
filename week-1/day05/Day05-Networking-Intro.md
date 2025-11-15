# 🧠 2025-11-01 — Day 5: Networking Introduction & Realization About Learning Setup

**Goal:**  
Begin understanding basic networking concepts — types, devices, and transmission methods — and reflect on the repeated system corruption issues that occurred while using Kali Linux Live Persistence.  
The main outcome today was recognizing that **a Virtual Machine (VM)** is a better environment for consistent and stable learning.

---

## 🧩 What I Learned

### 🌐 Networking Basics
Today I started learning the **introduction to networking** — the fundamental layer that everything in cybersecurity depends on.  

Key concepts covered:
- **Types of Networks:** PAN, LAN, MAN, WAN, VPN  
- **Internet Connections:** Broadband, Mobile Data, Satellite, Fiber  
- **Network Devices:** Routers, Switches, Hubs, Modems, Access Points, Bridges  
- **Transmission Media:** Wired (Twisted Pair, Coaxial, Fiber Optic) and Wireless (Radio Waves, Infrared, Microwave)  
- **Switching Methods:** Circuit Switching, Packet Switching, and Message Switching  

> 🧠 *Takeaway:* Networking is the foundation for everything that happens in cybersecurity.  
> Understanding how data moves across systems and devices is the first step toward learning how to secure — or exploit — those systems.

---

## 💥 What Went Wrong

While working on Kali Live Persistence, my screen went black during shutdown.  
I assumed the system was off and **removed the USB drive manually**.  

That mistake caused:
- **Windows corruption** on the host system  
- **Loss of persistence data** on the Kali USB  
- Need to rebuild both environments again  

This was my **second corruption incident** — and the breaking point where I realized that Live Persistence is not sustainable for long-term learning.

---

## ⚙️ The Realization

Using **Kali Live Persistence** might look convenient, but it’s not meant for beginners who are still learning Linux and system management.  

It’s fragile, slow, and one wrong shutdown can destroy hours of progress.  

### Why Live Persistence Failed Me
- Unsafe shutdowns corrupted persistence multiple times  
- Updates and upgrades often broke due to the overlay filesystem  
- USB write speeds caused freezes and incomplete writes  
- Difficult to back up or recover if something went wrong  

---

## 🔁 The Decision

Starting tomorrow (**Day 6**), I’ll move to a **Virtual Machine (VM)** setup.  
It’s safer, faster, easier to maintain, and supports snapshots — meaning I can roll back anytime something breaks.

> 🧭 *Lesson Learned:*  
> Learning cybersecurity isn’t about being fancy with your setup.  
> It’s about building a **stable, controlled environment** that lets you focus on learning — not constant recovery.

---

## 🧰 What’s Next

- Install **Kali Linux 2025.3** on a **Virtual Machine (VMware or VirtualBox)**  
- Set up a clean base snapshot for recovery  
- Continue learning from networking theory into practical hands-on work  
- Recreate my Git and system setup inside the VM for long-term use  

---

## ✅ Status Summary

| Area | Status |
|-------|---------|
| Networking Basics | Completed ✅ |
| Kali Live Persistence | Corrupted & Discontinued ❌ |
| Windows Host | Corrupted but Restored ⚠️ |
| VM Setup | Planned for Tomorrow 🕒 |
| Learning Stability | Improved Awareness ✅ |

---

## 📘 Takeaways

- Understanding **how networks function** is essential before doing anything in cybersecurity.  
- Stability is key — without it, every learning session turns into recovery time.  
- Never remove a USB drive or power off a system until it’s *fully* shut down.  
- Virtual Machines are the best learning environment for beginners.  

