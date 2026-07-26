# Implementing Enterprise Network Segmentation (VLANs), ACLs, NAT/PAT, IPsec VPN, and OSPF using Cisco Packet Tracer

## 📌 Overview

This project demonstrates the design and implementation of a segmented enterprise network optimized for high-security environments. It showcases a transition from a vulnerable, flat network architecture to a Role-Based Access Control (RBAC) architecture. By utilizing Virtual Local Area Networks (VLANs), Inter-VLAN routing (Router-on-a-Stick), and Access Control Lists (ACLs), the network ensures that sensitive corporate data remains strictly isolated while maintaining controlled communication lines where business operations dictate.

The network is divided into multiple departments using VLANs, with controlled communication enforced via Access Control Lists (ACLs). Inter-VLAN routing is configured using a Router-on-a-Stick approach, and dynamic IP addressing is provided through DHCP. This project reflects real-world Defense-in-Depth, least privilege, identity boundary alignment, and network segmentation strategies used in modern enterprise cybersecurity.

---

## 📡 Enterprise Multi-SSID Wireless Infrastructure Matrix

To align with your updated department mapping and extend role-based network containment across the mobility domain without deploying redundant physical hardware layers, the enterprise wireless architecture utilizes a single physical Wireless Access Point (WAP) array to broadcast three separate Service Set Identifiers (SSIDs). **Company PCs are strictly hardwired via Ethernet; Wi-Fi is reserved exclusively for smartphones and mobile endpoints.**

*   **SSID:** `Corporate-Secure`
    *   **Logical Network Bind:** VLAN 30 (IT / SOC / IAM Core), VLAN 10 (Finance), VLAN 15 (Executive Suite), and VLAN 20 (HR & Administration)
    *   **Target Scope:** Automatically maps authorized internal corporate **smartphones** to their respective departments based on their identity profiles. 
*   **SSID:** `Corporate-Guest`
    *   **Logical Network Bind:** VLAN 40 (Guest Space Tier)
    *   **Target Scope:** Provisioned exclusively for visitor smartphones and non-employee mobile infrastructure access.
*   **SSID:** `Corporate-IoT`
    *   **Logical Network Bind:** VLAN 50 (Hardened IoT & Surveillance Zone)
    *   **Target Scope:** Isolates facility smart systems, building management controllers, and wireless CCTV cameras scattered across the property.

---

## 🏢 Architectural Realities: Physical vs. Logical Deployment

### 1. The Real-Life (Physical) Architecture

In a real-world enterprise deployment, physical placement is determined by building layout, structural design, and cabling limits:

*   **Scattered Physical Footprint:** CCTV cameras, IP surveillance units, and wireless access points are scattered physically across corridors, building entrances, server rooms, and distinct floors depending on security coverage needs.
*   **Cable Consolidation Point:** Every physical device (including all corporate PCs) runs a dedicated Ethernet drop back to the nearest patch panel or local edge access switch situated in a wiring closet on that specific floor.
*   **SSID Broadcast Footprint:** Wireless access points are mounted to ceilings in structural high-points to optimize radio frequency coverage for smartphones, broadcasting multiple SSIDs (`Corporate-Secure`, `Corporate-Guest`, `Corporate-IoT`) from a single hardware chassis.
*   **Datacenter Infrastructure Anchor:** Critical assets like the Next-Gen Firewall (NGFW), core switches, Active Directory domain controllers, corporate servers, and rack-mounted UPS power frameworks are grouped physically inside a secure, centralized server room rack framework.

### 2. The Cisco Packet Tracer (Logical) Architecture

Inside Cisco Packet Tracer, the layout is organized purely by network security zones, administrative boundaries, and logical data flow containment:

*   **Centralized Visual Grouping:** Scattered physical assets are grouped together visually inside a single colored workspace container to visually demonstrate administrative alignment to the security perimeter policy.
*   **Interface Trunk Aggregation:** Hardware access points do not use separate physical lines for every wireless group. Instead, a single physical interface link is configured as an **802.1Q Trunk Link** (e.g., `Fa0/6`) to multiplex traffic from the secure, guest, and IoT wireless tiers back to the Core Switch framework.
*   **Boundary Enforcement:** Firewalls, Edge Routers, and Layer 2/3 Switch boundaries are drawn to map **East-West lateral movement controls** via stateless Extended Access Control Lists (ACLs) applied directly to subinterfaces.

