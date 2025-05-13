### 📍 Network Address – Samedan

> What is the network address for the Samedan location?

**SHORT ANSWER**
**192.168.3.0/24**
The router at Samedan uses `192.168.3.1` as the gateway, placing the entire subnet in `192.168.3.0/24`.

---

### 📡 Access Point – Bellinzona

> What IP address is the AccessPoint located at in Bellinzona?

**SHORT ANSWER**
**192.168.4.253**
The AP in Bellinzona is a ZyXEL NWA1123-AC with this static IP address on VLAN-3.

---

### 🖥️ VLAN – Workstation PCs

> In which VLAN are the workstation PCs located?

**SHORT ANSWER**
**VLAN-2: Office**
All PCs are connected to ports 1–23 on the switches, which are assigned to VLAN-2 (Office).

---

### 🔧 Manageable Switch – Chur

> What IP address is the manageable switch located at in Chur?

**SHORT ANSWER**
**192.168.2.253**
This is the static IP of the ZyXEL manageable switch at the Chur location.

---

### 🔐 VPN Gateway – Bellinzona

> What IP addresses are configured for the LAN side and tunnel side of the VPN gateway at the Bellinzona location?

**SHORT ANSWER**
**LAN:** `192.168.4.1` | **Tunnel (VPN-B):** `172.200.4.2/24`
The router handles internal routing and VPN connections to other locations.

---

### 🌐 Default Gateway – Samedan

> What is the default gateway configured for the workstation PCs at the Samedan location?

**SHORT ANSWER**
**192.168.3.1**
The router in Samedan is configured as the default gateway for local PCs.

---

### 🧳 VPN for Field Service

> A field service employee needs access to the company network. How should they configure their VPN-SW IP address?

**SHORT ANSWER**
**Use VPN-C (Remote Access) with IP range 172.200.5.0/24**
The gateway IP is `172.200.5.1`, providing encrypted remote access.

---

### ☎️ VoIP – CAD Water Engineering

> Who installed the VoIP phones in the CAD Water Engineering office?

**SHORT ANSWER**
**abisang**
According to the patch panel log, abisang installed the VoIP phone on `19.05.14`.

---

### 🍽️ AccessPoint – Bistro

> When was the AccessPoint installed in the Bistro?

**SHORT ANSWER**
**10.01.14**
Two RJ45 outlets are present, and the Access Point was installed on that date. 
Located in the Bistro (Erdgeschoss, Hauptsitz Chur), according to the Verkabelungsplan and patch list entries

---

### 👨‍💼 Rene Sauter – Leaving the Company

> IT employee Rene Sauter (rsauter) is leaving the company. Which tasks or responsibilities are affected? Who would you suggest as the future contact person for problems?

**SHORT ANSWER**
**Affected:**
* Patch panel documentation and port assignments (e.g., E1/1, E2/1, E3/2) were entered or maintained by rsauter. His initials are associated with several workstation and printer installations across the network
**Suggested successor:** abisang
rsauter set up many patch ports and hardware. abisang appears active and competent in similar areas. (VoIP, CAD)



---

### 🧮 RJ45 Sockets – Project Manager Office

> How many RJ45 sockets are available in the project manager’s office, and how many of them are currently not occupied?

**SHORT ANSWER**
**6 total**, **1 free**
the Bauleiterbüro: 6 ports exist (E3–E5); only E3/1 is free.

* Total RJ45 sockets: 6 (E3/1, E3/2, E4/1, E4/2, E5/1, E5/2)
* Occupied: 5 (All except E3/1 are marked as "Belegt")
* Free sockets: 1 (→ E3/1)

---

### 📞 VoIP Phone – CAD Civil Engineering

> In the CAD Civil Engineering office, another VoIP phone needs to be provided. How should this connection be patched? The patch panel configuration and the switch port are required.

* Available RJ45 socket: E2/2 (Free)
* Patch panel location: E2/2 (CAD Tiefbau)
* Switch port (Office VLAN): Ports 1–23 in VLAN-2 (Office)

**Patch configuration:**

* Connect E2/2 (Patchpanel) → Switch Port 1–23 (VLAN-2)
This VLAN is used for both workstation PCs and VoIP phones

---

### 🖥️ Ethernet – Bistro Presentation

> A project presentation is scheduled in the Bistro. An Ethernet cable connection needs to be provided for this.

**SHORT ANSWER**
**Use one of the 2 RJ45 sockets and patch it to VLAN-2 (Port 1–23)**
This ensures standard office Ethernet access for a laptop or presentation device.

---

### 🧑‍💻 Temporary Workstation – CAD Water Engineering

> In the CAD Water Engineering office, a temporary workstation needs to be set up. How would you solve this task?

**SHORT ANSWER**
**Patch E11/2 to Switch Port 1–23 (VLAN-2)**
This port is free and provides both DHCP and internet access via Office VLAN.

* Available RJ45 socket: E11/2 (assuming it refers to CAD Wasserbau; status is blank → free)
* Patch panel: E11/2
* Switch port: Connect to Port 1–23 (VLAN-2) for standard PC access

**Steps:**

* Patch E11/2 to a switch port in VLAN-2
* Place a temporary PC at the corresponding outlet
* DHCP will assign IP via 192.168.2.x or relevant subnet

---

### 🖲️ Switches – Chur Location

> How many switches are available at the Chur location?

**SHORT ANSWER**
**3 total switches**
Two are stacked ZyXEL XGS1910-24 units, and one standalone XG1910-24 is also present.

---

### 🚫 No Internet – Mrs. Sommer

> Mrs. Sommer works at the CAD workstation and reports that she no longer has an internet connection. What will you check?

**SHORT ANSWER**
**Check cable, patchpanel port (E2/1), switch port, DHCP lease, and default gateway**
Ensure she’s patched into VLAN-2, has a valid IP, and can reach `192.168.2.1`.

Since Mrs. Sommer works at a **CAD workstation**, likely located in **CAD Tiefbau** or **CAD Wasserbau**, follow these steps:

#### 🔍 **Checklist for Troubleshooting:**

1. **Physical Connection (Layer 1):**

   * Check the **RJ45 socket** (e.g., `E2/1` for Tiefbau or `E11/1` for Wasserbau).
   * Ensure the cable is securely connected to both the PC and wall socket.
   * Inspect patch panel connection.

2. **Patchpanel & Switch (Layer 2):**

   * Verify that the patchpanel port (e.g., `E2/1`) is still patched to a **switch port** in **VLAN-2: Office** (Port 1–23).
   * Ensure switch port is active and link LED is on.

3. **IP Configuration (Layer 3):**

   * Check if the workstation has a valid IP address in the expected subnet (`192.168.2.x` for Chur).
   * Ping the **gateway (192.168.2.1)** and **DNS (192.168.2.3)**.

4. **DHCP Status:**

   * Make sure DHCP is functioning.
   * Router/Firewall in Chur handles DHCP on `192.168.2.3` – verify if lease is assigned.

5. **User Device:**

   * Restart network adapter.
   * Run `ipconfig /renew` or check logs for driver or software issues.

---

### 📶 SSID – Chur AccessPoint

> What is the SSID of the Chur AccessPoint?

**SHORT ANSWER**
**Not specified in the documentation**
The documentation does **not explicitly list** the SSID of the Access Point. However:

* It **shows the Access Points** are ZyXEL NWA1123-AC units.
* These are configured in **VLAN-2 (Office)** and **VLAN-3**.
* The SSID is likely broadcast for internal employee use, but the exact SSID (e.g., `Caprez_Office`) is **not mentioned in the provided network diagram or documentation**.
