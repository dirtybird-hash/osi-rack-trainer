# OSI / TCP-IP Reference

The source of truth for everything the trainer scores.

## The chart

| TCP/IP | OSI | # | PDU | Address | Devices |
|---|---|---|---|---|---|
| Application | Application | 7 | Data | — | — |
| Application | Presentation | 6 | Data | — | — |
| Application | Session | 5 | Data | — | — |
| Transport | Transport | 4 | Segments | Port #s | — |
| Internet | Network | 3 | Packets | IP Addresses | Routers |
| Network Access | Data Link | 2 | Frames | MAC Addresses | Switches / Bridges, NIC |
| Network Access | Physical | 1 | Bits | — | Hubs / Repeaters, NIC |

Cells marked — are the blacked-out cells on the printed chart. They are not oversights; nothing operates there.

## Mnemonics

| Column | Mnemonic (7 → 1) |
|---|---|
| OSI | **A**ll **P**eople **S**eem **T**o **N**eed **D**ata **P**rocessing |
| TCP/IP | **A**pple **T**ainted **I**ngest **N**ever |
| PDU | **D**rippy **S**weet **P**ancakes **F**or **B**reakfast |

## Spans worth memorizing

- TCP/IP **Application** absorbs OSI 7, 6 and 5.
- TCP/IP **Network Access** absorbs OSI 2 and 1.
- **Transport** is the only 1:1 mapping between the two models.
- **PDU "Data"** covers 7, 6 and 5 — nothing has been encapsulated yet.
- **NIC** straddles 1 and 2: it puts signal on the wire and carries the MAC address.

## Encapsulation, top down

```
Data  ──(+TCP/UDP header, ports)──►  Segment
      ──(+IP header, addresses)───►  Packet
      ──(+MAC header, FCS trailer)►  Frame
      ──(signal on the medium)────►  Bits
```

De-encapsulation is the same list read upward.

## Layer functions in one line each

| # | Layer | Owns |
|---|---|---|
| 7 | Application | The interface the user touches. HTTP, FTP, DNS, SMTP, DHCP, SNMP |
| 6 | Presentation | Translation, encryption, compression. TLS/SSL, ASCII/EBCDIC, JPEG |
| 5 | Session | Establish, maintain, terminate. Logon, checkpoints, tunneling |
| 4 | Transport | End-to-end delivery. TCP vs UDP, ports, sequencing, 3-way handshake |
| 3 | Network | Logical addressing and path selection. IP, ICMP, OSPF, NAT, fragmentation |
| 2 | Data Link | Node-to-node framing and physical addressing. Ethernet, ARP, PPP, VLAN tags |
| 1 | Physical | Signal, media, connectors. Copper, fiber, radio, RJ45, speed/duplex |

## Layer 2 sublayers

- **LLC** — Logical Link Control: flow control, error control, talks to Layer 3.
- **MAC** — Media Access Control: media access method and the 12-hex-character hardware address. First half is the manufacturer OUI, second half is the node ID.

## Troubleshooting tells

| Symptom | Layer |
|---|---|
| No link light, bent pin, EMI, attenuation, speed/duplex mismatch | 1 |
| MAC flapping, wrong VLAN tag, ARP anomalies, switching loops | 2 |
| Duplicate IP, wrong gateway, no route, MTU/fragmentation | 3 |
| Blocked port, UDP dropouts with no retransmit, handshake failure | 4 |
| Session drops on idle, re-authentication loops, tunnel instability | 5 |
| Certificate expired, character encoding garbled, compression mismatch | 6 |
| HTTP 404, application error message, app logic failure | 7 |

## Known courseware conflicts

**ARP** — scored here as Layer 2. Called "Layer 2.5" in some material because it bridges L3 to L2 addressing. CompTIA treats it as data link.

**DNS** — scored here as Layer 7. Some older courseware places it at Layer 5 because name resolution is framed as a session service. CompTIA and Professor Messer both place it at the application layer.
