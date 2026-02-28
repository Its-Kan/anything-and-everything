---
dateCreated: 2026-01-15 17:23
---
[Module:: [[Communication Systems and Digital Communications]]]

Let's say we have a train of impulses $x(t)$, which passes through a transmit filter $h(t)$. The receiver receives the signal, with some [[Additive White Gaussian Noise]]. We want to design a filter $r(t)$, that ignores the noise, and focuses on the signal, $y(t) = h(t) \cdot r(t)$. What's the optimal filter to use that best minimises the [[signal to noise ratio]]? The goal of the receiver is to maximise the signal power exactly when we measure it 
1. A series of impulses are sent 
2. $h(t)$ shapes the signal to allow it to travel through a medium 
3. AWGN is added somewhere in the channel 
4. The receiver $r(t)$ "un-modulates" the signal to get the original impulse again
```table-of-contents
```
---
## Optimum Filtering
Optimum in this case means achieving the highest possible [[signal to noise ratio]]. 
- The [[signal]] is measured as the instantaneous power at the sampling moment. 
- The noise is measured as the mean power of the noise over time, which should always be constant. 
- The sampling time is the time the system "decides" to take a snapshot of the signal and tracks it as an impulse. Of course it can't be $t=0$ as the energy hasn't arrived to the receiver yet, so we have to wait for a duration $T$ before sampling. 
We want to design a filter where the [[signal to noise ratio]] peaks after time $T$. 

Maths time! Given a signal of shape $h(t)$ (transmitter's output), and a receive filter of impulse $r(t)$, a [[convolution]] of both gets us the output at the receiver $y(t)$.
- Output of the receiver:
$$y(t) = h(t)*r(t) = \int^{\infty}_{- \infty} r(\tau)h(t- \tau) \space d \tau$$
- Noise power after a receiver with an impulse response $r(\tau)$
$$\text{Noise} = \frac{N_{0}}{2} \int^{\infty}_{- \infty} r^{2}\tau \space d \tau $$
- Therefore, the [[signal to noise ratio]] as some time $T$ can be expressed as
$$\text{SNR} = \frac{2 \vert \int^{\infty}_{- \infty} r (\tau) h (T- \tau) \space d \tau \vert^{2}}{N_{0} \int^{\infty}_{- \infty} r^{2}(\tau) \space d \tau}$$
We interested in finding a receive filter $r(\tau)$, where the SNR is maximised. What shape of filter allows us to maximise the signal to be the loudest over noise?
### Schwarz Inequality
The SNR equation is quite messy. What if we could abstract parts of it, and have a rule that let's us check if the filter is designed optimally? That gives us the [[Schwarz Inequality]]. Generalising $r(\tau)$ to $a(t)$, and $b(t)$ to $h(T-\tau)$, we have this equation:
$$
\left| \int_{-\infty}^{\infty} a(t)b(t) \, dt \right|^2 \le \int_{-\infty}^{\infty} |a(t)|^2 \, dt \int_{-\infty}^{\infty} |b(t)|^2 \, dt
$$
When this equality is true, $a(t) = kb(t)$, where $k$ is a constant. Rearranging, we get
$$
\left. \frac{\left| \int_{-\infty}^{\infty} a(t)b(t) \, dt \right|^2}{\int_{-\infty}^{\infty} |a(t)|^2 \, dt} \right|_{MAX} = \int_{-\infty}^{\infty} |b(t)|^2 \, dt
$$
Optimum SNR occurs when the Schwarz inequality gets us $r(\tau) = kh(T-\tau)$. In other words, the receive filter's impulse response should be the time-reverse of the transmit filter's impulse response, possibly weighted by some factor $k$. The filter that satisfies this is called a [[Matched Filter]].
### Time and Frequency Domains
The impulse response of the receiver filter should be the **time reverse** (mirrored across the y-axis) of the transmitter's impulse response. This means the peak of the signal lines up at the sampling time, maximising SNR.
$$
r(\tau) = kh(T-\tau)
$$
The constant $k$ represents gain applied to both the signal and noise, so it cancels out when put in the SNR equation, and has no effect. If the Tx filter is symmetrical in time, then the Tx and Rx filter should be identical. 

In the frequency domain, if the transmit filter $h(t)$ has a Fourier transform $H(\omega)$, then the Fourier transform of the optimum receive filter $r(t)$ is:
$$R(\omega) = \exp(-j \omega T) H*(\omega)$$
The amount of energy that the receive filter lets through at each frequency is equal (or at least proportional) to the amount of energy in the received waveform at that frequency. If a lot of energy at a certain frequency comes through, the higher the gain will be at that frequency. And the opposite for less energy.
### Polar Modulation 
When the receiver "decides" what bit is being sent after a decision time (T), it has to read the **instantaneous** signal power (S) at that time.
$$S=(E_{S})^{2}$$
- where $S$ is the signal power
- $E_{S}$ is the square of the energy in the transmitted symbol (assuming there's not loss)

So, the signal to noise ratio will be:
$$\text{SNR}= \frac{2E_{s}}{N_0}$$

![[Matched Filter-1.png]]