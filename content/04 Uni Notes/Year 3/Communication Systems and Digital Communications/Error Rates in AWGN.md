---
dateCreated: 2026-01-19 21:50
---
[Module:: [[Communication Systems and Digital Communications]]]

How do we track the performance of a [[baseband modulation and coding]] scheme? There are two performance indicators:
- [[spectral efficiency]] (bits/Hz)
- [[bit error]] rate (BER)/probability of [[bit error]] for a given [[signal to noise ratio]] (SNR)
```table-of-contents
```
---
![[Error Rates in AWGN.png]]
## Assumptions 
To determine the theoretical minimum BER, you should assume the following conditions:
- The channel is linear, and doesn't introduce any distortion to the transmitted signal 
- The bit stream has an equal probability for ones and zeros. 
- No attenuation in the channel
## A Channel
Let's look at a channel.
### No signal
![[Error Rates in AWGN-1.png]]

This is where no signal sent down the channel, and it's just noise. We just get [[Additive White Gaussian Noise]]. 
### 1 received with noise 
![[Error Rates in AWGN-2.png]]

When a 1 is received, the signal "shifts" up, and the mean of the Gaussian probability density function is $A$. Due to noise, there is a probability that a 1 gets decoded as a 0.
### 0 received with noise
![[Error Rates in AWGN-3.png]]

When a 0 is received, the signal "shifts" down, and the mean of the Gaussian probability density function is $-A$. Due to noise, there is a probability that a 0 gets decoded as a 1.
## Optimum SNR 
As we saw in [[Matched Filter]], the optimum instantaneous [[signal to noise ratio]] after the receive filter depends on the total energy per transmitted symbol, and noise power spectral density:
$$\text{SNR}_{\text{opt}} = \frac{2E_{S}}{N_{0}}$$
This expression is only valid when:
- The symbol is sampled at the optimum time (T) 
- The receive filter is the optimum (matched) filter
- The delay through the receive filter is sufficient to allow all the energy in the received pulse to arrive
- The noise is white
- There's no inter-symbol interference
## Gaussian Distribution 
[[Additive White Gaussian Noise]], as a reminder, has a Gaussian probability distribution with a zero mean value. If it's filtered linearly, it'll still have a Gaussian distribution, but no longer white. Filtered noise added to a constant signal, results in a Gaussian distribution with a mean equal to the amplitude of the signal.
$$p(x) = \frac{1}{\sqrt{2 \pi \sigma}} \exp $$
### Q-function
For any zero-mean Gaussian distribution, the mean power is $\sigma^{2}$. We can use the **Q-function** to calculate the probability that the noise amplitude will exceed a specific threshold, which determines our error probability: 
$$\begin{align}
P_{x}(x>X) &= Q\left(\frac{X-a}{\sigma}\right) \\
\text{where} \quad Q(z) &\approx \frac{1}{z \sqrt{2\pi}}\exp(\frac{-x^{2}}{2})
\end{align}$$
- where $a$ is the mean (signal amplitude)
- and $\sigma$ is the standard deviation (noise power)
![[Error Rates in AWGN-4.png]]
## Polar Scheme
The optimum [[signal to noise ratio]] ($\text{SNR}_{\text{opt}} = \frac{2E_{S}}{N_{0}}$) represents a quality of the environment, it tells us how strong the signal is compared to the noise. This results in the bit error rate ($\text{BER}$), and tells us the percentage of the data actually made it through correctly. Noise amplitude has a Gaussian Probability Distribution. For polar signalling, the symbols "0" maps to "-A", and "1" maps to $+A$. The BER calculated is the theoretical minimum. 
- Average signal power: $A^{2}$
- Noise power: $\omega^{2}$
- Therefore the signal-to-noise ratio is also $\frac{A^{2}}{\sigma^{2}}$

The probability of a [[bit error]] is:
$$\begin{align}
P_{x}(x > \text{Threshold}) &= Q \left(\frac{\text{Threshold}-\text{Mean}}{\sigma}\right) \\ 
P_{e} &= Q(\sqrt{\frac{2E_{s}}{N_{0}}})
\end{align}$$
- or in words, this is the probability that random noise will be strong enough to cause a decoding error, is the Q-function 
![[Error Rates in AWGN-5.png]]
## Unipolar Scheme
For polar signalling, the symbols "0" maps to "0", and "1" maps to $+A$. The BER calculated is the theoretical minimum. A unipolar scheme is similar, however since the signals are closer together (as we're not considering $-A$), the threshold is halved/
$$P_{e} = Q(\sqrt{\frac{E_{s}}{N_{0}}})$$
HOWEVER, at large values of $\frac{E_{S}}{N_{0}}$ (small values of BER) the difference in transmitted power to achieve the same levels of BER is about 3dB. People often speak of a "3dB penalty" when using unipolar modulation.
![[Error Rates in AWGN-6.png]]