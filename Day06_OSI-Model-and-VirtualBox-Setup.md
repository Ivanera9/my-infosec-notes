🧠 Day 6 — OSI Model & VirtualBox Setup

📅 Date: 2025-11-05
🧩 Focus: Understanding the 7 Layers of Networking & Setting up a VirtualBox Environment

🎯 Goal

After multiple persistence issues and system corruptions, today’s goal was twofold:

Build a stable, isolated learning environment using VirtualBox.

Begin learning foundational networking — specifically the OSI 7-Layer Model — which is crucial for cybersecurity, packet analysis, and understanding network tools later on.

⚙️ System Setup
Component	Details
Virtualization Software	VirtualBox 7.1
Host System	Windows 10 (Repaired & Stable)
Guest OS	Kali Linux 2025.3 Rolling
Resources Allocated	4 GB RAM / 2 CPU cores / 40 GB Virtual Disk
Network Adapter Mode	NAT (Default)
ISO Used	kali-linux-2025.3-installer-amd64.iso

🧰 Reason for switching:
Live persistence caused frequent file system corruption and unsafe shutdowns. VirtualBox provides a safe sandbox, snapshot control, and better persistence management — ideal for consistent learning.

🌐 Networking Fundamentals — OSI 7 Layer Model

The OSI (Open Systems Interconnection) Model standardizes how data travels through a network.
It breaks communication into 7 layers, each with a defined role:

Layer	Name	Function	Example Protocols
7	Application	Interface between user and network	HTTP, HTTPS, SSH, FTP
6	Presentation	Data translation, encryption, compression	SSL/TLS, JPEG, ASCII
5	Session	Establishes and maintains sessions	NetBIOS, RPC
4	Transport	Reliable data transfer, segmentation	TCP, UDP
3	Network	Logical addressing and routing	IP, ICMP
2	Data Link	Physical addressing, error detection	Ethernet, ARP
1	Physical	Transmission of bits through medium	Cables, NIC, Wi-Fi, Hubs

🧠 Analogy:

Layer 7 is what you see (browser).

Layer 4 ensures delivery.

Layer 1 is the wire carrying the signal.

💻 Commands Practiced
Command	Purpose
ip a	Display network interfaces & IPs
ping 8.8.8.8	Test connectivity to Google DNS
netstat -tulnp	View active listening ports
traceroute google.com	Show route packets take across the network
ifconfig	(legacy) Check interface configuration
hostname -I	Show local IP address
🧩 Problems & Fixes
Problem	Cause	Fix
Host-only network not detected	VirtualBox network service missing	Reinstalled VirtualBox with “Network Adapter” checked
Kali VM black screen	Display controller mismatch	Changed from VMSVGA → VBoxSVGA in display settings
Slow updates	Default mirror lag	Changed to http://http.kali.org/kali
No internet in guest	Network adapter misconfigured	Switched adapter mode to “NAT”
📘 Takeaways

The 7 layers of OSI define how data flows — from user applications to hardware signals.

Each layer depends on the one below it, forming a modular stack.

VirtualBox snapshots are your new best friend:

“If you break the system, revert — don’t reinstall.”

A VM is vastly safer and faster than Live USB persistence for experimentation.

⚙️ Next Steps (Day 7 Preview)

Practice TCP/IP vs OSI mapping (practical version).

Capture packets using Wireshark to visualize the OSI flow.

Document network configurations in VirtualBox.

✅ Status
Component	Result
OSI Model Understanding	✅ Clear conceptual grasp
VirtualBox Setup	✅ Complete & Stable
Network Connectivity	✅ Working (NAT mode)
Host OS Recovery	✅ Successful after corruption
Next Focus	🟢 TCP/IP stack + Wireshark intro
