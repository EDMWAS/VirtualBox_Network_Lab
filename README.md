# VirtualBox_Network_Lab
This project demonstrates how to design and build a multi-subnet network environment inside Oracle VirtualBox. The lab focuses on network segmentation, traffic isolation, and controlled pivoting using a multi-homed system to manage access between distinct Local Area Networks (LANs).

## 🏢 Real-World Application

This lab mimics a standard enterprise security architecture used by businesses to protect their most sensitive data. 

* **The Jump Box / Bastion Host Pattern:** In the real world, **Linux Mint** acts as a "Jump Box." Companies do not allow employees or outside vendors to connect directly to database servers. Instead, users must log into the Jump Box first, and then jump to the secure internal network.
* **Blast Radius Minimization:** If an internet-facing machine (**Kali/External network**) gets compromised by an attacker, the attacker cannot immediately see or steal data from the internal database (**Ubuntu**). 
* **Defense in Depth:** This layout forces attackers to make multiple "hops" and break through multiple layers of security, giving network defenders more time to detect and stop the intrusion.

## Network Design & Isolation Rules

The infrastructure consists of three Virtual Machines (VMs) organized across two separate subnets:

* **Subnet 1 (Management/External LAN):** Shared by **Kali Linux** and **Linux Mint**. 
* **Subnet 2 (Secure/Internal LAN):** Shared by **Linux Mint** and **Ubuntu**.
* **The Bridge Node:** **Linux Mint** is configured with dual virtual network interfaces (Dual NICs), allowing it to communicate with both subnets simultaneously.
* **The Isolation Layer:** **Ubuntu** is initially blind to **Kali Linux** (and vice versa) because they live on entirely different network segments with no direct routing between them.

![Network Segmentation Diagram](<img width="1408" height="768" alt="image" src="https://github.com/user-attachments/assets/05fffbf7-0a58-4dcb-896b-71815962164d" />
)

## Technical Summary of Activities
1. **Multi-Subnet Architecture:** Built two isolated network segments inside VirtualBox to enforce hardware-level traffic separation.
2. **Dual-NIC Configuration:** Configured Linux Mint with two active adapters, assigning it one IP address on Subnet 1 and a second IP address on Subnet 2.
3. **Connectivity Verification:** Proven that Kali can talk to Mint, and Mint can talk to Ubuntu, while maintaining zero direct visibility between Kali and Ubuntu.
4. **Controlled Infrastructure Entry:** Established a secure remote connection path across the boundaries using **Port 22 (SSH)**.
