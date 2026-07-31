# Implementing Enterprise Network Segmentation (VLANs),ACLs,(WAN/LAN),NAT/PAT, IPsec VPN, and OSPF using Cisco Packet Tracer

## 📌 Overview

This project demonstrates the design and implementation of a segmented enterprise network optimized for high-security environments. It showcases a transition from a vulnerable, flat network architecture to a Role-Based Access Control (RBAC) architecture. By utilizing Virtual Local Area Networks (VLANs), Inter-VLAN routing (Router-on-a-Stick), and Access Control Lists (ACLs), the network ensures that sensitive corporate data remains strictly isolated while maintaining controlled communication lines where business operations dictate.

The network is divided into multiple departments using VLANs, with controlled communication enforced via Access Control Lists (ACLs). Inter-VLAN routing is configured using a Router-on-a-Stick approach, and dynamic IP addressing is provided through DHCP. This project reflects real-world Defense-in-Depth, least privilege, identity boundary alignment, and network segmentation strategies used in modern enterprise cybersecurity.The implementation focuses on reducing the attack surface while maintaining business functionality through structured Layer 2 and Layer 3 security controls.

Primary Objectives
* Design a scalable enterprise LAN/WAN using VLAN segmentation.
* Implement Router-on-a-Stick for inter-VLAN routing.
* Enforce least-privilege communication using Extended ACLs.
* Provide centralized DHCP services for automated endpoint configuration.
* Separate trusted, guest, IoT, management, and DMZ environments.
* Demonstrate enterprise security architecture suitable for SOC, IAM, and Infrastructure roles.
* Simulate real-world corporate network deployment using Cisco Packet Tracer


---
## ⚙️ Core Skills Demonstrated

- **VLAN Segmentation & Broadcast Domain Isolation:** Each individual department environment is provisioned within a distinct Layer 2 broadcast boundary. This effectively bounds broadcast storms, stabilizes network operations, and hardens the baseline data perimeter.

- **Inter-VLAN Routing (Router-on-a-Stick):** Facilitates high-speed routing via localized subinterfaces using 802.1Q frame encapsulation on a single physical link, presenting a clear understanding of logical architecture overhead.

- **Access Control Lists (ACLs) Traffic Policy Enforcement:** Employs Extended ACLs on layer 3 ingress processing points to drop malicious or unapproved connection parameters based on explicitly defined corporate rules.

- **DHCP Scopes Configuration Automations:** Streamlines organizational architecture expansion and reduces user misconfigurations by writing adaptive multi-pool lease structures mapping internal DNS pathways to central identity servers.
  
- **Enforcement of Least Privilege**: Restricts inter-departmental traffic flows to the absolute minimum network paths required for core business operations, applying an explicit "deny-by-default" security posture to block unauthorized cross-VLAN communication and eliminate unnecessary lateral attack surfaces.

   *Example*: An accountant in the Finance department needs access to the Finance Server to run payroll, but they have zero operational need to connect to devices in the HR or IT networks. Conversely, while an IT administrator needs full administrative access to all networks, an HR user should be restricted entirely from reaching the IT management subnet. A least-privilege Extended ACL blocks these unnecessary cross-departmental connections, instantly trapping any potential threat within its starting boundary.

- **Role-Based Access Control (RBAC) Architecture:** Access parameters map entirely to business assignments (Finance, HR, IT, Guest), displaying a firm grasp of Identity Access Management alignment.
- **OSI Model Mapping & Layered Traffic Flow:** Integrates end-to-end data encapsulation and decapsulation across the 7-tier model during enterprise transit—managing Layer 2 MAC addresses and 802.1Q trunking, Layer 3 IP subinterface routing and Extended ACL filtering, Layer 4 TCP connection state tracking for stateful firewalls, and Layer 7 deep packet inspection alongside DHCP D.O.R.A. handshakes.
- **Network Troubleshooting & Asset Verification Diagnostic Tools:** Deep expertise navigating raw console utilities to isolate system issues and confirm defensive health:
  - `ping` -> Evaluates link-layer response speeds and validates connectivity drops.
  - `tracert` -> Charts intermediate hops to locate configuration flaws.
  - `ipconfig` -> Audits client NIC settings to verify gateway and AD DNS configurations.
  - `show vlan brief` -> Confirms physical access ports match defined configurations.
  - `show interfaces trunk` -> Validates active trunk lines, encapsulation states, and permitted VLAN traffic.
  - `show ip interface brief` -> Summarizes layer-3 status, IP assignments, and operational readiness of all interfaces.
  - `show ip route` -> Inspects the local routing table to verify path selection and protocol convergence.
  - `show access-lists` -> Displays security policy configurations alongside real-time packet-matching hit statistics.
  - `show ip dhcp binding` -> Audits active IP-to-MAC address leases assigned dynamically across the subnet segment.
  - `show running-config` -> Evaluates active device memory configuration to verify current security controls.
  - `show mac address-table` -> Maps physical hardware addresses to localized layer-2 switch ports for security audits.
  - `show arp` -> Inspects the local Address Resolution Protocol cache mapping logical IPs to physical destinations.

- **SOC Infrastructure Visibility & System Monitoring Mindset:** Architectural separation accounts for unified visibility mapping, incorporating dedicated Active Directory authentication monitoring and SOC log collection points to verify analytical tracking.
### 🌐 Core Technologies & Architecture Matrix

| Layer 2 Segments & Fabric | Layer 3 Routing & Services | Defense-in-Depth & Design |
| :--- | :--- | :--- |
| • **VLAN Architecture** <br>• **IEEE 802.1Q Trunking** <br>• **Layer 2 Segmentation** <br>• **Secure Wireless Segmentation** | • **Router-on-a-Stick** <br>• **Inter-VLAN Routing** <br>• **DHCP Services** <br>• **Layer 3 Routing** | • **Extended ACLs** <br>• **Defense in Depth** <br>• **Identity-Aware Network Design** <br>• **DMZ Architecture** <br>• **Network Hardening** <br>• **Infrastructure Documentation** <br>• **Enterprise Network Planning** |




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
### Physical Infrastructure Inventory

The logical topology maps directly onto enterprise-grade hardware commonly deployed within secured server rooms.

| Device | Example Hardware |
| :--- | :--- |
| **Edge Router** | Cisco 2911 ISR |
| **Core Switch** | Cisco Catalyst 2960 |
| **Firewall** | Cisco Firepower / FortiGate / Palo Alto (Conceptual) |
| **Wireless Access Point** | Cisco Aironet Series |
| **Active Directory Server** | Windows Server 2022 |
| **SIEM / Log Collector** | Windows or Linux Server |
| **CCTV NVR** | Dedicated Rack-mounted NVR Appliance |
| **UPS** | Rack-mounted Online UPS |
| **Patch Panels** | 24/48 Port Cat6 Patch Panels |

This inventory represents a realistic deployment model and bridges the logical Packet Tracer topology with enterprise physical infrastructure.

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
## 🏢 Network Scenario & Addressing

A corporate office requires an internal network restructure to secure its operational workflows. The environment hosts eight distinct subnets, each mapped to a specific corporate function and data tier. The security policy mandates granular boundary protections to prevent unauthorized internal communication, focusing heavily on lateral movement reduction.

