# IP Addressing Plan

## MPLS & VPN Links

- CE1–PE1 (Emergence)     : 172.60.30.0/28
- PE1–P1                  : 172.60.30.16/28
- P1–P2                   : 172.60.30.32/28
- P2–PE4                  : 172.60.30.48/28
- PE4–CE4 (Rep_Yde)       : 172.60.30.64/28
- P2–PE5 (Ancien_Port)    : 172.60.30.80/28
- PE5–CE5 (Mboro)         : 172.60.30.96/28
- P1–PE3 (Mboro)         : 172.60.30.112/28
- PE3–CE3 (Mboro)        : 172.60.30.128/28

## PE Loopback Addresses

- Loopback0 on PE1: 20.0.0.10/32
- Loopback0 on PE2: 20.0.0.20/32
- Loopback0 on PE3: 20.0.0.30/32
- Loopback0 on PE4: 20.0.0.0/32


# Routing Steps Overview

This document explains the configuration order in detail:

1. **VRF Creation** on PE routers
2. **Interface Configuration** plus enabling LDP for MPLS
3. **OSPF Configuration** in the MPLS backbone
4. **EIGRP Setup** between PE and CE routers
5. **MP-BGP Configuration** between PE routers (using loopbacks)
6. **Route Redistribution** between EIGRP and BGP

# Route Redistribution Steps

This document provides detailed commands for redistributing routes between EIGRP and BGP for each VRF, step by step:

- Commands to redistribute EIGRP into BGP
- Commands to redistribute BGP routes back into EIGRP
