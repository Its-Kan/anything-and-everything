---
dateCreated: 2026-01-21 23:48
---
[Module:: [[Communication Systems and Digital Communications]]]

A transmitted signal has modifiable properties that can be [[modulation|modulated]], such as amplitude in [[Baseband Modulation and Coding|baseband modulation]] or amplitude and phase in passband modulation. Any quantity with two independent components can be represented with a complex number. We can still apply the theory developed for baseband modulation, as long as they're valid for complex quantities.   
```table-of-contents
```
---
![[Equivalent Baseband.png]]

- The baseband modulation is the original data signal, at low frequencies near 0Hz. We can measure bandwidth, [[signal to noise ratio]] and the [[bit error]] rate to ensure the data stays intact.
- Ultimately, we'll modulate the [[signal]] to a higher frequency with passband modulation to transfer the signal. 
- To make the maths easier, we can use a shortcut with the equivalent baseband, where we treat the passband modulation as it's near 0Hz, treating it as an [[LTI systems|LTI system]]. 

We now have to extend communication theory to handle complex signals and system, using  [[Fourier Transforms]] to convert between the time and frequency domain, to show how the equivalent baseband representation relates with the passband.
## [[Matched Filter|Matched Filtering]] of Complex Signals 
In the equivalent baseband impulse response of the transmit filter $h(t)$ can be complex. Thus, the optimum receive filter is $g(t) = h*(t-\tau)$.
![[Equivalent Baseband-1.png]]

With a [[Matched Filter]], we can show that the optimum signal to noise ratio for a complex signal is:
$$\text{SNR} = \frac{2E_{S}}{N_{0}}$$
## Complex representation of amplitude and phase
Any passband signal can be expressed in terms of a carrier frequency, where $x_{E}(t)$ is known as the equivalent baseband representation of the signal. 
$$
x(t) = \mathbb{R}\{ x_{E}(t)\exp(j \omega_{c}t) \} \qquad x_{E}(t)=A(t)\exp(j \phi(t)) 
$$
The equivalent baseband representation of the signal is just the difference between the signal and the unmodulated carrier expressed in complex form. 

![[Equivalent Baseband-2.png]]

The following are the time-domain signal, frequency-domain signal, the noise power spectral density (power of the white noise per hertz) and energy per symbol.
- Real signals: $x(t) \space X(\omega) \space N_{0} \space E_{S}$
- Equivalent baseband signals: $x_E(t) \space X_E(\omega) \space N_{0E} \space E_{SE}$

![[Equivalent Baseband-3.png]]