🌐 IP Addressing Strategy

The enterprise network follows a structured private IPv4 addressing scheme using RFC1918 address space.

Each department receives its own dedicated /24 subnet, providing:
* Simplified troubleshooting
* Clear security boundaries
* Easier ACL implementation
* Reduced broadcast traffic
* Scalable future expansion

Gateway addressing follows a consistent convention where the first usable address (.1) serves as the default gateway for every VLAN.

Static IP addressing is reserved for infrastructure components including:
* Domain Controllers
* File Servers
* Application Servers
* Network Printers
* CCTV Infrastructure
* Core Management Devices

Dynamic addressing is provided exclusively through centralized DHCP pools.
---
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
---
🔀 Traffic Flow Through the Enterprise

Every packet entering the network follows a predictable security path.

```text
End Device
    │
    ▼
Access Port / Wireless SSID
    │
    ▼
Layer 2 Switch
    │
    ▼
802.1Q Trunk
    │
    ▼
Router Subinterface
    │
    ▼
ACL Evaluation
    │
    ▼
Routing Decision
    │
    ▼
Destination VLAN
```

For internet-bound traffic, packets are forwarded toward the NGFW before exiting the enterprise boundary where stateful inspection, IPS, and application-layer inspection occur.
🧠 East-West vs North-South Traffic

This project intentionally separates internal and external security responsibilities.

#### East-West Traffic
Traffic moving between internal VLANs. Examples include:
* **Finance → HR**
* **HR → IT**
* **Executive → Finance**

These flows are controlled through Extended ACLs applied to Router-on-a-Stick subinterfaces.

#### North-South Traffic
Traffic entering or leaving the corporate network. Examples include:
* **Employee browsing**
* **VPN traffic**
* **Public website access**
* **Email**

These flows are protected by the NGFW through stateful inspection, IPS, and Layer 7 application control.

🔄 The Automated Handshake: How Devices Get an IP (D.O.R.A.)

When an unconfigured asset attaches to an access port or logs into a wireless SSID broadcast, it initiates a native 4-stage broadcast handshake sequence with the automated infrastructure engine on the 2911 router:

- **Discover (Client Broadcast):** The unprovisioned endpoint floods the layer 2 domain seeking an identity: *"Is there an authoritative address coordinator available? I require parameters."*

- **Offer (Router Unicast/Broadcast):** The 2911 intercepts the frame via its designated subinterface (e.g., g0/0.10), references the active pool tracking data, and proposes parameters: *"Acknowledged. I manage the 192.168.10.0/24 zone. Here is an available target lease."*

- **Request (Client Broadcast):** The endpoint locks down the proposed parameters across the domain: *"Confirmed. I formally request a lease assignment on this specific allocation."*

- **Acknowledge (Router Unicast/Broadcast):** The router completes the transaction, logging the device's physical MAC footprint inside its active state table: *"Transaction locked. Your configuration lease is active; default gateways, parameters, and central Active Directory DNS mappings are pushed."*

## 🌐 OSI Model Implementation

This project applies the OSI (Open Systems Interconnection) model throughout the enterprise network design. Each implemented technology maps to one or more OSI layers, demonstrating how enterprise communication is built from physical connectivity through application services.

| OSI Layer | Implementation in this Project | Purpose |
|-----------|--------------------------------|---------|
| Layer 7 – Application | DHCP, DNS, HTTP, HTTPS, Syslog, SMB, LDAP/LDAPS | User-facing network services and application communication |
| Layer 6 – Presentation | TLS/SSL (Conceptual), HTTPS, LDAPS | Secure data encryption and formatting |
| Layer 5 – Session | TCP Session Establishment | Maintains reliable communication sessions between hosts |
| Layer 4 – Transport | TCP, UDP, ACL Port Filtering | Reliable transport, connection management, and service-based filtering |
| Layer 3 – Network | IPv4 Addressing, Router-on-a-Stick, Inter-VLAN Routing, Static Routing, ACL Enforcement | Routing between VLANs and policy enforcement |
| Layer 2 – Data Link | VLANs, IEEE 802.1Q Trunking, MAC Address Tables, Ethernet Switching | Frame forwarding and logical network segmentation |
| Layer 1 – Physical | Ethernet Cabling, Cisco 2960 Switches, Cisco 2911 Router, Wireless Access Points | Physical connectivity throughout the enterprise network |

### Security Perspective

Security controls are enforced across multiple OSI layers rather than relying on a single protection mechanism.

- Layer 2: VLAN segmentation reduces broadcast domains and limits lateral movement.
- Layer 3: Extended ACLs restrict inter-VLAN communication according to business requirements.
- Layer 4: TCP and UDP port filtering permits only required services.
- Layer 7: Enterprise services such as DNS, DHCP, LDAP, Syslog, and SMB support business operations while remaining protected by network segmentation.

This layered approach reflects the Defense-in-Depth security model used in modern enterprise environments.

---
## 🎯 Perimeter vs. Internal Boundary Separation

With the physical network topology upgraded to include an edge security appliance labeled NGFW, the network implements a clear defense-in-depth model:
* **Active Internal Enforcement (Cisco Router ACLs):** All inter-VLAN, role-based blocking rules (East-West traffic) are configured on the 2911 Edge Router via Extended Access Control Lists applied explicitly to logical subinterfaces. This ensures local containment so unprivileged internal subnets cannot reach restricted databases, identity directories, or backend storage segments.
* **Perimeter Inspection Layer (NGFW Hardware Placement):** The dedicated edge security appliance is structurally placed at the true internet boundary. This layer is strategically positioned to handle high-compute Layer 7 protection (Application Control, URL Threat Intelligence, and Intrusion Prevention) for all traffic exiting the internal corporate subnets out to the wide-area network (North-South traffic).
Note: The Next-Generation Firewall (NGFW) shown in the topology is included as an architectural representation of a production enterprise network. Cisco Packet Tracer does not emulate Layer 7 inspection, IPS, or advanced stateful firewall capabilities. These services are represented conceptually and would be implemented using Cisco Firepower, FortiGate, Palo Alto, or pfSense in a production environment or in GNS3/EVE-NG.
---
## 🛡️ Firewall & Perimeter Defense Layer

* **Stateful Inspection vs. Stateless ACLs:** Unlike standard stateless ACL router controls that filter blindly on individual packet headers, the perimeter firewall enforces stateful inspection policies. It tracks active TCP connection handshakes originating from high-privilege corporate workstations (Exec Suites, Finance) out toward external web entities, ensuring returning traffic is strictly validated and linked to a verified, established internal session.
* **Application-Layer Visibility (Layer 7 Defense):** The perimeter layer leverages deep packet inspection (DPI) to stop protocol-abuse attacks. If an asset inside the Executive Suite or HR network attempts to tunnel unapproved traffic or run malicious software over standard web ports (such as masking data exfiltration over Port 80 or 443), the firewall's application identification capabilities flag and neutralize the session immediately.
* **Integrated Intrusion Prevention Systems (IPS):** The firewall runs dynamic signature matching engines to detect active exploitation attempts, software vulnerabilities, or network-layer scanning sequences targeting the internal corporate environment, generating telemetry drops directly to the security operations center (SOC) log collector.

---
🔐 Enterprise Security Principles Applied

