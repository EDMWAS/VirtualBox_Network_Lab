# 🔐 VirtualBox Network Pivoting Lab

## Overview

This project demonstrates a segmented cybersecurity lab built using **Oracle VirtualBox**. Three Linux virtual machines are separated across two isolated LANs, with a dual-homed Linux Mint system providing the only connection between the external and internal network segments.

The lab demonstrates **network segmentation, multi-NIC configuration, routing verification, SSH access, connectivity testing, and controlled pivoting between isolated networks**.

---

## 🌐 Network Architecture

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/31f54c7c-e022-4872-93f9-0ea20d2aa331" />


### Network Segments

**LAN 1:** `192.168.10.0/24`  
Kali ↔ Linux Mint

**LAN 2:** `192.168.20.0/24`  
Linux Mint ↔ Ubuntu

Linux Mint is **dual-homed**, with one network interface connected to each LAN.

---

## 🖥️ Lab Environment

The environment consists of three Linux virtual machines running simultaneously in VirtualBox.

**Screenshot:** VirtualBox environment showing Kali Linux, Linux Mint and Ubuntu.
<img width="1918" height="1011" alt="image" src="https://github.com/user-attachments/assets/28ad70c6-c9a9-49a9-9f91-5830d9d45a9b" />




---

## 🔀 Dual-Homed Pivot Configuration

Linux Mint provides the connection point between the two isolated networks.

<img width="943" height="623" alt="image" src="https://github.com/user-attachments/assets/f7fa6a0f-48f9-4b20-8ee9-cba19e5e0ec2" />


The Mint routing table confirms two active network connections:

```text
192.168.10.0/24 → 192.168.10.3
192.168.20.0/24 → 192.168.20.3
```

This allows Mint to communicate directly with systems on both LANs.

---

## 🔎 Connectivity & Isolation Testing

Connectivity testing was performed to verify the segmentation design.

| Test | Result |
|---|---|
| Kali → Mint | ✅ Reachable |
| Mint → Ubuntu | ✅ Reachable |
| Kali → Ubuntu | ❌ No Direct Access |

### Kali → Mint

```bash
ping 192.168.10.3
```

<img width="926" height="782" alt="image" src="https://github.com/user-attachments/assets/55b9caaa-3e77-4ae8-970a-be0c4c895dac" />


### Mint → Ubuntu

```bash
ping 192.168.20.2
```


<img width="937" height="621" alt="Screenshot 2026-08-14 010909" src="https://github.com/user-attachments/assets/6739d8e2-b8d6-4cde-9302-8470c8d84404" />



### Kali → Ubuntu

```bash
ping 192.168.20.2
```

<img width="922" height="776" alt="Screenshot 2026-08-14 011247" src="https://github.com/user-attachments/assets/d30cd056-4d18-425d-9824-1412459b1f89" />




The failed direct connection demonstrates that Kali and Ubuntu remain isolated on separate network segments.

---

## 🔐 SSH & Pivoting

SSH is used to establish access from Kali to the dual-homed Mint system.

```bash
ssh <username>@192.168.10.3
```


<img width="918" height="780" alt="Screenshot 2026-08-14 011545" src="https://github.com/user-attachments/assets/1f0cb859-85b7-408d-bb91-b2f73ce67cdd" />




From the Mint system, the internal Ubuntu host on `192.168.20.2` becomes reachable through LAN 2.

### Access Path

```text
Kali Linux
192.168.10.2
      │
      │ SSH
      ▼
Linux Mint
192.168.10.3
192.168.20.3
      │
      │ Internal LAN
      ▼
Ubuntu
192.168.20.2
```

<img width="932" height="848" alt="Screenshot 2026-08-14 011826" src="https://github.com/user-attachments/assets/bb348331-28c9-47a0-a9ab-aebff5e52a40" />


**Final path:** `Kali → Linux Mint → Ubuntu`

---

## 🛠️ Skills Demonstrated

- VirtualBox network configuration
- Network segmentation and subnetting
- Linux TCP/IP configuration
- Dual-NIC / multi-homed host configuration
- Linux routing analysis
- ICMP connectivity testing
- SSH remote access
- Network isolation verification
- Pivoting between segmented networks

---

## ⚙️ Technologies

`VirtualBox` `Kali Linux` `Linux Mint` `Ubuntu` `SSH` `TCP/IP` `IPv4`

---

## ⚠️ Disclaimer

This project was performed entirely within an isolated, locally controlled virtual lab for cybersecurity education and network administration practice.
