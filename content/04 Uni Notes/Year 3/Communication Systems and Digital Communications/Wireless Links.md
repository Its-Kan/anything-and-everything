---
dateCreated: 2025-12-14 19:36
---
[Module:: [[Communication Systems and Digital Communications]]]
 
In wireless communications, we need to ensure a [[signal]] sent from Point A actually reaches Point B. To do this, we can use link budgets!
```table-of-contents 
```
---
## Introduction
A radio link needs to be designed to operate within an adequate received [[signal to noise ratio]] (SNR), in which we where we calculate a [[link budget]]. If there are any interfering signals, we use signal to
## Initial Link Budget
Link budgets are used to design a link, and investigate trade-offs. For example for a:
- required received power (how much power do I need?) 
- required [[signal to noise ratio]] (how much louder should the signal be than static?)
- for a given communication range (how far apart can the receiver and transmitter be?)

They can also be used to analyse the performance of a link, through mapping the [[signal to noise ratio]], to a [[bit error]] rate or [[packet loss]] rate (how often will data errors occur at this signal quality?).

To do this, we'll need a set of system and link parameters:
- Transmit power 
- Antenna parameters, like gain
- Receiver noise levels, like its noise temperature 
- And other factors, such as propagation losses
### Antennas 
Let's consider a theoretical isotopic antenna, which radiates equally in all directions. A sphere!

Since it radiates equally, it follows the inverse square law, so the [[power flux density]] (PFD) on the surface on the sphere is calculated via the according formula. Assuming the transmit power, $P_T$ stays constant, for every $d$ meters away from the antenna you are, the PFD drops by a factor of $d^2$.

![[Wireless Links.png]]

But in reality, we don't want to transmit a signal in all directions, we want to concentrate the power in a single direction. To do this, real antennas have gain, which "pulls" the isotropic antenna in a direction, and is relative to the isotropic antenna in units of dBi (decibels relative to isotropic). At the centre, there is 0dBi. 

![[Wireless Links-1.png]]

#### Radiation Patterns
We can represent how an antenna distributes its energy into space graphically, where the y-axis is the relative power or field strength, and x-axis is the angular direction in radians. The centre point (0) is the **bore sight direction**, where the antenna is "aimed" towards, and has the maximum signal strength. The pattern may be different if we're measuring in azimuth (top-down view) or elevation (side-on view).

Surprisingly, the main beam isn't the only beam that's transmitted, smaller side lobes are radiated too, in directions that are undesired. We try to minimise these to reduce interference. 

![[Wireless Links-2.png]]

![[Wireless Links-3.png]]

#### Gain and Directivity
Gain be defined as:
$$\text{Gain} = \frac{\text{Max. power density radiated by the antenna}}{\text{Power density radiated by a perfect isotropic antenna with the same input power}}$$
And directivity can be defined as:
$$\text{Directivity} = \frac{\text{Max. power density radiated by the antenna}}{\text{Avg. power density radiated by the antenna}}$$
If an antenna has no losses and is virtually perfect, then gain and directivity are the same thing. Otherwise:
$$\text{Gain} = \text{Directivity} \times \text{Efficiency}$$
### Simple Links
Let's look at a simple link between a transmitter, $Tx$, and receiver, $Rx$, separated by a distance $d$. 

![[Wireless Links-4.png]]

The power flux density (strength of the transmitter) in the wanted direction is increased by a factor if $G_T$. At the receiver, the approaching signal could be simplified into an isotopic antenna, with power $P_{T}G_{T}$, which is called the **Effective Isotropic Radiated Power (EIRP)**
$$PFD_{\text{realAntenna}} = \frac{P_{T}G_{T}}{4 \pi d^{2}} \space \text{w/m}^2$$
When the signal is sent, it arrives at the receiving antenna as a "cloud" of energy called the **incident [[power flux density]]**, which is dependent on how much of the antenna captures the [[signal]]. The [[effective aperture]] ($A_{e}$) is the *functional* capturing area of the antenna. Of course, the antenna doesn't work 100% efficiently, so the aperture efficiency ($\eta$) dictates how much of the *actual* aperture ($A_{\text{actual}}$) is used. :
In maths:
$$\begin{align}
P_{R} &= PFD_{\text{realAntenna}} \times A_{e} \quad\\
&= \frac{P_{T}G_{T}}{4 \pi d^{2}} \times A_{e}
\end{align}$$
- where $A_{e}$ is the effective aperture, and $P_{R}$ is in watts.
$$A_{e} = \eta \times A_{\text{actual}}$$
- where $\eta$ is the aperture efficiency, and $A_{e}$ is in meters squared.
### Free Space Path Loss
Between any two antennas, the signal isn't transmitted perfectly, and there will be some loss. To make up for this in equations, we add **FSPL**, which is a [[Dimensional Analysis|dimensionless]] quantity measured in $dB$, and is a function of range and wavelength.