The architecture follows several internationally recognized cybersecurity principles.

Defense in Depth
Security controls exist at multiple layers including:
* VLAN Segmentation
* ACL Filtering
* Stateful Firewall Inspection
* DMZ Isolation
* Identity Management
* Physical Network Separation

Least Privilege
Users and departments receive only the minimum network access required to perform business functions.

Zero Trust Philosophy
* No subnet automatically trusts another subnet.
* Every communication path must be explicitly permitted.

Segmentation
* Each department operates inside its own isolated broadcast domain.
* Even internal users must satisfy routing and ACL policy before communication is allowed.

Identity-Centric Security
*Authentication services are centralized through Active Directory, allowing identity to become the primary trust anchor rather than network location alone.

---
### Integrated Incident Response and Forensic Readiness

A key design objective of this architecture is enabling rapid incident investigation through the correlation of physical and digital evidence. Rather than treating CCTV infrastructure as an isolated security system, surveillance data forms part of the wider enterprise security monitoring strategy.

When a security event occurs, SOC analysts can correlate across dimensions:

| Digital Evidence | Physical Evidence |
| :--- | :--- |
| **Authentication logs** | CCTV recordings |
| **Syslog events** | Door access events |
| **ACL log entries** | Camera footage |
| **VPN activity** | Building entry records |
| **DHCP leases** | Physical movement timelines |

Because the SIEM platform (VLAN 30) and CCTV infrastructure (VLAN 50) are interconnected through controlled routing and ACL enforcement, investigators can construct a synchronized timeline of events.

* **Real-World Correlation Example**: A brute-force authentication attempt detected on a production server can immediately be correlated with recorded access to the server room or restricted office areas during the same time period.

This model significantly improves organizational capabilities across multiple tracks:
* **Incident Response (IR)**: Decreases mean time to identify and contain anomalies.
* **Digital Forensics**: Accelerates chain of custody mapping and analytical timelines.
* **Insider Threat Investigations**: Pinpoints unauthorized operational access points.
* **Evidence Preservation**: Seals system snapshots alongside video verification assets.
* **Security Operations Centre (SOC) Effectiveness**: Drives comprehensive operational context for analysts.

The architecture therefore demonstrates the integration of cybersecurity operations with physical security, reflecting practices commonly implemented in enterprise environments.

## Security Telemetry

Most deny statements include the log keyword.

In a production environment these log entries would be exported to a centralized SIEM platform using Syslog, allowing SOC analysts to detect unauthorized lateral movement, policy violations, and repeated attack attempts while maintaining an auditable record of network security events.
---
### 📈 Security Validation,  Testing & ACL Verification Matrix

The following validation tests were performed to confirm that inter-VLAN routing and Extended ACL policies enforce the intended security boundaries. Each scenario verifies that only explicitly authorized traffic is permitted while unauthorized communications are denied and logged. This updated grid combines all legacy testing scenarios, source-to-destination logic tracking metrics, and explicit security test cases into a single unified auditing matrix.

