# NETWORKWALKS-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP
Cybersecurity Lab Setup
# 🔐 Cybersecurity Lab Environment Setup

Isolated virtual lab for penetration testing and ethical hacking practice, built on VirtualBox + Kali Linux.
<p align="center">
  <img src="https://img.shields.io/badge/Skill-Cybersecurity-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ver-Virtualbox%20v7.2-0070C0?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Kali%20Linux-v2026.2-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Linux-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Network-10.0.0.0%2F24-238F89?style=flat-square&labelColor=000000" />
  <img src="https://img.shields.io/badge/Penetration%20Testing-C00000?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Skill-Virtualization-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/GitHub-404040?style=flat-square&labelColor=0070C0&logo=github&logoColor=white" />
  <img src="https://img.shields.io/badge/Kali%20Linux-404040?style=flat-square&labelColor=C00000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/NetworkWalks-404040?style=flat-square&labelColor=C00000" />
  <img src="https://img.shields.io/badge/Ethical%20Hacking-E87500?style=flat-square&labelColor=000000&logo=kalilinux&logoColor=white" />
  <img src="https://img.shields.io/badge/Victor%20Olatuja%20-C00000?style=flat-square" />
</p>


## Overview
<img width="1365" height="733" alt="image" src="https://github.com/user-attachments/assets/c8f6b4ce-e7c9-4cd6-a3fc-ffd87e9b410e" />

I set up a virtual pentesting lab using VirtualBox and Kali Linux to have a safe, repeatable environment for practicing network scanning, recon, and vulnerability assessment. The lab sits on its own private virtual network, so I can drop in additional target machines later without touching my host network.

## 🎯 Objectives

- Install and configure VirtualBox
- Import Kali Linux as a VM
- Create a private NAT Network for the lab
- Get Kali talking on that network with a consistent IP
- Verify connectivity and DNS resolution
- Document the setup and any issues I ran into along the way

## ⚙️ Lab Configuration

| Component | Configuration |
| :--- | :--- |
| Host OS | Windows (Lenovo ThinkPad) |
| Hypervisor | VirtualBox |
| Security OS | Kali Linux 2026.2 |
| Kali RAM | 2048 MB |
| Virtual Network | NAT Network (`NatNetwork`) |
| Network Address | 10.0.0.0/24 |
| Kali IP Address | 10.0.0.2/24 |
| Default Gateway | 10.0.0.1 |
| DNS Server | 8.8.8.8 |

## 🪜 Setup Steps

### 1. Install VirtualBox
Installed VirtualBox on the host to act as the type-2 hypervisor for the lab.

### 2. Create the NAT Network 
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/b67eeba8-bc5e-48f7-9c22-2de796d247fe" />

Created a dedicated NAT Network (`NatNetwork`) with the IPv4 prefix `10.0.0.0/24` and DHCP enabled, so any future VMs added to the lab can reach each other and still get outbound access.

### 3. Import Kali & Configure Adapters
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/c60b9717-1432-4139-a257-6c611f12cbdb" />

Imported the Kali Linux VM and set it up with:
- Adapter 1 attached to `NatNetwork`, adapter type Intel PRO/1000 MT Desktop
- 2048 MB RAM allocated

### 4. Configure Static IP
<img width="1366" height="768" alt="image" src="https://github.com/user-attachments/assets/d7e76190-b688-4592-8034-66e1194403a7" />

Gave Kali's network interface a static address (`10.0.0.2`), gateway (`10.0.0.1`), and DNS (`8.8.8.8`) so it's consistent across future labs instead of getting a new DHCP lease every boot.

## 🐞 Problems I Ran Into

### VT-x disabled in BIOS
First boot of the Kali VM failed — turned out hardware virtualization (VT-x) was disabled in the ThinkPad's firmware settings.

**Fix:**
1. Restarted the laptop and entered the ThinkPad Setup utility
2. Went to Security → Virtualization
3. Enabled Intel Virtualization Technology
4. Saved with F10 and rebooted into Windows
5. Launched VirtualBox and Kali booted fine after that

## 💡 What I Learned

- How to set up isolated NAT networks for multi-VM labs
- Why VT-x/SVM needs to be enabled in BIOS/UEFI before a hypervisor will even boot a VM
- How to configure and verify a static IP on Linux

## 🔒 Security & Ethical Use

This lab is for educational purposes and authorized security testing only.