---

## 🗺️ Logical Architecture Blueprint

```text
                                     [ The Internet / WAN Cloud ]
                                                  |
                                     [ Next-Gen Firewall (NGFW) ]
                                     (Perimeter Stateful Defense)
                                                  |
                                 [ Edge Router / Firewall (2911) ]
                                                |
                                                | g0/0 (802.1Q Trunk Link)
                                                |
                                      [ Core Switch (2960) ]
              __________________________________|__________________________________
             |                                  |                                  |
        [ Trunk / VTP ]                      [ Fa0/3 ]                          [ Fa0/4 ]
             |                                  |                                  |
 ==========🔴 THE RED ZONE ==========   ===============🔵 BLUE ZONE ============ ============🟢 GREEN ZONE ============
 |  (High-Privilege Security Policy) |   |  VLAN 20: HR & Administration   | |  VLAN 30: IT / SOC / IAM        |
 |                                   |   |  Subnet: 192.168.20.0/24        | |  Subnet: 192.168.30.0/24        |
 |  Executive Suite [3rd Floor]      |   |                                 | |                                 |
 |  VLAN 15                          |   |  [HR_PC]         [HR_Server]    | |  [IT_PC]        [AD_DomainCtrl] |
 |  Subnet: 192.168.15.0/24          |   |  (Wired Ethernet)(192.168.20.50)| |  (Wired Ethernet)(192.168.30.100)|
 |  - CEO/COO/CFO PCs (Wired)        |   |                                 | |                                 |
 |  - Exec Smartphones (Wi-Fi)       |   |  [HR_Phone]      [HR_FileServer]| |  [IT_Phone]     [Log_Server]    |
 |        \                          |   |  (Wi-Fi)         (192.168.20.60)| |  (Wi-Fi)        (192.168.30.200)|
 |         \                         |   |        |                ^       | |        |                ^       |
 |          v                        |   |        v                |       | |        v                |       |
 |  Finance [2nd Floor: Finance Dept]|   (Allowed) --------->      |       | |    (Allowed) ---------> |       |
 |  VLAN 10                          |   =================================== |                     |       |
 |  Subnet: 192.168.10.0/24          |            |                ^         |                     |       |
 |  - [Finance_PC] (Wired Ethernet)  |            |                |         ===================================
 |  - [Fin_Phone] (Wi-Fi Smartphone) |            |                X (Blocked via ACL)                 ^
 |  - [Fin_FileShare](192.168.10.60) |            |                v                                   |
 |        |                |         |       (Blocked via ACL) ----------------------------------------|
 |        v                v         |             |
 |   (Allowed) ----> [Shared_Fin_Srv]|             |
 |                    (10.50)        |             v
 =====================================             
               |                 ^                 
               |                 |                 
          (Blocked via ACL) -----X------------------|---------------|---------------------------------------
               |                                    |
               v                                    v
        =====================================🟡 YELLOW ZONE =====================================
        |  VLAN 40: Guest Space (Wired & Mobility Tier)                                         |
        |  Subnet: 192.168.40.0/24                                                              |
        |                                                                                       |
        |  [Guest Kiosk PC] (Wired Fa0/5) --\                                                   |
        |                                     +--> [VLAN 40 Gateway] -> X (Implicitly Dropped via ACL) |
        |  [Guest SmartPhones] (Wi-Fi) -----/                                                   |
        |  - Connected via Corporate-Guest SSID Mobility Array                                  |
        =========================================================================================
        
        =====================================🟣 PURPLE ZONE =====================================
        |  VLAN 50: Hardened IoT & Perimeter Surveillance Zone                                  |
        |  Subnet: 192.168.50.0/24                                                              |
        |                                                                                       |
        |  [Wired Network Infrastructure Anchor]                                                |
        |   |-- [Office_MFP_Printer_1] ---- (Static IP: 192.168.50.20 on Switch Port Fa0/10)    |
        |   |-- [Physical_CCTV_NVR] ------- (Static IP: 192.168.50.25 on Switch Port Fa0/11)    |
        |   `-- [IP_Surveillance_Cam_1] --- (Static IP: 192.168.50.11 on Switch Port Fa0/12)    |
        |                                                                                       |
        |  [Corporate-IoT SSID Wi-Fi Broadcast Matrix]                                          |
        |   |-- [Boardroom_SmartTV] ------- (Static IP: 192.168.50.30 via WAP Client Link)       |
        |   |-- [Smart_Thermostat_Node] --- (DHCP Pool Assigned via WAP Client Link)             |
        |   `-- [Wireless_CCTV_Camera_2] -- (Static IP: 192.168.50.12 via WAP Client Link)       |
        |                                                                                       |
        |  --> X (Unsolicited Outbound Communications Blocked via Edge Router Gateway ACL)      |
        =========================================================================================

        =====================================🟤 OOB MANAGEMENT ZONE =============================
        |  VLAN 99: Out-of-Band Management (Control Plane Isolation)                            |
        |  Subnet: 192.168.99.0/24                                                              |
        |                                                                                       |
        |  [Network Admin PC] (Wired: 192.168.99.100) ----> [Switch SVIs & Router VTY Lines]    |
        |                                                    (Only allowed host via Access-Class)|
        =========================================================================================

        =====================================🔒 HARDENED DMZ SERVER FARM =======================
        |  VLAN 100: Hardened DMZ Server Farm (Public-Facing Isolation Tier)                    |
        |  Subnet: 192.168.100.0/24                                                             |
        |                                                                                       |
        |  [App Server]     [Mail Server]     [Web Server]      [SFTP Server]                   |
        |  (192.168.100.10) (192.168.100.20)  (192.168.100.30)  (192.168.100.40)                |
        |                                                                                       |
        |  --> (Isolated from internal networks; traffic inspected statefully via NGFW perimeter)|
        =========================================================================================

        =====================================⚡ HARDWARE RESILIENCE LAYER =======================
        |                                                                                       |
        |  [Rack-Mounted UPS (Uninterruptible Power Supply)]                                    |
        |  --> Provides clean power conditioning, baseline surge protection, and power backup.  |
        =========================================================================================

```

