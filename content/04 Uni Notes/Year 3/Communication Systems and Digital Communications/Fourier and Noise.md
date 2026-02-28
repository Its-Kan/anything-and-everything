---
dateCreated: 2026-01-06 22:50
---
[Module:: [[Communication Systems and Digital Communications]]]

We need to represent signals and systems in both the time and frequency domains. [[Fourier series]] and transformations can be used as a tool to convert between the two domains; series for periodic signals, and transformations for aperiodic/random signals. 
```table-of-contents
```
---
## Fourier
### Fourier Series 
Any real or complex periodic signal can be represented by an infinite summation of harmonically related, continuous sine and cosine functions. 

![[Fourier series]]

### Fourier Transform 
The [[Fourier transform]] is  used for an aperiodic time domain signals. 
![[Fourier transform]]
### [[Parseval's Theorem]] 
![[Parseval's Theorem]]
## Noise
### AWGN
 We'll mostly cover [[Additive White Gaussian Noise]] (AWGN) in this module. 
 - **Additive** meaning noise is added or superimposed on the signal via addition
 - **White** is a frequency domain characteristic. It has a constant noise power spectral density (PSD), which means the voltage at any one time for a given frequency is random (with a Gaussian probability), but the average power density is consistent.
	- Usually, we talk about PSD in a single-sided sense, where power is spread from $0$ to $+\infty$. However for analysis, we can express it as a double-sided PSD, which is spread from $-\infty$ to $+\infty$.
- **Gaussian** means that the time domain amplitude is a random variable with the Gaussian distribution. The mean is zero, and mean power is the variance ($\sigma^{2}$).
### Non-WDGN noise
- Coloured Gaussian noise is where the amplitude is still Gaussian, but noise samples at two different times are correlated. It's putting WGN through a [[LTI systems]].
- White non-Gaussian noise is where we get every frequency again, but its more uniformly distributed noise.
- Impulse noise 
- Interference 