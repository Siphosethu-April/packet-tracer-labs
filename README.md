# 🌐 Multi-VLAN Network with Internet Access (Cisco Packet Tracer)

## 📘 Overview

This project simulates a real-world small office network using **Cisco Packet Tracer**. It includes:

- Multiple VLANs: Accounting (VLAN 10) & Payroll (VLAN 20)
- Inter-VLAN routing via **Router-on-a-Stick**
- **DHCP** per VLAN
- Internet access via **NAT** and an **ISP router**
- Shared network printer
- Fully documented configs

---

## 🛠 Topology

![Topology](https://github.com/user-attachments/assets/59b3ac9f-aae7-492b-a504-a764972d06da)



---

## 🧩 Network Design

| VLAN | Department | IP Range           | Gateway         |
|------|------------|--------------------|-----------------|
| 10   | Accounting | 192.168.10.0/24    | 192.168.10.1    |
| 20   | Payroll    | 192.168.20.0/24    | 192.168.20.1    |

---

## 🔧 Devices Used

- 🛜 Cisco 2811 Router (R1) – Inter-VLAN routing, NAT, DHCP
- 🌐 Cisco 2811 Router (R2) – Simulated ISP
- 🧩 2x Cisco 2960 Switches (SW1, SW2)
- 💻 4 PCs
- 🖨 1 Printer
- 🌍 Optional: Server for internet simulation

---

## 🧰 Configurations

All CLI configurations are in the `/configs` folder:

