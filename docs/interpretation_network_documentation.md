### Network Address – Samedan

> What is the network address for the Samedan location?

**SHORT ANSWER**
**192.168.3.0/24**
The IPFire router at Samedan uses `192.168.3.1` as the gateway, which places all local devices in the `192.168.3.0/24` subnet.

---

### Access Point – Bellinzona

> What IP address is the AccessPoint located at in Bellinzona?

**SHORT ANSWER**
**192.168.4.30**
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
**23.07.14**
Installed by `rsauter` via patch panel port `E8/1`. Installation details appear in the Verkabelungsplan and patch panel log.

---

### Rene Sauter – Leaving the Company

> IT employee Rene Sauter (rsauter) is leaving the company. Which tasks or responsibilities are affected? Who would you suggest as the future contact person for problems?

**SHORT ANSWER**
**Affected tasks:**

* Patch panel records and cabling for:

  * Empfang EG PC (E1/11)
  * CAD Tiefbau (E2/1)
  * MF-Kopierer (E3/2)
  * Bistro AccessPoint (E8/1)

**Suggested successors:**
**blaeuchli**, **abisang**, **rkundert** – All actively involved in infrastructure and support.

---

### RJ45 Sockets – Project Manager Office

> How many RJ45 sockets are available in the project manager’s office, and how many of them are currently not occupied?

**SHORT ANSWER**
**8 total**, **2 free**
Located in the Bauleiterbüro from `E3/1` to `E6/2`. Two of the eight RJ45 sockets are currently unoccupied.

---

### VoIP Phone – CAD Civil Engineering

> In the CAD Civil Engineering office, another VoIP phone needs to be provided. How should this connection be patched? The patch panel configuration and the switch port are required.

**SHORT ANSWER**
**Patch Panel:** E2/3
**Switch Port:** 24–47 (VLAN-1: Phone)
Connect E2/3 on the patch panel to a switch port in VLAN-1 to enable VoIP functionality.

---

### Ethernet – Bistro Presentation

> A project presentation is scheduled in the Bistro. An Ethernet cable connection needs to be provided for this.

**SHORT ANSWER**
Use one of the RJ45 outlets in the Bistro (e.g., `E9/1` or `E9/2`) and patch it to **VLAN-2 (Port 1–23)**.
This provides standard office network access.

---

### Temporary Workstation – CAD Water Engineering

> In the CAD Water Engineering office, a temporary workstation needs to be set up. How would you solve this task?

**SHORT ANSWER**
Use a free RJ45 socket from the patch panel, connect it to **VLAN-2 (Port 1–23)**

**Steps:**

1. Select a free patch port (e.g., `E11/2`)
2. Patch it to a switch port in VLAN-2
3. Connect workstation
4. DHCP assigns an IP in `192.168.2.x`

---

### Switches – Chur Location

> How many switches are available at the Chur location?

**SHORT ANSWER**
**2 switches total**

* 2x ZyXEL XGS1910-24 (stacked)

---

### No Internet – Mrs. Sommer

> Mrs. Sommer works at the CAD workstation and reports that she no longer has an internet connection. What will you check?

**SHORT ANSWER**
**Check cable, patchpanel port (e.g., E2/1), switch port, DHCP lease, and default gateway**
Ensure she’s patched into VLAN-2, has a valid IP, and can reach `192.168.2.1`.

Since Mrs. Sommer works at a **CAD workstation**, likely located in **CAD Tiefbau** or **CAD Wasserbau**, follow these steps:

#### **Checklist for Troubleshooting:**

1. **Physical Connection (Layer 1):**

   * Check the **RJ45 socket** (e.g., `E2/1` for Tiefbau or `E11/1` for Wasserbau).
   * Ensure the cable is securely connected to both the PC and wall socket.
   * Inspect patch panel connection.

2. **Patchpanel & Switch (Layer 2):**

   * Verify that the patchpanel port is patched to a **switch port** in **VLAN-2: Office** (Port 1–23).
   * Ensure switch port is active and link LED is on.

3. **IP Configuration (Layer 3):**

   * Check if the workstation has a valid IP in `192.168.2.x`.
   * Ping the **gateway (192.168.2.1)** and **DNS (192.168.2.3)**.

4. **DHCP Status:**

   * Ensure DHCP on `192.168.2.3` is assigning leases.

5. **User Device:**

   * Restart network adapter.
   * Run `ipconfig /renew`, check for software/driver issues.

---

### SSID – Chur AccessPoint

> What is the SSID of the Chur AccessPoint?

**SHORT ANSWER**
**Not specified in the documentation**
The documentation does **not explicitly list** the SSID of the Access Point. However:

* ZyXEL NWA1123-AC units are used
* Configured in **VLAN-2 (Office)** and **VLAN-3**
* The SSID is likely internal (e.g., `Caprez_Office`) but not documented