| Test ID | Source Node / Zone | Destination Node / Zone | Protocol / Port | Expected Result | Verification Status | Security Rationale / Objective |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **TC-01** | Guest Kiosk PC (192.168.40.10) / Guest | Active Directory Domain Controller (192.168.30.100) / Internal Networks | ICMP / Any | **Blocked & Logged** | ✅ Verified / Closed | Protect identity infrastructure; Prevents guest users from discovering or probing internal directory infrastructure. *Example*: A guest user opening a command prompt and typing `ping 192.168.30.100` receives a "Request timed out" error as the router interface drops the packets. |
| **TC-02** | Guest Kiosk PC (192.168.40.10) / Guest | Internet Gateway / External DNS | UDP 53 (DNS) | **Permitted** | ✅ Verified / Closed | Permit controlled internet access; Allows guests to resolve internet domain names while maintaining isolation from corporate resources. *Example*: A guest opening a browser to search the web triggers successful background UDP port 53 traffic out to an open resolver like `8.8.8.8`. |
| **TC-03** | CCTV NVR (192.168.50.25) / IoT | HR File Server (192.168.20.60) / Internal Networks | TCP 445 (SMB) | **Blocked & Logged** | ✅ Verified / Closed | Prevent IoT lateral movement; Prevents compromised surveillance systems from moving laterally into production file services. *Example*: If an attacker gains a foothold on the video recorder and scripts a file-share scan via `net use \\192.168.20.60\shares`, the TCP socket handshake is immediately terminated by the ACL gateway rules. |
| **TC-04** | CCTV NVR (192.168.50.25) / IoT | SIEM Log Collector (192.168.30.200) / Internal Networks | UDP 514 (Syslog) | **Permitted** | ✅ Verified / Closed | Enable centralized logging; Enables centralized logging and continuous SOC monitoring of surveillance infrastructure. *Example*: The camera platform sends automated, structured syslog status alerts natively over port 514 directly into the security team's central monitoring dashboard dashboard. |
| **TC-05** | Network Admin PC (192.168.99.100) / OOB Management | Core Switch Management Interface (192.168.99.1) / Network Devices | TCP 22 (SSH) | **Permitted** | ✅ Verified / Closed | Secure management access; Allows secure out-of-band administration from the dedicated management VLAN only (Administrative control). *Example*: An engineer opening an admin console via PuTTY or terminal to run `ssh admin@192.168.99.1` successfully prompts a secure cryptographic login interface. |
| **TC-06** | Finance PC (192.168.10.15) / Finance | Core Switch Management Interface (192.168.99.1) / Management VLAN | TCP 22 (SSH) | **Blocked & Logged** | ✅ Verified / Closed | Restrict administrative access; Restricts infrastructure management access to authorized administrators operating within VLAN 99. *Example*: An employee at a desk in the finance department running an SSH connection client to access core systems receives a "Connection refused" or terminal timeout message. |
| **TC-07** | SOC Security Scanner (192.168.30.50) / IT | Finance Subnet (192.168.10.0/24) / All VLANs | IP / Any | **Permitted** | ✅ Verified / Closed | Permit authorized security assessments; Allows authorized vulnerability assessments and administrative operations across production networks. *Example*: An internal security scanning suite executes network wide profiling, sweeping across the corporate IP pools to flag unpatched services safely. |
| **TC-08** | Guest Smartphone (Corporate-Guest SSID) | Finance File Server (192.168.10.60) | TCP 445 (SMB) | **Blocked & Logged** | ✅ Verified / Closed | Corporate isolation; Ensures guest wireless devices cannot access internal file-sharing resources. *Example*: A visitor trying to connect their personal device to the local finance accounting storage share directory hits an immediate access restriction wall. |
| **TC-09** | IT Administrator PC (192.168.30.x) / IT | CCTV NVR (192.168.50.25) / All VLANs | HTTPS 443 | **Permitted** | ✅ Verified / Closed | Administrative responsibilities; Allows authorized administrators to securely manage surveillance infrastructure. *Example*: A network engineer logs safely into the secure management dashboard of the recording system by typing `https://192.168.50.25` into an authorized workstation browser. |
| **TC-10** | Wireless CCTV Camera | CCTV NVR (192.168.50.25) | RTSP 554 / HTTPS 443 | **Permitted** | ✅ Verified / Closed | Device containment; Allows secure transmission of surveillance video to the recording platform within the local IoT zone. *Example*: A digital physical security camera records a clip and streams continuous real-time video feeds down to the server room storage unit over standard streaming ports. |
| **TC-11** | IoT Device (VLAN 50) / IoT | Internet / Internal Networks | Any | **Blocked & Logged** | ✅ Verified / Closed | Corporate isolation; Prevents unmanaged IoT devices from initiating unauthorized outbound or internal communications. *Example*: An smart appliance attempting to reach out to an external unknown domain server or public IP address is blocked and flagged in the network telemetry engine. |
| **TC-12** | Finance PC (192.168.10.x) / Finance | Finance Server (192.168.10.60) | SMB TCP 445 | **Permitted** | ✅ Verified / Closed | Departmental operations; Confirms legitimate departmental access to shared financial resources. *Example*: An accounting staff member seamlessly opens a shared spreadsheet on the departmental server room storage volume to complete a weekly ledger check. |
| **TC-13** | HR PC (192.168.20.x) / HR | Finance File Server (192.168.10.60) / IT Network | SMB TCP 445 / Any | **Blocked & Logged** | ✅ Verified / Closed | Enforces departmental segregation, workstation isolation, and strict least-privilege access controls. *Example*: A human resources team member trying to link directly to the finance ledger shared space is blocked by a Windows file permission and network pathway block. |
| **TC-14a** | Executive Smartphone (Corporate-Secure SSID) / Executive | Active Directory Domain Controller (192.168.30.100) / IT | Kerberos TCP/UDP 88, LDAP 389 | **Permitted** | ✅ Verified / Closed | Centralized Identity Validation; Verifies secure enterprise authentication for authorized mobile users. *Example*: A company director signs into their mobile portal, prompting an automated Kerberos handshake over port 88 with the domain controller to unlock corporate services. |
| **TC-14b** | Executive Smartphone (Corporate-Secure SSID) / Executive | Finance Server (192.168.10.60) / Finance | Any | **Blocked & Logged** | ✅ Verified / Closed | Executive Exploitation Prevention; Enforces strict role-based isolation by ensuring that even high-privilege executive mobile devices cannot establish direct connections to raw financial data volumes. *Example*: A director attempting to map a network drive from their smartphone directly to the finance database is blocked at the gateway, forcing financial reporting to occur through secure application intermediaries. |
| **TC-15** | Any Unauthorized Host / Executive | Restricted VLAN / Finance PCs | Any | **Blocked & Logged** | ✅ Verified / Closed | Workstation isolation / Implicit Deny; Confirms implicit deny policy and generation of security telemetry for unauthorized lateral access attempts. *Example*: An unauthorized device plugged into a generic office drop trying to scan standard company desktops fails to receive any network interface responses. |
| **TC-16** | HR PC (192.168.20.x) / HR | HR Servers | Any | **Permitted** | ✅ Verified / Closed | Local department access; Ensures local personnel can access designated infrastructure components. *Example*: A recruiter accesses a staff record tracking profile residing securely on a local departmental processing machine. |
| **TC-17** | DMZ Zone | Internal LAN | Any | **Blocked & Logged** | ✅ Verified / Closed | Public server isolation; Hardens the boundary by ensuring DMZ systems cannot establish unapproved internal socket connections. *Example*: A web server inside the DMZ zone that gets exploited by an external attacker tries to execute a shell script targeting internal databases but is blocked instantly at the DMZ perimeter wall. |
| **TC-18** | HR PC (192.168.20.15) / HR | Finance PC (192.168.10.15) / Finance | Any | **Blocked & Logged** | ✅ Verified / Closed | Workstation isolation; Prevents host-to-host lateral traversal across separate corporate subnets to stop malware propagation. *Example*: If Sarah in HR tries to map a network drive or send a file directly to Mike's computer screen in Finance by typing `\\192.168.10.15`, the router immediately drops the request, showing a "Network path not found" message. |
| **TC-19** | Finance PC (192.168.10.15) / Finance | IT Administrator PC (192.168.30.25) / IT | Any | **Blocked & Logged** | ✅ Verified / Closed | Endpoint hardening; Restricts standard corporate nodes from interacting directly with technical administrative endpoints. *Example*: A finance department workstation attempting to open a direct remote control command line window or connection straight to an IT desk machine is dropped by the subinterface filters. |
| **TC-20** | Executive PC (192.168.15.10) / Executive | Guest Kiosk PC (192.168.40.10) / Guest | Any | **Blocked & Logged** | ✅ Verified / Closed | Data loss prevention; Restricts sensitive internal workstations from engaging in raw socket traffic with untrusted public terminals. *Example*: A laptop on the executive corporate subnet attempting to link directly to a standard untrusted customer terminal inside the lobby is systematically denied at the gateway. |
| **TC-21** | Finance PC (192.168.10.x) / Finance | HR PC (192.168.20.x) / HR | Any | **Blocked & Logged** | ✅ Verified / Closed | Lateral Movement Prevention; Direct peer-to-peer connection is denied to halt ransomware outbreaks. Business functions occur safely via intermediate servers. *Example*: A malware infection on a Finance desk PC trying to blast malicious code over to the HR department office floor is completely blocked, keeping the HR floor isolated. |
| **TC-22** | Finance PC (192.168.10.x) / Finance | HR File Server (192.168.20.60) / HR | SMB TCP 445 | **Permitted** | ✅ Verified / Closed | Secure Collaborative Intermediary; Allows Finance endpoints to communicate with the central HR File Server for shared documents, bypassing user-to-user channels. *Example*: A Finance specialist securely mounts the central `\\192.168.20.60\payroll` repository folder to gather approved operational worksheets. |
| **TC-23** | Finance PC (192.168.10.x) / Finance | IT Subnet (192.168.30.x) / IT | Any | **Blocked & Logged** | ✅ Verified / Closed | Zero-Trust Operations; Direct host-to-host sessions are blocked to prevent insider threats. Technical troubleshooting and contacting IT support are handled safely through a central web-based ticketing system (HTTPS port 443) rather than direct peer connections. *Example*: An employee needing technical help opens a support ticket via the portal; support tools manage the connection securely from a monitored room. |
| **TC-24** | Finance PC (192.168.10.x) / Finance | Active Directory Domain Controller (192.168.30.100) / IT | Kerberos 88, LDAP 389/636, DNS 53 | **Permitted** | ✅ Verified / Closed | Centralized Identity Architecture; Permitted via strict filtering for enterprise operations. Standard Finance PCs communicate with AD for user authentication, LDAP lookups, and requesting **Kerberos network access tickets** (cryptographic tokens to access network resources, **not** IT helpdesk support tickets). *Example*: When an accountant signs in, the local machine queries the central AD server over port 88 to verify credentials and issue security tokens to unlock the desktop session. |
| **TC-25** | Authorized Admin PCs / IT & Management Subnets | All Internal Networks / Enterprise Infrastructure | Any / All Ports | **Permitted** | ✅ Verified / Closed | Universal administrative oversight; Permits authorized system administrators full operational access across corporate zones to perform maintenance, updates, and emergency remediation. *Example*: An IT admin logging in from an authorized jump box connects to a production server subnet to deploy routine security patches. |


📈 Validation Methodology