## 🎯 Perimeter vs. Internal Boundary Separation

With the physical network topology upgraded to include an edge security appliance labeled NGFW, the network implements a clear defense-in-depth model:
* **Active Internal Enforcement (Cisco Router ACLs):** All inter-VLAN, role-based blocking rules (East-West traffic) are configured on the 2911 Edge Router via Extended Access Control Lists applied explicitly to logical subinterfaces. This ensures local containment so unprivileged internal subnets cannot reach restricted databases, identity directories, or backend storage segments.
* **Perimeter Inspection Layer (NGFW Hardware Placement):** The dedicated edge security appliance is structurally placed at the true internet boundary. This layer is strategically positioned to handle high-compute Layer 7 protection (Application Control, URL Threat Intelligence, and Intrusion Prevention) for all traffic exiting the internal corporate subnets out to the wide-area network (North-South traffic).

---

## 🎛️ Physical Server Room & Rack Architecture Mapping

The section below maps the logical topology directly onto physical corporate infrastructure units housed within the IT Operations room datacenter frame, visualizing the containment boundaries and edge endpoints:

* **Edge Transit Tier:** The Core Router (2911) hosts the public WAN interface (`g0/1`: `203.0.113.2`) and terminates a hardware-accelerated `Tun0` secure IPsec VPN tunnel back to the Cape Town Remote Branch (`10.255.255.1`).
* **Logical Trunking Aggregation:** A Layer 2/3 Core Switch distributes 802.1Q tagged configurations down through dedicated access links to physical server blades, utilizing an 802.1Q Trunk Link interface on `Fa0/6` to aggregate multi-SSID corporate wireless arrays (`Corporate-Secure`, `Corporate-Guest`, `Corporate-IoT`).
* **Segregated Compute Zone Assets:**
  * 🔴 **Finance Production Vault:** Hosts the Finance Server (`192.168.10.50`) and the centralized Finance File Share (`192.168.10.60`) handling general ledgers. Finance PCs are strictly hardwired; supports Finance staff smartphones via the Corporate-Secure mobility framework.
  * 🔴 **Executive Suite Repository (Admin):** Hosts management communication assets for the CEO, COO, and CFO within VLAN 15. Executive PCs are strictly hardwired; supports C-level executive smartphones via the Corporate-Secure mobility framework.
  * 🔵 **HR Administration Repository:** Hosts the HR Database Server (`192.168.20.50`) and the HR File Server (`192.168.20.60`) containing employee records. HR PCs are strictly hardwired; supports HR staff smartphones via the Corporate-Secure mobility framework.
  * 🟢 **Core Directory & SOC Hub:** Hosts the Active Directory Domain Controller (`192.168.30.100`), Web Server (`192.168.30.50`), and the central Log / SIEM Server (`192.168.30.200`). Serves as the identity engine validating wireless enterprise client authentications anchored to the Corporate-Secure mobility framework. IT PCs are strictly hardwired.
  * 🟡 **Guest Access & Mobility Gateway:** Anchored cleanly to VLAN 40 to completely drop unauthorized traffic before it leaves the rack plane. This handles both the physical field-drop interface and the local hardware Wireless Access Point (AP) broadcasting the `Corporate-Guest` SSID network framework for guest smartphones.
  * 🟣 **IoT & Printer Infrastructure Anchor:** Houses high-risk network assets, managing static endpoints including the Corporate Multi-Function Printer (`192.168.50.20`) connected via physical switch port `Fa0/10` and Smart TV nodes (`192.168.50.30`) isolated via the Corporate-IoT SSID broadcast matrix.
  * 🟤 **Out-of-Band Management (OOBM) Shield:** Enforces complete control plane isolation via VLAN 99, providing a dedicated interface infrastructure path restricted strictly to management operations.
  * 🔒 **Hardened DMZ Production Segment:** Hosts public-facing corporate infrastructure elements within VLAN 100, isolated fully from trusted user tiers to terminate exterior requests safely.
