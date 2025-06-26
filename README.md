# MPLS-VPN-KRIBI
# MPLS VPN Configuration – Port Autonome de Kribi

This project demonstrates the configuration of a full MPLS Layer 3 VPN (L3VPN) infrastructure to interconnect four remote sites of the Port Autonome de Kribi (PAK):

- **Emergence** (`CE1`)
- **Ancien Port** (`CE2`)
- **Mboro** (`CE3`)
- **Représentation Yaoundé** (`CE4`)

## Network Overview

The MPLS VPN solution enables seamless communication between all CE routers via MPLS backbone (P/PE routers). The deployment uses:

- **OSPF** for IGP in the MPLS backbone (P/PE)
- **EIGRP** between CE and PE
- **MP-BGP** for VPN route exchange between PE routers
- **VRF**, RD, and RT for VPN segmentation and control

## Folder Structure
```text
├── configs/
│ ├── CE1_Emergence.cfg
│ ├── CE2_AncienPort.cfg
│ ├── CE3_Mboro.cfg
│ ├── CE4_RepYde.cfg
│ ├── PE1.cfg
│ ├── PE2.cfg
│ ├── PE3.cfg
│ ├── PE4.cfg
│ ├── P1.cfg
│ ├── P2.cfg
│ ├── P3.cfg
│ └── PC1.vpc
├── README.md 
```

## Configuration Steps

### 1. Create VRFs on PE routers
Each PE router has one or more VRFs to separate customer routing tables.

### 2. Configure Interfaces
Assign IP addresses to all interfaces and associate CE-facing interfaces with the correct VRFs.

### 3. Enable MPLS
Enable `mpls ip` on all interfaces between PE and P routers.

### 4. IGP (OSPF) in the Core
Configure OSPF between all P and PE routers using Area 0.

### 5. PE-CE Routing (EIGRP)
Configure EIGRP between each CE and its connected PE using appropriate VRF context.

### 6. MP-BGP Between PEs
Configure full-mesh BGP using Loopback0 addresses as update-source.
- Activate `vpnv4` address-family
- Use `send-community both` to propagate RTs

### 7. Route Redistribution
- **EIGRP → BGP**: Inside `address-family ipv4 vrf`
- **BGP → EIGRP**: Also under `address-family ipv4 vrf`

## Devices

| Device | Role          | Loopback     | Connected Subnets         |
|--------|---------------|--------------|----------------------------|
| PE1    | Provider Edge | 20.0.0.10    | CE1 - 172.60.30.0/28       |
| PE2    | Provider Edge | 20.0.0.20    | CE2 - 172.60.30.64/28      |
| PE3    | Provider Edge | 20.0.0.30    | CE4 - 172.60.30.128/28     |
| PE4    | Provider Edge | 20.0.0.40    | CE3 - 172.60.30.96/28      |
| P1-P3  | MPLS Backbone | —            | MPLS transit subnets       |

## Simulation

You can simulate this topology using:
- **Cisco Packet Tracer**
- **GNS3**
- **EVE-NG**

Each configuration file in the `configs/` folder is copy-paste ready.

## Contact

Maintained by [Your Name] at Port Autonome de Kribi.  
If you find issues or have improvements, feel free to open an issue or pull request.

---

## Notes

- Ensure all routers have CEF, MPLS, and BGP capabilities.
- Loopback interfaces must be advertised in OSPF for MP-BGP peering to work.
- Verify `show ip bgp vpnv4 all`, `show mpls ldp neighbor`, and `show vrf` to debug.