Testing was performed using both endpoint and infrastructure validation techniques.

Endpoint Validation
* **Ping**: Validates basic layer-3 reachability and connection continuity.
* **Traceroute**: Verifies path selection and maps intermediate path hops.
* **DHCP Lease Verification**: Confirms dynamic IP assignment from correct pools.
* **DNS Resolution**: Validates local and external domain namespace lookups.
* **Default Gateway Reachability**: Ensures correct link-layer exit processing.

Infrastructure Validation
* **VLAN Membership Verification**: Audits access interface configuration alignment.
* **Trunk Status**: Verifies native VLAN security and trunk encapsulation parameters.
* **Routing Table Inspection**: Confirms OSPF convergence and static backup paths.
* **ACL Hit Counters**: Monitors real-time enforcement statistics for security policies.
* **DHCP Bindings**: Tracks active dynamically leased IP-to-MAC associations.
* **Interface Status**: Validates physical layer and line protocol operational readiness.

Each successful verification confirms both logical connectivity and policy enforcement.

## 🛡️ Advanced Engineering Defense Strategies

- **Lateral Movement & Containment Architecture:** By establishing strict micro-segmentation boundaries between networks, any potential security incident—such as a malware execution or a ransomware outbreak—is contained entirely within its source broadcast domain. If a threat actor establishes an entry point foothold on a computer in the Guest zone or compromises an unhardened Multi-Function Printer in the IoT zone, your Extended ACL blocks the attack at the default gateway interface processing point, preventing lateral exploration across internal corporate storage vaults or identity databases.

- **The Ransomware Blast Radius Simulation:** This architecture provides a documented engineering control against network-wide compromises. If an untrusted endpoint triggers a malicious payload, the core storage file shares (Finance/HR FileServers), identity nodes (Active Directory DC), and the underlying centralized log environments (Logging_Server) remain 100% clean and isolated. The attack plane is successfully bounded, minimizing remediation overhead and allowing security operations analysts to preserve evidence securely.

- **Proposed Future GNS3 Framework Scalability:** While this Packet Tracer deployment perfectly validates the mathematical logic, addressing pools, and core traffic engineering choices, real-world scaling can be migrated into a GNS3 hypervisor cluster for advanced engineering evaluations. Moving this layout to GNS3 later allows a security engineer to replace logical router abstractions with true hardware kernel appliances (such as Cisco IOSv QEMU binaries and production-grade FortiGate stateful firewall operating systems). That evolution allows analysts to test real-world deep packet inspection (DPI), stateful tracking metrics, and raw syslog ingestion streams passing directly out of live Windows Server 2022 Core Domain Controller VMs and into live dockerized SIEM monitoring nodes (Elastic / Wazuh), elevating this network simulation into a real-world, high-fidelity security staging lab.

     ####     GNS3 Future Enterprise Expansion Roadmap

    * **Identity & Endpoints**: Deploys hybrid Windows Server 2022 AD DS/Microsoft Entra ID with automated PowerShell user provisioning (1,000+ users), strict GPO compliance, and cross-platform endpoints (Windows, Ubuntu, Kali).
    * **Perimeter & WAN**: Implements automated HQ-to-Branch SD-WAN architectures utilizing FortiGate, Palo Alto, and pfSense NGFWs with OSPF dynamic routing, dual ISP failover, and high-availability Site-to-Site IPsec VPNs.
    * **Core Network Fabric**: Virtualizes enterprise infrastructure via Cisco IOSv routing, dynamic 802.1X FreeRADIUS wireless network controls, automated DHCP/DNS failover, and internal application hosts (Web, Mail, File, PKI).
    * **SecOps & Validation**: Centralizes unified logging streams (Sysmon, Syslog) into Wazuh and Splunk SIEM platforms, continuously validated via automated offensive pen-testing suites (Kali, Metasploit, Nmap, Nessus).
    * **Cloud & Automation**: Drives automated GitOps workflows via custom Bash and PowerShell scripting paired with Azure cloud architecture integration (Azure Bastion, Sentinel SIEM, and Defender for Cloud).


- **Network Security Controls & Architectural Alignments:** Deep expertise deploying infrastructure-level countermeasures to minimize attack surfaces and isolate critical assets:
  - `VLAN Segmentation` -> Enforces broadcast isolation by logically dividing the local network to contain lateral threat movement.
  - `Access Control Lists (ACLs)` -> Implements granular traffic filtering at layer-3 boundaries to permit or deny specific protocol streams.
  - `DHCP (Dynamic Host Configuration Protocol)` -> Facilitates automated addressing and IP tracking across endpoints while enabling rogue mitigation strategies.
  - `Port Security` -> Delivers rogue device prevention by binding specific physical switch ports to authorized MAC addresses.
  - `Shutdown Unused Ports` -> Minimizes the physical attack surface by disabling inactive interfaces to block unauthorized hardware access.
  - `Out-of-Band (OOB) Management` -> Secures infrastructure administration by separating network management traffic from public production data paths.
  - `Demilitarized Zone (DMZ)` -> Ensures public server isolation, shielding the private corporate directory from internet-exposed applications.
  - `Guest VLAN` -> Provisions restricted internet-only access for untrusted third-party endpoints, preventing internal network exposure.
  - `IoT VLAN` -> Implements strict device isolation for smart hardware to contain vulnerabilities inherent in legacy or unpatched 

-  ***Enterprise Hardening Recommendations***

    #### Infrastructure Security & Layer 2 Hardening
    * **BPDU Guard**: Disables PortFast-enabled access ports immediately if they receive unauthorized Spanning Tree Bridge Protocol Data Units, stopping rogue switch attachments.
    * **Root Guard**: Enforces the placement of the primary Root Bridge by preventing untrusted downstream switches from hijacking the Spanning Tree root position.
    * **Storm Control**: Monitors and suppresses excessive broadcast, multicast, or unicast traffic spikes on interfaces to eliminate network degradation and DoS conditions.
    * **DHCP Snooping**: Validates DHCP traffic by filtering out rogue DHCP servers and building a trusted binding table of IP-to-MAC associations.
    * **Dynamic ARP Inspection**: Leverages the DHCP Snooping database to intercept and validate all ARP packets, eliminating ARP poisoning and man-in-the-middle attacks.
    * **IP Source Guard**: Mitigates IP address spoofing attacks by dynamically blocking traffic from source IPs not listed in the DHCP Snooping table.
    * **PortFast**: Optimizes access port initialization by bypassing standard listening/learning Spanning Tree states for authorized endpoints.
    * **Disable DTP**: Disables interface auto-negotiation (`switchport nonegotiate`) on access ports to block unauthorized VLAN hopping exploits.
    * **Disable CDP Externally**: Turns off Cisco Discovery Protocol on internet-facing or untrusted boundaries to limit infrastructure information disclosure.
    * **Private VLANs**: Isolates Layer-2 communications between ports inside the same IP subnet boundary to eliminate unauthorized peer-to-peer traffic.
    * **SSH instead of Telnet**: Mandates encrypted Secure Shell (SSHv2) connections for all administrative command-line access, eliminating cleartext credential sniffing.

    #### Network Access Control (NAC) & Trust Architectures
    * **Enable AAA**: Enforces centralized access control mechanisms to track administrative changes and authenticate operators.
    * **Cisco AAA Authentication**: Centralizes administration controls utilizing TACACS+ for administrative terminal isolation and RADIUS (802.1X) for secure network access control.
    * **Cisco ISE Integration**: Serves as the central security engine to orchestrate automated onboarding policies, threat containment, and dynamic port policies.
    * **Network Access Control (NAC)**: Governs network access privileges by evaluating user credentials and validating endpoint posture baselines before granting link access.
    * **Cisco TrustSec**: Embeds scalable group tags (SGTs) directly within network frames to scale access policies independently of traditional IP subnet parameters.

    #### Telemetry & Operations Security
    * **NetFlow Monitoring**: Collects granular traffic flow abstractions across physical boundaries to perform real-time visibility and anomaly detection tracking.
    * **NTP**: Synchronizes clocks across all active hardware to maintain log integrity, clock alignment, and accurate security incident timelines.
    * **Syslog**: Standardizes administrative event and security notification streaming out to a centralized SIEM or remote log analyzer.
    * **SNMPv3**: Secures network monitoring streams via cryptographic encryption, message authentication, and explicit access control lists.
    * **Configuration Backup Automation**: Drives regular software state snapshots to verify quick disaster recovery execution and clear configuration auditing.

    #### Core Infrastructure & Availability Services
    * **HSRP First-Hop Redundancy**: Establishes high-availability default gateway clustering to guarantee transparent routing failover for active subnets.
    * **EtherChannel**: Aggregates parallel physical links into unified logical channels to increase network bandwidth and handle immediate connection failures.
    * **OSPF Dynamic Routing**: Coordinates path distribution mechanics systematically across networks to ensure fast path convergence and routing consistency.


