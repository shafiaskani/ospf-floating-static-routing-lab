# OSPF + Floating Static Routing Lab

## Project Overview

A three-router Cisco Packet Tracer lab focused on **OSPF dynamic routing** and **floating static routes**.

I designed and configured the entire lab independently to practice routing, route selection, verification, and systematic troubleshooting.

## Topology

```text
                  R1
                /    \
               /      \
              R2------R3
```

### Router Connections

* R1 ↔ R2 — `10.0.12.0/30`
* R1 ↔ R3 — `10.0.13.0/30`
* R2 ↔ R3 — `10.0.23.0/30`

### Loopback Networks

| Router | Loopback     | Purpose                 |
| ------ | ------------ | ----------------------- |
| R1     | `1.1.1.1/32` | OSPF advertised network |
| R2     | `2.2.2.2/32` | OSPF advertised network |
| R3     | `3.3.3.3/32` | OSPF advertised network |

## Technologies & Concepts

* OSPF
* OSPF Area 0
* OSPF Router IDs
* OSPF neighbor relationships
* OSPF route advertisement
* Loopback interfaces
* Floating static routes
* Administrative Distance
* Routing-table analysis
* Network connectivity testing
* Cisco IOS verification commands
* Systematic routing troubleshooting

## OSPF Configuration

OSPF process `1` was configured on all three routers using **Area 0**.

Each router advertises its directly connected point-to-point networks and loopback interface.

Router IDs:

* R1 — `1.1.1.1`
* R2 — `2.2.2.2`
* R3 — `3.3.3.3`

Loopback interfaces were configured as passive OSPF interfaces because they do not require OSPF neighbor formation.

## Floating Static Routes

Floating static routes were configured with an **administrative distance of 200**.

OSPF has an administrative distance of **110**, so OSPF remains the preferred routing source while the floating static route is configured as a backup.

Examples:

```cisco
R1:
ip route 2.2.2.2 255.255.255.255 10.0.12.2 200

R2:
ip route 3.3.3.3 255.255.255.255 10.0.23.2 200

R3:
ip route 1.1.1.1 255.255.255.255 10.0.13.1 200
```

The purpose of this configuration was to practice **route preference and administrative distance**, without performing route-failure or failover testing.

## Verification

The following Cisco IOS commands were used to verify the configuration:

```cisco
show ip interface brief
show ip ospf neighbor
show ip ospf interface brief
show ip protocols
show ip route
show ip route ospf
show ip route static
show ip ospf database
ping
traceroute
```

### Connectivity Verification

Connectivity between the router loopbacks was tested using:

```cisco
ping 1.1.1.1
ping 2.2.2.2
ping 3.3.3.3
```

Traceroute was also used to observe the routing path.

## Troubleshooting

The lab also included systematic troubleshooting and verification rather than relying only on configuration commands.

The troubleshooting process followed a layered approach:

1. Verify interface status and IP addressing.
2. Test directly connected neighbors.
3. Verify OSPF neighbor relationships.
4. Check OSPF configuration and advertised networks.
5. Inspect the routing table.
6. Verify OSPF-learned routes.
7. Verify floating static route configuration.
8. Test end-to-end connectivity with ping and traceroute.

This helped reinforce the process of identifying whether a routing problem originates from the interface, OSPF adjacency, route advertisement, or routing table.

## Tools

* Cisco Packet Tracer
* Cisco IOS CLI

## AI-Assisted Troubleshooting

I completed the network design and configuration independently.

During troubleshooting, I used **ChatGPT as a troubleshooting assistant** to help interpret Cisco IOS command output, narrow down possible causes, and understand the reasoning behind the troubleshooting process.

The goal was to use AI as a learning and troubleshooting aid while maintaining hands-on configuration and verification of the network myself.

## Key Learning Outcomes

This lab strengthened my practical understanding of:

* How OSPF establishes neighbor relationships.
* How OSPF advertises routes.
* How routers select routes using administrative distance.
* How floating static routes can be configured as backup routes.
* How to verify OSPF using Cisco IOS commands.
* How to systematically troubleshoot routing problems.
* How to interpret routing tables and OSPF information.

## Project File

The Cisco Packet Tracer project file is included in this repository:

`OSPF-Floating-Static.pkt`
