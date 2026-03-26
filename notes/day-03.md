# Day 3 — VirtualBox: Configuring Virtual Machines

## 🎯 Objective

To install and configure the VMs for this homelab:

- Windows Server
- Employee Machine
- Attacker Machine
- SEIM Server (Ubuntu)

---

## 🧠 Lab Design Overview

This lab will go through the configuration steps for the configuration of the VMs that will be used for this project

- Frist: set-up and configure Windows Server 2022
- Second: set-up and configure Ubuntu 24.04.4 LTS
- Third: set-up and configure Windows 10
- Fourth: set-up and configure Kali Linux

---

## 🖥️ VirtualBox VM Specs

| Machine Name | OS | Base Memory | # CPUs | Hard Disk |
| ------------ | -- | ----------- | ------ | --------- |
| Dpmain-Controller01 | Windows Server 2022 | 4096 MB | 2 | 50 GB |
| SIEM-01 | Ubuntu 24.04.4 LTS | 2048 MB | 2 | 30 GB |
| WIN10-CLIENT | Windows 10 (64-bit) | 4096 MB | 2 | 40 GB |
| kali-linux-2026.1-virtualbox-amd64 | Kali Linux | 2048 MB | 2 | 30 GB |

---

## 🌐 Set-up Walk Through

### Domain Controller - Windows Server

**Domain Controller VM Specs:**
![DC-Specs](vb-setup-01.png)
![DC-Specs](vb-setup-02.png)
![DC-Spces](vb-setup-03.png)

**Domain Controller Launch Set-up:**
![DC-Setup](dc-setup-01.png)
![DC-Setup](dc-setup-02.png)
![DC-Setup](dc-setup-03.png)
![DC-Setup](dc-setup-04.png)
![DC-Setup](dc-setup-05.png)

### SIEM Server - Ubuntu

**SIEM Server VM Specs:**
![SIEM-Specs](siem-setup-01.png)
![SIEM-Specs](siem-setup-02.png)
![SIEM-Specs](siem-setup-03.png)
![SIEM-Specs](siem-setup-04.png)

**SIEM Server Launch Set-up:**
![SIEM-Setup](siem-setup-05.png)
![SIEM-Setup](siem-setup-06.png)
![SIEM-Setup](siem-setup-07.png)
![SIEM-Setup](siem-setup-08.png)
![SIEM-Setup](siem-setup-09.png)
![SIEM-Setup](siem-setup-10.png)
![SIEM-Setup](siem-setup-11.png)
![SIEM-Setup](siem-setup-12.png)
![SIEM-Setup](siem-setup-13.png)
![SIEM-Setup](siem-setup-14.png)
![SIEM-Setup](siem-setup-15.png)
![SIEM-Setup](siem-setup-16.png)
![SIEM-Setup](siem-setup-17.png)

### Client Machine - Windows 10

**Client Machine VM Specs:**
![Client-Specs](windows-setup-01.png)
![Client-Specs](windows-setup-02.png)
![Client-Specs](windows-setup-03.png)
![Client-Specs](windows-setup-04.png)

**Client Machine Launch Set-up:**
![Client-Set-up](windows-setup-05.png)
![Client-Set-up](windows-setup-06.png)
![Client-Set-up](windows-setup-07.png)
![Client-Set-up](windows-setup-08.png)

### Attacker Machine - Kali Linux

**Attacker Machine VM Specs:**
![Attacker-Specs](kali-setup-01.png)
![Attacker-Specs](kali-setup-02.png)
![Attacker-Specs](kali-setup-03.png)

**Attacker Machine Launch Set-up:**
![Attacker-Setup](kali-setup-04.png)
![Attacker-Setup](kali-setup-05.png)

## 📡 Internal Network Testing

As a refresher the machines that are within the Internal Network (internal-labnet):

- Domain Controller
- SIEM Server
- Client Machine

In this Lab the Attacker Machine was configured to NAT but I have also enabled its Adapter 2 to Internal Network and linked it to internal-labnet. This will save time as I want to practice insider threats as well.

### Test Results

![Net-Test](network-test-01.png)
![Net-Test](network-test-02.png)
![Net-Test](network-test-03.png)
![Net-Test](network-test-04.png)
![Net-Test](network-test-05.png)
![Net-Test](network-test-06.png)
![Net-Test](network-test-07.png)
![Net-Test](network-test-08.png)
![Net-Test](network-test-09.png)

**Attacker Machine on Internal Network Test Reaults:**
![Net-Test](kali-setup-06.png)
![Net-Test](kali-setup-07-1.png)
![Net-Test](kali-setup-08.png)
![Net-Test](kali-setup-09.png)

## 🧠 Key Learnings

- Installing various virtual machines with different OS
- Firewall rule creation to allow echo requests
- Network connection between machines within the same network
- Ubuntu, Windows, and Kali Linux OS configuration

---

## 🚧 Challenges

The biggest challenge I encountered was testing the connection between the client, domain controller, and attacker machines.

First when I tested the connection with **ping 192.168.56.10 (DNS Server)** on the client machine, I was losing packets. I was flustered as I did not know what caused that. I thought that since in the set-up of the client vm, I set its adapter to **Internal Network** on **internal-labnet**, it was all that it needed. After doing some research, turns out, Windows by default blocks echo requests to other machines. This supprised me, so I went and found out I can create an inboud rule to the Windows Firewall.

Which I went into **Windows Defender Firewall with Advanced Security** and created an allow rule to allow all echo requests. I first did this on the client machine and when I tested it again, I was shocked that it failed once more. So I sat ther for a bit and it kicked into me that it should be configured on my Domain Controller machine. Which I made the change and then tested after on the client machine. And was happy that I was not receivng packets compared to losing them.

**This taught me two things:**

- One Windows by default allow everything except for Echo request, which confuses me. I will have to research it first.
- Two, creating vms, testing them and finding out it failed but then after you fix the issue, it works. Is so much fun!

---

## 🔜 Next Steps

- Active Directory setup
- Promote DC
- JJoin Windos 10 to domain
