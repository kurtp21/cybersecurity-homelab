# Day 2 — Network Design & Virtual Lab Planning

## 🎯 Objective

Designing and the lab network architecture, planning IP addressing and setting up VirtualBox netorking

---

## 🧠 Lab Design Overview

This lab with document and simulate a small enterprise network with a domain controller, client, threat actorm, and monitoring system (for future use)

---

## 🖥️ Planned Virtual Machines

| Machine Name | OS | Role | Notes |
| ------------ | -- | ---- | ----- |
| Windows Server | Windows Server 2022 | Acts as the Domain controler | 2-4 GB |
| Employee Machine | Windos 10 | Target machine for attackers | 2-4 GB |
| Attacker Machine | Kali Linux | Plays the attacker | 2 GB |
| SEIM Server | Ubuntu Server 22.04 LTS | Simulates SOC environment | 2 GB |

---

## 🌐 Network Configuration Plan

### Network Type

**This lab will utilize two network types:**

Internal Network:

- Used by Windows Server, Employee Machine, SEIM server
- To isolate the environment and make it safe for testing

NAT:

- Used by the Attaker Machine
- To simulate an external attacker of the network

### Network Name

***internal-labnet***

- Configured with Internal Network
- Essentially the lab's LAN

### IP Range

***192.168.56.0/24***

- For simplicity and easy management
- Simulates a small enterprise network
- 192.168.56.xxx is a private IP Range thats great for homelabs

---

## 📡 IP Addressing Scheme

***Internal Network***

| Machine | IP Address | Purpose | Notes |
| ------- | ---------- | ------- | ----- |
| Domain Controler | 192.168.56.10 | AD, DNS | Critical server |
| Employee Machine | 192.168.56.20 | Client | User Machine |
| Ubuntu Server | 192.168.56.30 | SEIM | Log collection |
| Reserved | 192.168.56.40 | SEIM | Used for Kali Later |

***NAT Network***

| Machine | IP Address | Purpose | Notes |
| ------- | ---------- | ------- | ----- |
| Kali Linux | DHCP | Attacker | Dynamically assigned |

---

## 🔐 Network Segmentation (Optional)

The network will be segmented into two:

- Internal Network (192.168.56.0/24)
- External Network (NAT - for now)

---

## 🧪 Connectivity Plan

The internal lab machines "internal-labnet" containing the Domain Controller, Clients, and Ubuntu Servers. Will be able to communicate over a private subnet with static IPs. Will be able to ping internal network machines and use RDP and SSH as well.

Attacker machine will be isolated from the internal network as it is configured with NAT. Can enable dual-network cofiguration to allow insider threat simulation. This can be done by adding a second network adaptor.

---

## 📸 Diagrams

***Network Layout***
![Network Layout](network-layout-diagram.png)

---

## 🧠 Key Learnings

- Importance of network design, separating internal and external networks
- Avoiding IP addressing conflicts by segmenting networks and static IP addressing
- Importance of VM layout for small enterprise homelab setup

---

## 🚧 Challenges

- Allocating RAM ussage: Ensuring that personal machine will be cappable of running multiple VMs.
- Decision on Network Segmentation: Was unsure how to segment the internal network and external network, to simulate real world attacks. Did not know how IP addressing should be layed out for the attacker machine, but eventually settled with NAT for DHCP allocation.

---

## 🔜 Next Steps

- Create virtual machines
- Configure networking in VirtualBox