To model this, we use a **Zeroth order model**, which assumes the transmitter creates a "cloud" of energy that spreads out in a cone, which means the receiver only captures a portion of this signal. It does not take into account frequency, atmospheric interference or antenna efficiency, purely physical space. 

Simply, the bigger the dish (or smaller coverage) implies more power, and a higher data rate.

![[Wireless Links-5.png]]

This ratio of energy that gets captured is calculated by:
$$\frac{P_{R}}{P_{T}}= \frac{\text{Dish aperture}}{\text{Coverage area}}$$
This only works for unobstructed, clear lines of sight. Most environments in the real world introduce reflections, scattering, diffraction and absorption. To account for this, our channel model will be in the form:
$$\text{Loss(dB)} = K + 10 \cdot \gamma \cdot \log_{10}(d) + \eta$$
- where $K$ is the loss from a reference distance 
- $\gamma$ is the *path loss exponent*, and is usually around 4 in urban environments
- $\eta$ is a normally-distributed random variable, with 0 mean and a standard deviation between 8 and 12.
### Noise and Interference
There are two sources of power that cause problems in communications.
- Noise is power picked up from the environment, even when no-one is transmitting intentionally (due to the thermal movement of electrons).
- Interference is power picked from anyone transmitting at he same time that you don't want to listen to.

![[Wireless Links-6.png]]
## Completing the Link Budget
The ratio of useful power, to unwanted power determines whether a [[frame]] can be received or not, basically determines how reliable a communication link is. There's a few metrics that can show this:
- **SINR** (Signal-to-Interference-plus-Noise Ratio) accounts for noise and interference:
$$\text{SINR} = \frac{\text{Signal} \space (W)}{\text{Interference} \space (W) + \text{Noise} \space (W)}$$
- **SIR** (Signal-to-Interference Ratio) is used when background noise is negligible
$$\text{SIR} = \frac{\text{Signal} \space (W)}{\text{Interference} \space (W) }$$
- **SNR** (Signal-to-Noise Ratio) is used in a point-to-point budget, where there are no other transmitters interfering, and we only care about the signal relative to background noise.
$$
\begin{align}
\text{SNR} &= \frac{\text{Signal}}{\text{Noise}}  \\
\text{SIR(dB)} &= \text{Signal(dBm)} - \text{Noise(dBm)}
\end{align}
$$If we don't know the receiver [[bandwidth]], then we can calculate the link budget as a density ratio ($C / N_{o}$), where $C$ is the carrier power, and $N_{o}$ is noise power spectral density (noise power per $1Hz$ of bandwidth). We can calculate it by subtracting all the losses from the total signal power,
$$\begin{align}
\frac{C}{N_o} &= \frac{P_R}{k \cdot T_N} = P_T + G_T - 20 \log \left( \frac{4 \pi d}{\lambda} \right) + G_R - k - T_N \quad \text{dB-Hz} \\
\frac{C}{N_o} &= EIRP - FSPL + G_R - k - T_N \quad \text{dB-Hz}
\end{align}$$
- where $\frac{C}{N_o}$ is carrier-to-noise density ratio
- $P_{R}$ is the received power
- $k \cdot T_{N}$ is the noise density ($N_{o}$), which is $k$ Boltzmann's constant and $T_{N}$ is the noise temperature
- $EIRP$ is the effective isotropic radiated power, calculated as $P_{T} + G_{T}$
- $FSPL$ is the free space path loss, represented by  $20\log \frac{4\pi d}{\lambda}$

Radio modems are usually specified using $C/N_{o}$ as you want to estimate your achievable [[bit rate]] ($R_{b}$), as
$$\begin{align}
\text{Carrier (signal) power} &= \text{Energy per bit} \times \text{Number of bits per second} \\
C &= E_{b} \cdot R_{b}  
\end{align}
$$
Or with noise density ($N_{0}$) it's:
$$
\frac{C}{N_{0}}= R_{b} \cdot \frac{E_{b}}{N_{0}} \quad \text{or in dB units:} \quad \frac{C}{N_{0}}= R_{b}+ \frac{E_{b}}{N_{0}} 
$$A higher bit rate will need a better $C/N_{o}$, while a lower bit rate can get away with a lower one.