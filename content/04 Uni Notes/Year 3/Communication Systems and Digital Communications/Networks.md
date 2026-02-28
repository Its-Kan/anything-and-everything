---
dateCreated: 2026-01-01 18:22
share_link: https://share.note.sx/4c6kw2sz#NwLwxBY7elVNT02U/R0d1sxTe/NCBwR76MimyhLi1dQ
share_updated: 2026-01-21T17:10:07+00:00
---
[Module:: [[Communication Systems and Digital Communications]]]

So far, we've only be considering a single receiver and transmitter, but a real [[communication system]] has many users. It also involves multiple hops, where data packets use several links and intermediate nodes to get to its destination.
```table-of-contents
```
---
## Network Architectures
There are multiple ways a network can be designed. 

![[Networks.png]]

| **Architecture**                | **Description**                                                                                                                                                                        | **Analogy**                                                                                                                                                                                                           | **Pros**                                                                                                   | **Cons**                                                                           |
| ------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Circuit-Switched Networks       | Sets up a dedicated connection between a pair of users, where nodes act as switches.                                                                                                   | Network reserves a specific "lane" for the connection, and only breaks when the connection ends.                                                                                                                      | Guarantees a certain data rate and delay between users, can be virtual circuit in packet-switched network. | Connection has to be set up in advance, which adds overheads.                      |
| Packet-Switched Networks        | Data stream divided into packets, each of which is individually routed through the network. Nodes act as routers, which store and forward packets, and determine next hop destination. | Network breaks down a message into packets, and sends packets via multiple routes, which can change dynamically. The receiver gets the packets potentially out of order, however the packets store its order as well. | No setup required, which reduced delay for short messages.                                                 | Congestion can occur at nodes which increases delay and may cause [[packet loss]]. |
| Local Area Networks (LANs)      | Multi-user private networks serving a restricted area.                                                                                                                                 |                                                                                                                                                                                                                       | Single hop with direct [[communication]] is always possible from one terminal to another                   |                                                                                    |
| Wide Area Networks (WANs)       | Multi-hop, multi-user networks, covering a wide geographical area. may be circuit or packet switched.                                                                                  |                                                                                                                                                                                                                       | Often heterogenous (supports multiple links, hardware, software and protocols).                            |                                                                                    |
| Wireless Sensor Networks (WSNs) | A collection of small electronic devices which are able to monitor and record environmental conditions, communicate via radio, report back to a central location.                      |                                                                                                                                                                                                                       | Spontaneous, doesn't need infrastructure, multi-hop, doesn't need a fixed power source.                    |                                                                                    |
| Satellite Networks              | Provides broadcast television and data services to remote locations                                                                                                                    |                                                                                                                                                                                                                       | Wide coverage for broadcasts                                                                               | Long delays, limited capacity.                                                     |
## Protocols 
The task of working out how to send information through a network is usually divided into layers, called a protocol, each doing one thing:
1. **Application Layer**: User interface, source and destination of data
2. **Transport Layer**: end-to-end error and flow control 
3. **Network Layer**: routing
4. **Logical Link Layer**: hop-by-hop error and flow control 
5. **Medium Access Control Layer**: when to transmit
6. **Physical Layer**: getting data from transmitter to receiver 
Each protocol has an interface to the protocol above, and each one communicates with the peer-layer protocol at the other end of the link.

A protocol is a procedure for communications; a set of rules that programs use to communicate. In general, they contain a syntax (a language) and a series of timers to trigger events. They can be reliable or best effort, connection-oriented or connectionless, end-to-end or hop-by-hop. Some models include:
- ISO-OSI is complex, but consistent with seven layers. No one uses it, but it's an important reference model. 
- TCP/IP is not very consistent with five layers, but it's used in the wired/wireless internet.  
### Rules
There are rules in designing protocols. Traditionally:
- The interface between adjacent protocols should be simple.
- Only one protocol each layer
- Shouldn't require knowledge of the internal operation or state of any other protocol
But in practice:
- Cross-layer design can provide benefits, but complicates things
- Can have several different protocols at the same layer, which use the same lower layer protocol.
### Terminology
- [[network capacity]] - the maximum possible rate of receiving [[information]] 
- [[offered traffic]] - the amount of information a protocol is asked to transmit by  
the layer above
- [[throughput]] - the rate at which a protocol sends information to the layer above
- [[utilisation]] - the ratio of the [[throughput]] to the [[network capacity]] 
- **efficiency** - the ratio of the [[throughput]] to the [[offered traffic]] 
- **message** - an application layer [[payload]] 
- [[packet]] (and/or frame) - a group of bits that travels around together
- [[payload]] - the data part of a [[packet]] (not the [[header|headers]])
- [[header]] - information added to the [[payload]] by a protocol ([[overhead]])
- [[overhead]] - the amount of additional information that has to be transmitted to maintain network operation
### Types 
- **Best effort** - do their best to deliver packets, but don't guarantee anything 
	- Minimises energy per [[packet]] 
	- Fewer frames to transmit 
	- Smaller probability of collisions 
	- Potentially greater [[throughput]] 
- **Reliable** - will retransmit if something goes wrong, or can inform the layer above that a [[transmission]] has failed
	- Can introduce large delays 
	- Can introduce out-of-order [[packet]] delivery 
	- Uses more energy
- **Connectionless** - send individual data packets separately across a network 
- **Connection Oriented** - Establishes an end-to-end connection before sending data, providing strict quality of service requirements.

It sounds all protocols should be reliable, but you don't always need one. If a layer above is reliable, a large broadcast, or simply just not needing one are valid reasons. 