* **⚡ High-Availability Power Layer:** A dedicated, rack-mounted UPS (Uninterruptible Power Supply) backup system is installed at the framework foundation, ensuring continuous runtime, clean power conditioning, and operational resilience for the core security infrastructure during local power fluctuations or load-shedding events.
* **Vulnerability Management Baseline Enforcement:** 100% of unused physical switch ports and interface slots are administratively shut down (`shutdown`) to mitigate rogue network access vectors or physical bypass attacks.

---

## 🏢 Network Scenario & Addressing

A corporate office requires an internal network restructure to secure its operational workflows. The environment hosts eight distinct subnets, each mapped to a specific corporate function and data tier. The security policy mandates granular boundary protections to prevent unauthorized internal communication, focusing heavily on lateral movement reduction.

### VLAN & Access Policy Table

| VLAN ID | Department | Gateway IP | Subnet Mask | Access Policy | Plain-English Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **VLAN 10** | Finance | `192.168.10.1` | `255.255.255.0` | Secure financial data & file storage access. | Financial operations must be heavily guarded. Restricts incoming untrusted corporate segments while allowing verified business traffic to touch servers and file shares. PCs are hardwired; runs on Corporate-Secure for smartphones. |
| **VLAN 15** | Executive Suite | `192.168.15.1` | `255.255.255.0` | Full Server Access / Workstation Isolation. | Houses C-level executives (CEO, COO, CFO) on the 3rd floor. Granted explicit routing access to the Finance Server for strategic oversight, but logically isolated from local accounting endpoints. PCs are hardwired; runs on Corporate-Secure for smartphones. |
| **VLAN 20** | HR & Administration | `192.168.20.1` | `255.255.255.0` | Access Finance, blocked from IT. | Handles general corporate administration, payroll, and benefits. Requires clear tracking lines to the central Finance Server and local HR File shares, but core IT infrastructure subnets remain off-limits. PCs are hardwired; runs on Corporate-Secure for smartphones. |
| **VLAN 30** | IT / SOC / IAM | `192.168.30.1` | `255.255.255.0` | Full access (monitoring/privileged identity control). | IT maintains all production environments and manages the central Active Directory Domain Controller (`.100`) for IAM. Full visibility is required to troubleshoot, audit, and secure the network. PCs are hardwired; runs on Corporate-Secure for smartphones. |
| **VLAN 40** | Guest Space | `192.168.40.1` | `255.255.255.0` | External access only (fully restricted). | Consultants, interns, and visitor smartphones via Corporate-Guest receive basic internet connectivity. They are entirely blind to internal company infrastructure to protect corporate intellectual property. |
| **VLAN 50** | IoT & Printer Zone | `192.168.50.1` | `255.255.255.0` | Periphery Containment & Zero-Trust Print Spooling. | Traps unhardened smart infrastructure devices, Network Multi-Function Printers (MFPs), and facility CCTV networks via Corporate-IoT. Permitted to accept inbound print jobs and NVR traffic, but strictly blocked from initiating outbound connections. |
| **VLAN 99** | Out-of-Band Mgmt | `192.168.99.1` | `255.255.255.0` | Infrastructure Shield. | OOBM Layer: Isolates network management control elements and Switch SVIs. Completely blocks non-admin segments from interacting with administrative infrastructure. |
| **VLAN 100** | Secure Server Farm | `192.168.100.1` | `255.255.255.0` | DMZ Data Tier Isolation. | DMZ Layer: Moves critical production application servers out of standard client domains into a dedicated, hardened repository zone. |

