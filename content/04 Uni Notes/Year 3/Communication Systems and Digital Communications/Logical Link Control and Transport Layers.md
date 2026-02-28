---
dateCreated: 2026-01-05 17:12
share_link: https://share.note.sx/04yw9x6q#rBk59n/ATkvHwh+BgwY4hZbYBfUQ38MUhQVwbbZ+njI
share_updated: 2026-01-21T17:10:57+00:00
---
[Module:: [[Communication Systems and Digital Communications]]]

The logical link [[Networks#Protocols|layer]] (LLC) is concerned with reliability, notably flow control and [[Error Control Coding|error control]]  on a hop-by-hop basis. If it's reliable, then the next node alerts the current note to retransmit the data. The transport layer is similar, but end-to-end, so the final destination alerts the original source to retransmit the data.
```table-of-contents
```
---
## Reliability
Consider a long chain of communication nodes, connected in a line. 
- How can we protect against a packet being lost in an intermediate node? It's useful to have a reliable transport layer to inform the source and destination of nodes if there's a bottleneck in the connection. 
- Similarly, how can you best protect against a packet being lost during transmission? It's useful to have a reliable data link layer to efficiently deal with a short term problem on a link.

LLC reliability can save energy, has acknowledgements don't have network layer headers, so they're shorter. Retransmission are shorter and faster, as they come from the node that sent the lost packet. Transport layer reliability is required to be 100% confident about packet delivery. Both provide low retransmission delays and ensure delivery.

[[flow control|Flow control]] is the process of determining the rate with which to send packets to a receiver, required when a receiver has a limited buffer size. [[Error Control Coding|Error control]] is the process of detecting errors, and deciding whether and how to re-transmit packets. They're both often implemented together, e.g. stop-and-wait ARQ, go-back-n ARQ, selective repeat ARQ.
## Stop and Wait
This is the simplest flow and error control mechanism.
1. The transmitter sends a single packet, storing a copy
2. Receiver receives the packet, and check for errors. If there are no errors, it sends an acknowledgement (ACK)
3. If transmitter receives an ACK, it deletes the copy, and sends the next packet. If no ACK arrives within a certain timeout period, it retransmits the packet. 

![[Logical Link Control and Transport Layers.png]]

- If the packet is received correctly, but the ACK goes through an error or loss, the transmitter retransmits, and the receiver gets a duplicate packet. To account for this, the packets must be numbered so the receiver can recognise and discard duplicates.
- If the ACK is delayed instead due to congestion, the packet gets retransmitted, but the acknowledge arrives after that happens, skipping an entire packet. This time, numbering the ACKs prevents gaps in the delivered packets.
### Link Utilisation 
An important link parameter can be defined as:
$$a = \frac{t_{\text{prop}}}{t_{\text{packet}}}= \frac{d}{v} \cdot \frac{R}{L}$$
- $R$ is the link data rate ($\text{bps}$)
- $d$ is the link distance ($\text{m}$)
- $v$ is the propagation speed ($m/s$) 
- $L$ is the packet length ($\text{bits}$)

In the error-free case, the best case link utilisation of stop and wait ARQ is:
$$\text{LU} = \frac{1}{1+2a}$$
