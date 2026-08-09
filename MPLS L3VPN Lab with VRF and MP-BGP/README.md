# Cisco CCNP: MPLS L3VPN with VRF and MP-BGP

![MPLS Topology](MPLS%20Topology.png)

Service Provider infrastruktura koja omogućava spajanje udaljenih korisničkih lokacija (CE) preko MPLS jezgra koristeći VRF izolaciju i MP-BGP za razmenu VPNv4 ruta.

---

### Mrežne Uloge i Komponente

* **Customer Edge (CE):** CE-1, CE-2
* **Provider Edge (PE):** PE-1, PE-2 (MP-BGP, VRF, MPLS)
* **Provider Core (P):** R1 (LDP / MPLS Core)

---

### Configurations & Verification

* [CE-1 Configuration](./CE-1.md)
* [CE-2 Configuration](./CE-2.md)
* [PE-1 Configuration](./PE-1.md)
* [PE-2 Configuration](./PE-2.md)
* [P Router (R1) Configuration](./R1.md)
* [Traceroute Verification](./TracerouteFromPC1.PNG)