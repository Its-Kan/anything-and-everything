---
dateCreated: 2026-01-07 01:26
---
[Module:: [[Communication Systems and Digital Communications]]]
 
```table-of-contents
```
---
## Sending bits
Let's consider baseband [[modulation]]/coding schemes, which means modulation at its original, low-frequency range, rather than it being shifted up to higher radio frequencies for transmission. 

[[Information]] bits are transmitted across a medium by adjusting the amplitude of the signal. This mostly happens in a two-stage process:
- **Coding** - converts the stream of [[information]] bits into a stream of signalling bits more suitable for [[transmission]]. 
- **[[Modulation]]** - converts the coded bits into a set of waveforms suitable for [[transmission]].

Synchronous (serial [[communication]]) is a dedicated channel for the clock, and is used in very short-distance communication, e.g. I2C, SPI, I2S. Asynchronous is clock [[information]] is embedded with symbols, used in most long-haul communication, e.g. RS232, RS485, Ethernet, Inter-exchange [[communication]]. In this module, we'll only consider asynchronous [[communication]] schemes.  
## Choosing a scheme
There are a few requirements for a scheme:
- a low bit-[[error rate]], for a given transmit power over a specific channel. 
- AC coupling is often used for isolation, so a code needs to have a low DC content
- High-frequency content
- Ease of synchronisation
- Simplicity
- Symmetry

| **Coding Scheme**                                | **How it Works**                                                          | **Decoding**                                                                                                                                              | **Problems**                                                    |
| ------------------------------------------------ | ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Non-return to zero (**NRZ**)                     | Two distinct voltages to represent binary.                                | High is 1, low is 0.                                                                                                                                      | Long streams of 1's or 0's leads to desync and baseline wonder. |
| Return to zero (**RZ**)                          | Three voltage levels: +ve, -ve and zero, goes back to 0 after a period.   | High is 1, low is 0.                                                                                                                                      | Same issue as NRZ with 0's when unipolar, higher bandwidth      |
| Non-Return to Zero Inverted (**NRZI**)           | Encodes based on transitions                                              | 1 when there's a change, 0 when there's not (or vice versa)                                                                                               |                                                                 |
| Alternate Mark Inversion (**AMI**)               | Three voltage levels: +ve, -ve and zero, alternates between up and down.  | Non-zero is 1, zero is 0.                                                                                                                                 | Both ends don't use the same clock, causes desync.              |
| High Density Bipolar Order 3 (**HDB3**)          | Same as AMI, but four consecutive 0's are replaced with a code violation. | Zero is 0. Temporarily, non-zero is 1. V are violations (pulse doesn't alternate polarity), B correctly alternates. Replace 000V and B00V with 0000. <br> |                                                                 |
| **Manchester Coding**                            |                                                                           | Downward transition is 0, upward transition is 0.                                                                                                         | Wasteful, as it needs to fire twice for each bit.               |
| Multi-level Transmission Three-level (**MLT-3**) |                                                                           | No change is 0, any change is 1.                                                                                                                          |                                                                 |
| **Binary Block Codes**                           | Referred as nBmB, where $n$ is input bits, that produce $m$ output bits.  | Use a lookup table to retrieve the m-bit data.                                                                                                            |                                                                 |