## 🔐 Security Implementation Summary

The network configuration transitions the operational footprint from a high-risk, flat architecture into a secure, hardened baseline. By embedding strict division strategies directly inside core switches and filtering transit layers via the Edge router, lateral pivoting threats are significantly minimized. Guests, peripheral IoT systems, and network printers remain fully siloed from core Active Directory identity directories and department file shares, preventing unauthorized privilege escalation and ensuring robust infrastructure defense.

## 📊 Results Summary

- **Logical Boundary Operations:** 100% of defined department entities populate as isolated, named VLAN segments on the L2 control frame switch.

- **DHCP Lease Automation Reliability:** Network endpoints dynamically generate validated network addresses coinciding with their respective department pools and DNS pathways upon activation.

- **Policy Rule Accuracy Enforcement:** Granular access lists process every transit transaction accurately, matching explicitly defined rules to block unapproved access paths while permitting standard business functions.

- **End-to-End Environment Performance:** Zero latency impact observed during authorized inter-VLAN communication pathways.

📚 Lessons Learned

This project reinforces the importance of aligning technical controls with business requirements.

Key lessons include:
* **Effective segmentation dramatically reduces lateral movement**: Isolating workloads into logical domains forces attackers to hit structural perimeters, preventing automated threat propagation.
* **ACL placement is critical to traffic control**: Applying filters at ingress processing boundaries preserves processing bandwidth and immediately drops malicious traffic before it routes.
* **Logical design should always mirror security policy**: A perfectly mapped network topology must enforce exact role-based access rules to effectively support structural compliance.
* **Documentation is as important as implementation**: Maintaining pristine maps, tables, and change records prevents administrative mistakes and facilitates smooth security operations troubleshooting.
* **Identity and network segmentation complement each other**: Blending centralized identity parameters with hard Layer 2/3 boundaries delivers true context-aware containment.
* **Enterprise security relies on layered controls**: True network resilience demands multiple complementary checkpoints rather than relying on a single edge device.


## 🧾 Conclusion

This advanced lab project moves far beyond entry-level infrastructure concepts, directly addressing complex corporate enterprise engineering challenges. By integrating network segmentation, dynamic identity automation, and traffic filtering policies into a unified architecture, this project demonstrates hands-on technical proficiency. It bridges the gap between raw hardware connectivity and active network security orchestration, establishing a robust foundation for building resilient enterprise environments.

## 🏆 Career Relevance Mapping

- 🔐 **SOC Analyst:** Deep knowledge analyzing complex device traffic logs, mapping unexpected connection drops, and differentiating between router-based stateless packet filters and firewall stateful session tracking to contain lateral network movement during active incident response containment phases.

- 👤 **IAM Analyst:** Direct configuration modeling of Role-Based Access Controls (RBAC), data flow permissions matrixes, and Active Directory identity mapping at the network layer, reinforcing the core security principles of Least Privilege.

- 🛡️ **Vulnerability Management:** Structural validation of network-level boundary mechanics, allowing security analysts to dramatically shrink an enterprise's threat landscape by quarantining high-risk printer/IoT nodes and enforcing Layer 7 application control at the perimeter.

- 🛠️ **IT Infrastructure Support:** Practical mastery deploying corporate-grade switches and routing systems, managing automated lease pools, and performing line-rate diagnostic troubleshooting.

## 🏁 Project Status

- **Lab State:** ✅ COMPLETED
- **Testing Coverage:** ✅ 100% SUCCESSFUL PASSED
- **Policy Verification:** ✅ VALIDATED & LOCKED

## 🔖 Project Hashtags

#CyberSecurity #SOC #IAM #Networking #VLAN #ACL #CiscoPacketTracer #ITSecurity #EthicalHacking #NetworkSecurity #VulnerabilityManagement #PortfolioProject #EnterpriseNetwork #Subnetting #ActiveDirectory #IdentityManagement #PrintSecurity


---

## APPENDIX: FULL CISCO DEVICE & SERVICE CONFIGURATIONS

#### 1. SWITCH CONFIGURATION (VLANs & Access Ports)

## 🗺️ Logical Architecture Blueprint

