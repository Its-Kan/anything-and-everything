---
dateCreated: 2026-01-20 17:55
---
[Module:: [[Communication Systems and Digital Communications]]]

There are three main steps to transmit a signal over air:
1. A pure carrier is generated at the transmitter 
2. The carrier is [[modulation|modulated]] with the information to be transmitted. Any change in signal characteristics can carry [[information]]. 
3. At the receiver, the signal modifications or changes are detected and demodulated
```table-of-contents
```
---
## A wireless modem
![[Transceivers.png]]

Let's break this down step by step.
### Transmit Chain 
![[Transceivers-1.png]]
- **Crystal oscillators** are used as frequency references, can provide good frequency accuracy and low phase noise (frequency remains constant).
- **Frequency synthesisers** takes the stable frequency reference then produces a higher "carrier frequency", as crystal oscillators can't reach high frequencies. 
- **Baseband modulator** takes the baseband signal, and generates signals that can modify the carrier frequency (amplitude, frequency or phase)
- **Up-converter** combines the carrier frequency and the modulated baseband signal. 
![[Transceivers-2.png]]
- **Power control** allows dynamic adjustments to signal strength to adhere to CDMA standards.
- **Control amplifier** tend to be more efficient rather than flexible. Tend to produce harmonics, hence a **transmit filter**
- **Switch** toggles the antenna between the transmitter and receiver. 
### Receiver Chain
![[Transceivers-3.png]]
- **Preselection filter** focuses on a single range of frequencies 
- **Low noise amplifier** boosts signal, introducing as little noise as possible 
- **Down converter** shifts the signal down to the original baseband frequencies 
- **Synchroniser** compensates the difference between crystal oscillators 
- **Demodulator** recovers the original baseband signal 
### Modulation 
![[Transceivers-4.png]]
- **Amplitude modulation** can be simply an amplifier with a gain controlled by the baseband signal. 
- **Frequency modulation** can be done by allowing the baseband signal to change the frequency output by the frequency synthesiser directly. 
- **Phase modulation** is hard to generate, but very common.