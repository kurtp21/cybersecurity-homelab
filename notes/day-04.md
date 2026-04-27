# Day 4 - Active Directory and Domain Setup

## 🎯 Objective

Installation and configuration of Active Directory on Ddomain Controller and to join Client Machine to a Domain

---

## 🧠 Lab Design Overview

This lab will highlight the configuration of Active Directory on the Domani controller server.

1) Installation of Active Directory Services on DC server
2) Promotion of DC server to Active Directory
3) Adding WIN10-Client VM to new domain

---

## ⚙️ Domain Forest Specs

- **Forest Name:** homelab.local

## 🌐 Set-up Walk Through

**Active Directory Services installation on Windows Server**
![DC-Setup](ad-setup-01.png)
![DC-Setup](ad-setup-02.png)
![DC-Setup](ad-setup-03.png)
![DC-Setup](ad-setup-04.png)
![DC-Setup](ad-setup-05.png)
![DC-Setup](ad-setup-06.png)
![DC-Setup](ad-setup-07.png)
![DC-Setup](ad-setup-08.png)
![DC-Setup](ad-setup-09.png)
![DC-Setup](ad-setup-010.png)
![DC-Setup](ad-setup-11.png)
![DC-Setup](ad-setup-12.png)
![DC-Setup](ad-setup-13.png)

**Adding Windows Client to Domain Controller**
![Win-join-to-domain](ad-setup-17.png)
![Win-join-to-domain](ad-setup-14.png)
![Win-join-to-domain](ad-setup-15.png)
![Win-join-to-domain](ad-setup-16.png)

## 🧠 Key Learnings

- Instalation of Active Directory on a indows server
- Promoting a server to a to a domain controller
- Creation of a new domain forrest
- Adding a windows client to domain forest
- Trouble shooting on domain server with active directory installed

---

## 🚧 Challenges

The main issue I encountered was when I promoting the windows server to a domain controller. I received an error with the prerequisites check, I received the error: **"Verification of prerequisites for domain controller promotion failed. Certificate Server is installed."**

After searching through the web, I found out that, although you can technically install both **Active Directory Certificate Services** and **Active Directory Domain Services** on the same machine. It poses security issues and therefore not encouraged.

After finding this out I reconfigured the Windows Server, I removed the Active Directory Certificate Services and underwent the promotion again. I then was able to pass the prerequisite check and was able to promote the server to a Domain Controller.

![DC-Error](ad-setup-error-1.png)
![DC-Error](ad-setup-error-2.png)
![DC-Error](ad-setup-error-3.png)

---

## 🚀 Next Steps

- Create domain users
- Configure Group Policy
- Begin log collection into SIEM
- Simulate attacks from Kali