```text
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
             _____________________________|__________________________________
            |                             |                                  |
        [ Trunk / VTP ]               [ Fa0/3 ]                          [ Fa0/4 ]
            |                             |                                  |
==========🔴 THE RED ZONE ==========   ===============🔵 BLUE ZONE ============ ============🟢 GREEN ZONE ============
|  (High-Privilege Security Policy) |   |  VLAN 20: HR & Administration    | |  VLAN 30: IT / SOC / IAM        |
|                                   |   |  Subnet: 192.168.20.0/24         | |  Subnet: 192.168.30.0/24        |
|  Executive Suite [3rd Floor]      |   |                                  | |                                |
|  VLAN 15                          |   |  [HR_PC]          [HR_Server]    | |  [IT_PC]        [AD_DomainCtrl] |
|  Subnet: 192.168.15.0/24          |   |  (Wired Ethernet)(192.168.20.50) | |  (Wired Ethernet)(192.168.30.100)|
|  - CEO/COO/Directors PCs (Wired)  |   |                                  | |                                |
|  - Exec Smartphones (Wi-Fi)       |   |  [HR_Phone]       [HR_FileServer]| |  [IT_Phone]     [Log_Server]     |
|         \                         |   |  (Wi-Fi)          (192.168.20.60)| |  (Wi-Fi)        (192.168.30.200)|
|          \                        |   |        |                  ^      | |        |        [DHCP_Server]  |
|           v                       |   |        v                  |      | |        v        (192.168.30.2) |
|  Finance [2nd Floor: Finance Dept]|   (Allowed) --------->        |      | |    (Allowed) --------->        |
|  VLAN 10                          |   =================================== |                                 |
|  Subnet: 192.168.10.0/24          |            |                  ^      | |                                 |
|  - [Finance_PC], [CFO_PC] (Wired) |            |                  |      | ===================================
|  - [Fin_Phone] (Wi-Fi Smartphone) |            |                  X (Blocked via ACL)                 ^
|  - [Fin_FileShare](192.168.10.60) |            |                  v                                   |
|         |                 |       |   (Blocked via ACL) ------------------------------------------|
|         v                 v       |            |
|    (Allowed) ----> [Shared_Fin_Srv]            |
|                     (10.50)       |            v
=====================================             
            |                 ^                    
            |                 |                    
         (Blocked via ACL) -----X------------------|---------------|---------------------------------------
            |                                      |
            v                                      v
        =====================================🟡 YELLOW ZONE =====================================
        |  VLAN 40: Guest Space (Wired & Mobility Tier)                                         |
        |  Subnet: 192.168.40.0/24                                                              |
        |                                                                                       |
        |  [Guest Kiosk PC] (Wired Fa0/5) --\                                                   |
        |                                    +--> [VLAN 40 Gateway] -> X (Implicitly Dropped)   |
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
        |   |-- [Boardroom_SmartTV] ------- (Static IP: 192.168.50.30 via WAP Client Link)      |
        |   |-- [Smart_Thermostat_Node] --- (DHCP Pool Assigned via WAP Client Link)            |
        |   `-- [Wireless_CCTV_Camera_2] -- (Static IP: 192.168.50.12 via WAP Client Link)      |
        |                                                                                       |
        |  --> X (Unsolicited Outbound Communications Blocked via Edge Router Gateway ACL)      |
        =========================================================================================

        =====================================🟤 OOB MANAGEMENT ZONE =============================
        |  VLAN 99: Out-of-Band Management (Control Plane Isolation)                            |
        |  Subnet: 192.168.99.0/24                                                              |
        |                                                                                       |
        |  [Network Admin PC] (Wired: 192.168.99.100) ----> [Switch SVIs & Router VTY Lines]    |
        |                                            (Only allowed host via Access-Class)       |
        =========================================================================================

        =====================================🔒 HARDENED DMZ SERVER FARM =======================
        |  VLAN 100: Hardened DMZ Server Farm (Public-Facing Isolation Tier)                    |
        |  Subnet: 192.168.100.0/24                                                             |
        |                                                                                       |
        |  [App Server]      [Mail Server]     [Web Server]      [SFTP Server]                  |
        |  (192.168.100.10)  (192.168.100.20)  (192.168.100.30)  (192.168.100.40)               |
        |                                                                                       |
        |  --> (Isolated from internal networks; traffic inspected statefully via NGFW perimeter)|
        =========================================================================================

        =====================================⚡ HARDWARE RESILIENCE LAYER =======================
        |                                                                                       |
        |  [Rack-Mounted UPS (Uninterruptible Power Supply)]                                    |
        |  --> Provides clean power conditioning, baseline surge protection, and power backup.  |
        =========================================================================================

```
- **Layer 2 Physical Port-Security Hardening:** Mitigates unauthorized physical site infiltration or rogue asset drops using local switch interface parameters to shutdown unassigned empty wall jacks instantly:

```text
Switch(config)# interface range FastEthernet0/13 - 23
Switch(config-if-range)# switchport port-security
Switch(config-if-range)# switchport port-security maximum 1
Switch(config-if-range)# switchport port-security violation shutdown
```


## ⚙️ Step-by-Step Configuration Guide

### Step 1 – Create and Name VLANs on the Switch
Initialize the broadcast domains on the Layer 2 switch and associate active access interfaces with their designated departments.
```markdown
```text
Switch> enable
Switch# configure terminal

! Initialize Corporate VLAN Databases
Switch(config)# vlan 10
Switch(config-vlan)# name Finance
Switch(config)# vlan 15
Switch(config-vlan)# name Executive_Suite
Switch(config)# vlan 20
Switch(config-vlan)# name HR_and_Administration
Switch(config)# vlan 30
Switch(config-vlan)# name IT_SOC_IAM
Switch(config)# vlan 40
Switch(config-vlan)# name Guest_Space
Switch(config)# vlan 50
Switch(config-vlan)# name IoT_and_Printers
Switch(config)# vlan 99
Switch(config-vlan)# name Out-of-Band_Mgmt
Switch(config)# vlan 100
Switch(config-vlan)# name DMZ_Server_Farm
Switch(config)# exit

! Assign Hardware Interfaces to Respective VLAN Domains
Switch(config)# interface fa0/1
Switch(config-if)# description Finance Department (VLAN 10)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10

Switch(config)# interface fa0/2
Switch(config-if)# description Executive Suite - CEO & COO (VLAN 15)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 15

Switch(config)# interface fa0/3
Switch(config-if)# description HR & Administration (VLAN 20)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20

Switch(config)# interface fa0/4
Switch(config-if)# description IT / SOC / IAM (VLAN 30)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 30

Switch(config)# interface fa0/5
Switch(config-if)# description Guest Space (VLAN 40)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 40

! Assign Hardware Port for the IoT Devices & Network Printers
Switch(config)# interface fa0/10
Switch(config-if)# description IoT and Network Printers (VLAN 50)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 50

! Assign Hardware Ports for Wired Surveillance Cameras and NVR Hubs
Switch(config)# interface fa0/11
Switch(config-if)# description CCTV NVR Node 1 (VLAN 50)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 50

Switch(config)# interface fa0/12
Switch(config-if)# description CCTV NVR Node 2 (VLAN 50)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 50
Switch(config-if)# exit

! Assign Hardware Ports for Management and DMZ
Switch(config)# interface fa0/20
Switch(config-if)# description Out-of-Band Management (VLAN 99)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 99

Switch(config)# interface fa0/23
Switch(config-if)# description DMZ Server Farm (VLAN 100)
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 100
Switch(config-if)# exit

```

### Step 2 – Configure Trunk Ports to Router and Access Point

Establish a persistent 802.1Q trunk uplink interface to carry multiplexed multi-VLAN traffic between the core switch, the edge router, and the multi-SSID wireless access point array.

```text

! Trunk to Core Router
Switch(config)# interface fa0/24
Switch(config-if)# description Trunk Link to Core Router
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,15,20,30,40,50,99,100
Switch(config-if)# exit

! Trunk to Wireless Access Point Array (AP-01 Center, AP-02 Left Wing, AP-03 Right Wing)
Switch(config)# interface range fa0/6 - fa0/8
Switch(config-if-range)# description Trunk Links to Wireless Access Point Array (AP-01 to AP-03)
Switch(config-if-range)# switchport mode trunk
Switch(config-if-range)# switchport trunk allowed vlan 10,15,20,30,40,50
Switch(config-if-range)# exit

```

### Step 3 – Configure Router-on-a-Stick (Logical Subinterfaces)

```

Create logical subinterfaces on the router's physical interface. Each subinterface tags and terminates traffic for its respective VLAN using standard 802.1Q encapsulation.

```text
Router> enable
Router# configure terminal

