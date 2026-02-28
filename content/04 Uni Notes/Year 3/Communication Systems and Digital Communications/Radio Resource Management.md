---
dateCreated: 2026-01-05 16:55
---
[Module:: [[Communication Systems and Digital Communications]]]

RRM is a function to control and assign resources at the system/network level. Its purpose is to increase system spectral efficiency, or how effectively a system uses its assigned frequency spectrum to transmit data. For example, some functions include:
- Channel allocation at the network, base station and user level
- Selection of modulation and channel coding parameters 
- Managing handover in mobile systems
Static RRM is based on manual or computer aided planning, while dynamic RRM adapts in response to changing conditions.  
```table-of-contents
```
---
## RRM
### Connection Admission Control 
CAC is concerned with regulating access to a [[communication system]]. It determines whether there are sufficient resources available to admit the new connection. 
- Is there a channel available? 
- Can the new connection be accepted with its required quality of service? 
- Will the quality of existing connections be impaired by the new connection?
Connection request refusal results in **blocking**, and if a connection severely degrades the link quality of others, it may be **dropped**.
### Channel Assignment
This refers to the process of assigning channels to part(s) of a network and/or individual users. The objective is to maximise system spectral efficiency whilst meeting quality of service requirements. Applies to frequencies, time slots, spreading codes, etc. Fixed channel assignment refers to the allocation of a predetermined set of resources, while dynamic channel assignment refers to the flexible allocation of channels based on time varying needs. 
### Medium Access Control 
MAC is concerned with coordinating and regulating access to a shared channel. It specifies when nodes should transmit frames and manages addressing.
## Multiple Access Techniques

| **Technique**                                 | **Description**                                                    | **Key Features**                                                        |
| --------------------------------------------- | ------------------------------------------------------------------ | ----------------------------------------------------------------------- |
| **FDMA** - Frequency Division Multiple Access | Users transmit on different frequencies.                           | Simple, reliable for constant bit rate; needs guard bands.              |
| **TDMA** - Time Division Multiple Access      | Users transmit at different times on one frequency.                | Highly flexible for variable bit rates; needs accurate synchronization. |
| **CDMA** - Code Division Multiple Access      | Users transmit simultaneously on one frequency using unique codes. | No hard capacity limit; simplifies network design.                      |
| **CBA** - Contention-Based Access             | Users transmit on a common frequency at any time.                  | Simple and distributed; suffers from stability and collisions.          |