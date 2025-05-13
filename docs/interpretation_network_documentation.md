### Network Address – Samedan

> What is the network address for the Samedan location?

**SHORT ANSWER**
**192.168.3.0/24**
The IPFire router at Samedan uses `192.168.3.1` as the gateway, which places all local devices in the `192.168.3.0/24` subnet.

---

### Access Point – Bellinzona

> What IP address is the AccessPoint located at in Bellinzona?

**SHORT ANSWER**
**192.168.4.253**
The ZyXEL NWA1123-AC Access Point at Bellinzona is assigned a static IP in VLAN-3.

---

### VLAN – Workstation PCs

> In which VLAN are the workstation PCs located?

**SHORT ANSWER**
**VLAN-2: Office**
All workstation PCs are connected to switch ports 1–23, which are part of VLAN-2 (Office).

---

### Manageable Switch – Chur

> What IP address is the manageable switch located at in Chur?

**SHORT ANSWER**
**192.168.2.253**
This IP belongs to the ZyXEL manageable switch located at the Chur main office.

---

### VPN Gateway – Bellinzona

> What IP addresses are configured for the LAN side and tunnel side of the VPN gateway at the Bellinzona location?

**SHORT ANSWER**
**LAN:** `192.168.4.1`
**VPN Tunnel (VPN-B):** `172.200.4.2/24`
The gateway provides local access and secure VPN connectivity to other sites.

---

### Default Gateway – Samedan

> What is the default gateway configured for the workstation PCs at the Samedan location?

**SHORT ANSWER**
**192.168.3.1**
Configured on the IPFire router, used as the default gateway by all local clients.

---

### VPN for Field Service

> A field service employee needs access to the company network. How should they configure their VPN-SW IP address?

**SHORT ANSWER**
**Use VPN-C (RAS) within 172.200.5.0/24**
The gateway IP `172.200.5.1` is used for secure remote access via VPN-C (Remote Access).

---

### VoIP – CAD Water Engineering

> Who installed the VoIP phones in the CAD Water Engineering office?

**SHORT ANSWER**
**abisang**
According to the patch panel documentation, the VoIP installation on `19.05.14` was handled by abisang.

---

### Access Point – Bistro

> When was the AccessPoint installed in the Bistro?

**SHORT ANSWER**
**10.01.14**
Installed near the RJ45 outlets in the Bistro (Erdgeschoss, Chur). Installation details appear in the Verkabelungsplan and patch panel log.

---

### Rene Sauter – Leaving the Company

> IT employee Rene Sauter (rsauter) is leaving the company. Which tasks or responsibilities are affected? Who would you suggest as the future contact person for problems?

**SHORT ANSWER**
**Affected tasks:**

* Patch panel records
* Port assignments for PCs and printers (e.g., E1/1, E2/1, E3/2)

**Suggested successor:**
**abisang** – Actively involved in VoIP and CAD infrastructure.

---

### RJ45 Sockets – Project Manager Office

> How many RJ45 sockets are available in the project manager’s office, and how many of them are currently not occupied?

**SHORT ANSWER**
**6 total**, **1 free**
Located in the Bauleiterbüro (E3–E5). Only `E3/1` is currently unoccupied.

---

### VoIP Phone – CAD Civil Engineering

> In the CAD Civil Engineering office, another VoIP phone needs to be provided. How should this connection be patched? The patch panel configuration and the switch port are required.

**SHORT ANSWER**
**Patch Panel:** E2/2
**Switch Port:** 1–23 (VLAN-2: Office)
Connect E2/2 on the patch panel to a switch port in VLAN-2 to enable VoIP functionality.

---

### Ethernet – Bistro Presentation

> A project presentation is scheduled in the Bistro. An Ethernet cable connection needs to be provided for this.

**SHORT ANSWER**
Use one of the two RJ45 outlets in the Bistro and patch it to **VLAN-2 (Port 1–23)**.
This provides standard office network access.

---

### Temporary Workstation – CAD Water Engineering

> In the CAD Water Engineering office, a temporary workstation needs to be set up. How would you solve this task?

**SHORT ANSWER**
**Patch Panel:** E11/2 (free)
**Switch Port:** 1–23 (VLAN-2)

**Steps:**

1. Patch E11/2 to VLAN-2 switch port
2. Connect a workstation
3. DHCP assigns an IP in `192.168.2.x`

---

### Switches – Chur Location

> How many switches are available at the Chur location?

**SHORT ANSWER**
**3 switches total**

* 2x ZyXEL XGS1910-24 (stacked)
* 1x ZyXEL XG1910-24 (standalone)

---


### No Internet – Mrs. Sommer

> Mrs. Sommer works at the CAD workstation and reports that she no longer has an internet connection. What will you check?

**SHORT ANSWER**
**Check cable, patchpanel port (E2/1), switch port, DHCP lease, and default gateway**
Ensure she’s patched into VLAN-2, has a valid IP, and can reach `192.168.2.1`.

Since Mrs. Sommer works at a **CAD workstation**, likely located in **CAD Tiefbau** or **CAD Wasserbau**, follow these steps:

#### **Checklist for Troubleshooting:**

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

### SSID – Chur AccessPoint

> What is the SSID of the Chur AccessPoint?

**SHORT ANSWER**
**Not specified in the documentation**
The documentation does **not explicitly list** the SSID of the Access Point. However:

* It **shows the Access Points** are ZyXEL NWA1123-AC units.
* These are configured in **VLAN-2 (Office)** and **VLAN-3**.
* The SSID is likely broadcast for internal employee use, but the exact SSID (e.g., `Caprez_Office`) is **not mentioned in the provided network diagram or documentation**.