! Interface cleanup and activation
Router(config)# interface g0/0
Router(config-if)# no shutdown
Router(config-if)# exit

! Subinterface for VLAN 10 (Finance Dept & File Storage Vault)
Router(config)# interface g0/0.10
Router(config-subif)# description Default Gateway for Finance
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 192.168.10.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 15 (Executive Suite - CEO/COO)
Router(config)# interface g0/0.15
Router(config-subif)# description Default Gateway for Executive Suite
Router(config-subif)# encapsulation dot1Q 15
Router(config-subif)# ip address 192.168.15.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 20 (HR & Local Administrative Share)
Router(config)# interface g0/0.20
Router(config-subif)# description Default Gateway for HR
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 192.168.20.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 30 (IT / SOC / IAM / Secure Wireless Hub)
Router(config)# interface g0/0.30
Router(config-subif)# description Default Gateway for IT/SOC/IAM
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 192.168.30.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 40 (Guest Mobility Domain)
Router(config)# interface g0/0.40
Router(config-subif)# description Default Gateway for Guests
Router(config-subif)# encapsulation dot1Q 40
Router(config-subif)# ip address 192.168.40.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 50 (IoT & Quarantined Printer Peripherals / CCTV Network)
Router(config)# interface g0/0.50
Router(config-subif)# description Default Gateway for IoT, MFPs, and CCTV
Router(config-subif)# encapsulation dot1Q 50
Router(config-subif)# ip address 192.168.50.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 99 (Out-of-Band Management Environment)
Router(config)# interface g0/0.99
Router(config-subif)# description Default Gateway for OOBM
Router(config-subif)# encapsulation dot1Q 99
Router(config-subif)# ip address 192.168.99.1 255.255.255.0
Router(config-subif)# exit

! Subinterface for VLAN 100 (Hardened DMZ Cluster Tier)
Router(config)# interface g0/0.100
Router(config-subif)# description Default Gateway for Hardened DMZ
Router(config-subif)# encapsulation dot1Q 100
Router(config-subif)# ip address 192.168.100.1 255.255.255.0
Router(config-subif)# exit
```

### Step 4 – Configure Centralized DHCP Scopes

Automate network scaling, asset tracking, and device management profiles by executing dynamic lease scopes directly on the router's localized pools:

```text
```text
! Exclude default gateway tracking and static infrastructure server IPs from scope distribution
Router(config)# ip dhcp excluded-address 192.168.10.1 192.168.10.99
Router(config)# ip dhcp excluded-address 192.168.15.1 192.168.15.9
Router(config)# ip dhcp excluded-address 192.168.20.1 192.168.20.99
Router(config)# ip dhcp excluded-address 192.168.30.1 192.168.30.99
Router(config)# ip dhcp excluded-address 192.168.40.1 192.168.40.9
Router(config)# ip dhcp excluded-address 192.168.50.1 192.168.50.99

! Configure pools per segment
Router(config)# ip dhcp pool Finance_Pool
Router(dhcp-config)# network 192.168.10.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.10.1
Router(dhcp-config)# dns-server 192.168.30.100
Router(dhcp-config)# exit

Router(config)# ip dhcp pool Executive_Pool
Router(dhcp-config)# network 192.168.15.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.15.1
Router(dhcp-config)# dns-server 192.168.30.100
Router(dhcp-config)# exit

Router(config)# ip dhcp pool HR_Admin_Pool
Router(dhcp-config)# network 192.168.20.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.20.1
Router(dhcp-config)# dns-server 192.168.30.100
Router(dhcp-config)# exit

Router(config)# ip dhcp pool IT_SOC_IAM_Pool
Router(dhcp-config)# network 192.168.30.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.30.1
Router(dhcp-config)# dns-server 192.168.30.100
Router(dhcp-config)# exit

Router(config)# ip dhcp pool Guest_Pool
Router(dhcp-config)# network 192.168.40.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.40.1
Router(dhcp-config)# exit

Router(config)# ip dhcp pool IoT_Printers_Pool
Router(dhcp-config)# network 192.168.50.0 255.255.255.0
Router(dhcp-config)# default-router 192.168.50.1
Router(dhcp-config)# exit

```
## Step 5 – Configure Access Control Lists (Core Security Optimization)

To implement functional Inter-VLAN security boundaries within Cisco IOS Router-on-a-Stick deployments, Extended Access Control Lists are mapped precisely to logical subinterfaces.

```text
! ====================================================================
! 1. DEFINE ACCESS CONTROL LISTS
! ====================================================================

! --- ACL for Finance Department (VLAN 10) ---
Router(config)# ip access-list extended FINANCE_INBOUND_ACL
Router(config-ext-nacl)# permit tcp any any established
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! --- ACL for Executive Suite Tiers (VLAN 15) ---
Router(config)# ip access-list extended EXECUTIVE_INBOUND_ACL
Router(config-ext-nacl)# permit tcp any any established
Router(config-ext-nacl)# deny ip 192.168.15.0 0.0.0.255 host 192.168.10.50
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! --- ACL for HR & Administration (VLAN 20) ---
Router(config)# ip access-list extended HR_INBOUND_ACL
Router(config-ext-nacl)# permit tcp any any established
Router(config-ext-nacl)# deny ip 192.168.20.0 0.0.0.255 192.168.30.0 0.0.0.255
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! --- ACL for Guest Space Mobility Domain (VLAN 40) ---
Router(config)# ip access-list extended GUEST_INBOUND_ACL
Router(config-ext-nacl)# deny ip 192.168.40.0 0.0.0.255 192.168.0.0 0.0.255.255
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! --- ACL for IoT & Hardened Printer Domain (VLAN 50) ---
Router(config)# ip access-list extended IOT_INBOUND_ACL
Router(config-ext-nacl)# deny ip 192.168.50.0 0.0.0.255 192.168.0.0 0.0.255.255
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! --- ACL for Out-of-Band Management Tier (VLAN 99) ---
Router(config)# ip access-list extended OOBM_INBOUND_ACL
Router(config-ext-nacl)# permit ip host 192.168.99.100 any
Router(config-ext-nacl)# deny ip any any
Router(config-ext-nacl)# exit

! --- ACL for Hardened DMZ Server Farm (VLAN 100) ---
Router(config)# ip access-list extended DMZ_INBOUND_ACL
Router(config-ext-nacl)# permit tcp any any established
Router(config-ext-nacl)# deny ip 192.168.100.0 0.0.0.255 192.168.0.0 0.0.255.255
Router(config-ext-nacl)# permit ip any any
Router(config-ext-nacl)# exit

! ====================================================================
! 2. BIND ACCESS CONTROL LISTS TO LOGICAL SUBINTERFACES (INGRESS)
! ====================================================================

Router(config)# interface g0/0.10
Router(config-subif)# ip access-group FINANCE_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.15
Router(config-subif)# ip access-group EXECUTIVE_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.20
Router(config-subif)# ip access-group HR_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.40
Router(config-subif)# ip access-group GUEST_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.50
Router(config-subif)# ip access-group IOT_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.99
Router(config-subif)# ip access-group OOBM_INBOUND_ACL in
Router(config-subif)# exit

Router(config)# interface g0/0.100
Router(config-subif)# ip access-group DMZ_INBOUND_ACL in
Router(config-subif)# exit