---

## 🖥️ Centralized Infrastructure Layout

To maximize enterprise accuracy, our datacenter zone maps dedicated functional systems to mirror real production environments:
* **Active Directory Domain Controller (AD-DC):** `192.168.30.100` (VLAN 30) – Enforces enterprise Identity and Access Management (IAM), kerberos ticket verification, and central workstation user policies.
* **Finance Production Server:** `192.168.10.50` (VLAN 10) – Hosts core ledger, invoice processing, and financial accounting applications.
* **Finance File Share Server:** `192.168.10.60` (VLAN 10) – Secure localized repository hosting department financial records and spreadsheets.
* **HR Server:** `192.168.20.50` (VLAN 20) – Stores administrative records and employee management databases.
* **HR Department File Server:** `192.168.20.60` (VLAN 20) – Houses internal contracts, onboarding templates, and benefit records.
* **Web Server:** `192.168.30.50` (VLAN 30) – Disseminates internal corporate tools and internal web applications.
* **Logging / SOC SIEM Server:** `192.168.30.200` (VLAN 30) – Collects system logs and monitors simulated device telemetry.
* **Network Multi-Function Printer (MFP):** `192.168.50.20` (VLAN 50) – Static network printer device handling corporate print queues under rigid outbound communication containment.
* **Physical CCTV Network Video Recorder (NVR):** `192.168.50.25` (VLAN 50) – Secure internal node managing surveillance feeds mapped strictly within the IoT architecture.
* **DMZ Core Application Server:** `192.168.100.10` (VLAN 100) – Runs public web application components under stateful perimeter supervision.
* **DMZ Corporate Mail Server:** `192.168.100.20` (VLAN 100) – Directs inbound/outbound external corporate mail routing.
* **DMZ Public Web Server:** `192.168.100.30` (VLAN 100) – Hosts the primary external storefront and corporate web assets.
* **DMZ Hardened SFTP Server:** `192.168.100.40` (VLAN 100) – Validates encrypted external client file transfers.

---

## 🛡️ Firewall & Perimeter Defense Layer

* **Stateful Inspection vs. Stateless ACLs:** Unlike standard stateless ACL router controls that filter blindly on individual packet headers, the perimeter firewall enforces stateful inspection policies. It tracks active TCP connection handshakes originating from high-privilege corporate workstations (Exec Suites, Finance) out toward external web entities, ensuring returning traffic is strictly validated and linked to a verified, established internal session.
* **Application-Layer Visibility (Layer 7 Defense):** The perimeter layer leverages deep packet inspection (DPI) to stop protocol-abuse attacks. If an asset inside the Executive Suite or HR network attempts to tunnel unapproved traffic or run malicious software over standard web ports (such as masking data exfiltration over Port 80 or 443), the firewall's application identification capabilities flag and neutralize the session immediately.
* **Integrated Intrusion Prevention Systems (IPS):** The firewall runs dynamic signature matching engines to detect active exploitation attempts, software vulnerabilities, or network-layer scanning sequences targeting the internal corporate environment, generating telemetry drops directly to the security operations center (SOC) log collector.

