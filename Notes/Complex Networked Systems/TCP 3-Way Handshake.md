---
title: TCP 3-Way Handshake
aliases:
  - TCP Handshake
  - Three-Way Handshake
tags:
  - networking
  - tcp
description: "Three-step method to establish a reliable, full-duplex TCP connection between client and server."
---

The **TCP 3-Way Handshake** is the three-step method used to establish a reliable, full-duplex TCP connection between a client and a server before data transmission.

## Steps

**Step 1: SYN (Synchronize)**
Client sends a TCP packet with the SYN flag and an initial sequence number `seq=m` to the server.

**Step 2: SYN-ACK (Synchronize-Acknowledgment)**
Server replies with a packet containing both SYN and ACK flags. `seq=n`, `ack=m+1`. The ACK acknowledges the client's previous packet.

**Step 3: ACK (Acknowledgment)**
Client receives the SYN-ACK and sends back a packet with the ACK flag (`ack=n+1`) to confirm. The connection is now established.

```
Client                          Server
  |                                |
  | -----SYN (seq=m)-------------> |
  |                                |
  | <----SYN+ACK (seq=n, ack=m+1)- |
  |                                |
  | -----ACK (ack=n+1)-----------> |
  |                                |
  |          (established)         |
```

All subsequent packets contain the ACK flag, acknowledging the previously received packet.

## Relevance to Security

Stateless [[Firewall|firewalls]] use the TCP/ACK flag to distinguish new connection attempts (no ACK) from packets belonging to an existing flow (ACK set). This allows them to approximate connection state without tracking sessions.

## Related Concepts

- [[Firewall]]: stateless rules use the ACK flag to track connection direction
