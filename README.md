# 🚀 Enterprise Multi-VLAN Office Network — Infrastructure Design & Verification

![Cisco Packet Tracer](https://img.shields.io/badge/Cisco%20Packet%20Tracer-v8.x-blue?style=for-the-badge&logo=cisco)
![Network Architecture](https://img.shields.io/badge/Architecture-Multi--VLAN%20Office%20Network-orange?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Verified%20%26%20Tested-success?style=for-the-badge)

## 📌 Project Overview

This project presents a compact, secure **Enterprise Office Network** designed and implemented using **Cisco Packet Tracer**. It simulates a small multi-department corporate environment featuring VLAN segmentation, Router-on-a-Stick Inter-VLAN routing, multi-router OSPF connectivity, centralized network services (DHCP, DNS, Web), hardened switch-port security, and SSH-based remote management.

---

## 🏗️ Topology & Architectural Highlights

- **Multi-Router Backbone:** 3 Cisco 2911 Routers interconnected via dedicated point-to-point `/30` links, forming the routed backbone of the network.
- **Access Layer:** 4 Cisco 2960 Switches enforcing VLAN segmentation across Finance, Sales, HR, and the Server Room.
- **Inter-VLAN Routing:** Router-on-a-Stick design using sub-interfaces for Layer 3 routing between departmental VLANs.
- **Dynamic Routing:** OSPF deployed across all three routers for automated route discovery and full network reachability.
- **Centralized Enterprise Services:** Server Room hosting a combined DHCP/DNS Server and an HTTP Web Server.
- **Security Hardening:** Port Security (Shutdown & Restrict violation modes) on access ports, plus SSH for encrypted remote device management.

---

## 🛠️ Key Technologies & Protocols

| Protocol / Technology | Implementation Details |
| :--- | :--- |
| **VLAN Segmentation** | 4 departmental VLANs (Finance, Sales, HR, Server Room) isolated via 802.1Q trunking. |
| **Inter-VLAN Routing** | Router-on-a-Stick configuration using sub-interfaces on Cisco 2911 routers. |
| **OSPF Dynamic Routing** | Multi-router OSPF adjacency established across 3 Cisco 2911 routers. |
| **DHCP Relay Agent** | Centralized DHCP allocation using `ip helper-address` on router sub-interfaces. |
| **DNS & Web Hosting** | Internal DNS name resolution pointing to the local HTTP Web Server. |
| **Port Security** | Sticky MAC learning with Shutdown & Restrict violation modes on access switches. |
| **SSH Remote Management** | Secure CLI access to network devices for encrypted remote administration. |

---

## 📊 VLAN Addressing & Inter-Router Links

| VLAN ID | Department / Zone | IP Subnet | Default Gateway |
| :---: | :--- | :--- | :--- |
| **10** | FINANCE | `192.168.10.0/24` | `192.168.10.1` |
| **20** | SALES | `192.168.20.0/24` | `192.168.20.1` |
| **30** | HR | `192.168.30.0/24` | `192.168.30.1` |
| **40** | SERVER ROOM | `192.168.40.0/24` | `192.168.40.1` |

| Link | Network |
| :--- | :--- |
| Router1 ↔ Router2 | `10.0.0.0/30` |
| Router2 ↔ Router3 | `10.0.0.4/30` |

---

## ⚙️ Essential CLI Configuration Snippets

<details>
<summary><b>1. Router-on-a-Stick Inter-VLAN Routing & DHCP Relay</b></summary>

```text
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0

Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0

Router(config)# interface GigabitEthernet0/0.40
Router(config-subif)# encapsulation dot1Q 40
Router(config-subif)# ip address 192.168.40.1 255.255.255.0
Router(config-subif)# ip helper-address 192.168.40.2
```
</details>

<details>
<summary><b>2. Switch Port Security Configuration</b></summary>

```text
Switch(config)# interface FastEthernet0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport port-security
Switch(config-if)# switchport port-security maximum 1
Switch(config-if)# switchport port-security mac-address sticky
Switch(config-if)# switchport port-security violation restrict
```
</details>

---

## ✅ Verification & Testing Results

- **Dynamic IP Allocation:** Verified across all VLANs via DHCP Relay Agent (`ip helper-address`).
- **End-to-End Connectivity:** ICMP ping verified between all VLAN subnets and across all inter-router links.
- **DNS & Web Services:** End-user browser testing confirms successful HTTP web page access via the internal DNS record.
- **OSPF Neighbor Adjacency:** Confirmed full adjacency across all three routers via `show ip ospf neighbor`.
- **Remote Management & Port Security:** SSH access confirmed; Shutdown and Restrict violation modes tested and verified on access ports.

---

## 👤 Author
**Yadigarzade Ceyhun**
- **Project:** Enterprise Network Services Lab
- **Environment:** Cisco Packet Tracer v8.x