---

## ⚙️ Step-by-Step Configuration Guide

### Step 1 – Create and Name VLANs on the Switch

Initialize the broadcast domains on the Layer 2 switch and associate active access interfaces with their designated departments.

```text
Switch> enable
Switch# configure terminal

! Initialize Corporate VLAN Databases
Switch(config)# vlan 10
Switch(config-vlan)# name Finance
...
Switch(config-if)# exit
```

### Step 2 – Configure Trunk Ports to Router and Access Point

Establish a persistent 802.1Q trunk uplink interface to carry multiplexed multi-VLAN traffic between the core switch, the edge router, and the multi-SSID wireless access point array.

```text
! Trunk to Core Router
Switch(config)# interface fa0/24
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,15,20,30,40,50,99,100
Switch(config-if)# exit

! Trunk to Wireless Access Point
Switch(config)# interface fa0/6
Switch(config-if)# description Trunk Link to Corporate Wireless Access Point
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,15,20,30,40,50
Switch(config-if)# exit
```

### Step 3 – Configure Router-on-a-Stick (Logical Subinterfaces)

Create logical subinterfaces on the router's physical interface.

```text
Router> enable
Router# configure terminal

Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit

Router(config)# interface g0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
...
Router(config-subif)# exit
```

### Step 4 – Configure Centralized DHCP Scopes

Automate IP address assignment using DHCP.

```text
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.99
...
Router(config)# ip dhcp pool Finance_Pool
...
Router(dhcp-config)# exit
```

---

## 🔄 The Automated Handshake: How Devices Get an IP (D.O.R.A.)

When an unconfigured asset attaches to an access port or connects to a wireless SSID, it follows the standard DHCP DORA process:

- **Discover** – Client broadcasts for a DHCP server.
- **Offer** – Router offers an available address.
- **Request** – Client requests the offered lease.
- **Acknowledge** – Router confirms the lease.

### Step 5 – Configure Access Control Lists (Core Security Optimization)

Extended ACLs enforce inter-VLAN security policies.

```text
! ====================================================================
! 1. DEFINE ACCESS CONTROL LISTS
! ====================================================================

Router(config)# ip access-list extended ADMIN_INBOUND_ACL
...
Router(config)# interface g0/0.100
Router(config-subif)# ip access-group DMZ_INBOUND_ACL in
Router(config-subif)# exit
```

---

## 🧪 Verification & Testing Validation

### Automated Test Cases Matrix

| Test Case ID | Traffic Source Host | Destination Target | Expected Behaviour | Status |
|--------------|---------------------|--------------------|--------------------|--------|
| TC-01a | Guest Kiosk PC | Finance/Admin PC | Blocked | ✅ |
| ... | ... | ... | ... | ... |

---

## ⚙️ Core Skills Demonstrated

- VLAN Segmentation & Broadcast Domain Isolation
- Inter-VLAN Routing (Router-on-a-Stick)
- Access Control Lists (ACLs)
- DHCP Configuration
- RBAC
- Network Troubleshooting

---

## 🛡️ Advanced Engineering Defense Strategies

...

---

## 🔐 Security Implementation Summary

...

---

## 📊 Results Summary

...

---

## 🧾 Conclusion

...

---

## 🏆 Career Relevance Mapping

...

---

## 🏁 Project Status

- ✅ Lab State: COMPLETED
- ✅ Testing Coverage: 100% SUCCESSFUL
- ✅ Policy Verification: VALIDATED & LOCKED

---

## 🔖 Project Hashtags

`#CyberSecurity` `#SOC` `#IAM` `#Networking` `#VLAN` `#ACL` `#CiscoPacketTracer` `#ITSecurity` `#EthicalHacking` `#NetworkSecurity` `#PortfolioProject`







