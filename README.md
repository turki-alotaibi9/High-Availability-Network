# Enterprise High-Availability Network Design (Cisco Packet Tracer)

## Architecture Overview
This project presents a multi-tiered, resilient enterprise network architecture designed in Cisco Packet Tracer. The topology ensures seamless failover, optimal path selection, and department-level network segmentation through layer 2 and layer 3 redundancy protocols[cite: 3].

---

## Core Infrastructure & Topology Components

### 1. Gateway & Path Redundancy
* **HSRP (First Hop Redundancy Protocol):** Configured between `Multilayer Switch-1` and `Multilayer Switch0` to establish active/standby default gateway redundancy across subnets[cite: 3].
* **Rapid PVST+ (Spanning Tree Protocol):** Aligned with HSRP active roles to guarantee symmetric layer 2 forwarding paths and eliminate loops[cite: 3]:
  * **Multilayer Switch-1:** Primary Root Bridge & Active Gateway for **VLAN 20** and **VLAN 30**; Secondary Root Bridge & Standby Gateway for **VLAN 50**[cite: 3].
  * **Multilayer Switch0:** Primary Root Bridge & Active Gateway for **VLAN 50**; Secondary Root Bridge & Standby Gateway for **VLAN 20** and **VLAN 30**[cite: 3].

### 2. Routing & Switching Mechanics
* **Inter-VLAN Routing:** Managed directly on the Core Multilayer Switches via Switch Virtual Interfaces (SVIs)[cite: 3].
* **Dynamic Routing:** OSPF (Open Shortest Path First) runs between edge routers (`Router0`, `Router1`) and core multilayer switches to handle upstream path selection[cite: 3].

---

## VLAN & Subnet Mapping

| VLAN ID | Subnet / Segment | Designated Role / Access Switch | Active Gateway | Standby Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **VLAN 20** | `192.168.2.0/24` | Accounting (`SW-2`) | `Multilayer Switch-1` | `Multilayer Switch0` |
| **VLAN 30** | `192.168.3.0/24` | Human Resources (`SW-2`) | `Multilayer Switch-1` | `Multilayer Switch0` |
| **VLAN 50** | `192.168.4.0/24` | Information Technology (`SW-3`) | `Multilayer Switch0` | `Multilayer Switch-1` |

---

## Link addressing Summary

* **Point-to-Point Link 1 (`Router0` $\leftrightarrow$ `Multilayer Switch-1`):** `10.1.1.0/30`[cite: 3]
  * `Router0`: `10.1.1.1`[cite: 3]
  * `Multilayer Switch-1`: `10.1.1.2`[cite: 3]
* **Point-to-Point Link 2 (`Router1` $\leftrightarrow$ `Multilayer Switch0`):** `10.1.2.0/30`[cite: 3]
  * `Router1`: `10.1.2.1`[cite: 3]
  * `Multilayer Switch0`: `10.1.2.2`[cite: 3]
