 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-07-26]

--- 
[[Steady state error]] and the error transfer function shows how an error signal develops over time. Here, we'll look at how a disturbance affects the output over time, using [[disturbance rejection]] and a disturbance rejection transfer function.
```table-of-contents
```
---
## [[Disturbance]]
We only have closed-loop control because of [[disturbance]]; without it, a system is completely predictable.

We can model [[disturbance]] either at the input or the output of the plant, but we will look at output disturbance. 
- This could represent un-commanded changes to the system, like a physical disturbance, or sensor noise or other imprecision.

![[Disturbance Rejection.png|Modelling disturbance as an additive signal at the system output]]
 knowing $V(s)$ and $D(s)$ are independent (don't affect each other), we can use [[superposition]] to consider them separately. Assuming $V(s) = 0$:
 $$\begin{align}
Y(s) &= D(s) - G(s)H(s)Y(s) \\
(1+G(s)H(s))Y(s) &= D(s) \\
\frac{Y(s)}{D(s)} &= \frac{1}{1+G(s)H(s)}
\end{align}$$
This looks kinda similar to $\frac{Y(s)}{V(s)} = \frac{G(s)H(s)}{1+G(s)H(s)}$. If we represent the transfer functions in terms of their poles and zeros, we see:

$$\begin{flalign}
\frac{Y(s)}{V(s)} = \frac{Z(s)Z_{c}(s)}{P(s)P_{c}(s)+Z(s)Z_{c}(s)} && \frac{Y(s)}{V(s)} = \frac{P(s)P_{c}(s)}{P(s)P_{c}(s)+Z(s)Z_{c}(s)}
\end{flalign}$$
The denominators (the poles) are identical, but the zeros differ.

Poles in the output disturbance transfer function are the same as in the close-loop transfer function. This means in both functions, there are a few time-domain criteria that are based on the pole locations will also be the same:
- [[overshoot]] 
- [[settling time]] 
So if a system is disturbed, it will settle and overshoot the same time/amount as a normal input change.
## Sensor Noise 
Noise can be treated as an output disturbance, but it's continuous. Our definitions for settling time and overshoot are used for instantaneous changes. So, it might be useful to switch to the [[frequency domain]] for analysis. It also might be best analysed in the true system output, rather than the measured output.
![[Disturbance Rejection-2.png|Modelling noise as an additive signal in the feedback loop]]
Similarly to last time, $V(s)$ and $N(s)$ can be considered separately by [[superposition]], so assuming $V(s)= 0$:
 $$
\begin{align}
Y(s) &= -G(s)H(s)(Y(s) + N(s)) \\
(1 + G(s)H(s))Y(s) &= -G(s)H(s)N(s) \\
\frac{Y(s)}{N(s)} &= \frac{-G(s)H(s)}{1 + G(s)H(s)}
\end{align}
$$
- The noise transfer function is the **same** as the closed-loop transfer function.

Noise is often assumed to be **Gaussian**, where it has infinite bandwidth (every possible frequency is covered), and power density equal at all frequencies (every frequency receives the same amount of power). This mean's the noise voltage is *theoretically* unbounded, and true Gaussian noise has *technically* infinite power.
## [[Frequency Response]] 
If you remember from [[frequency response]] from Year 1, then you'd remember:
- Poles: 20dB per decade **decrease** in gain above corner frequency 
- Zeros: 20dB per decade **increase** in gain above corner frequency
- Integrators and differentiators are just poles and zeros with a zero corner frequency
Their effects are multiplicative, but are additive in decibels. [[Bode plots]] in control have frequency in radians per second (not Hz). Gain constant gives the value of the lowest frequency approximation line at $1\text{rad.s}^{-1}$. 

If we want to draw a Bode plot, we have to:
1. Prepare:
	- Calculate the gain constant by setting $s=0$ 
	- Convert the gain constant to decibels $dB = 20\log_{10}(K)$ 
	- Identify the frequencies of all [[poles and zeros]]
		- First-order: frequency is absolute pole or zero value
		- Second-order: use **natural frequency** $\omega_{n}$ (absolute distance to origin)
3. Starting the plot:
	- Look at the [[Steady State Error#System Type|System Type]] to determine the gradient of the lowest-frequency line
		- Type 0 will be $0$ dB/decade
		- Type 1 will be $+20$ dB/decade
		- Type 2+ adds on +20dB/decade
	- Move this line vertically so its amplitude at $1\text{rad.s}^{-1}$ matches the gain constant
	- This frequency and amplitude becomes the first known corner point
4. Now iterate through the poles and zeros in ascending order of frequency $\omega_{pz}$
5. Find the corner point for the pole or zero on the plot
	- Its frequency is just $\omega_{pz}$
	- For the amplitude, given a last known corner point ($\omega_{last}, A_{last}$) and gradient $m$
$$A = A_{last}+m \times \log_{10}\left(\frac{\omega_{pz}}{\omega_{last}}\right)= A_{last} + m (\log_{10}(\omega_{pz})-\log_{10}(\omega_{last}))$$
6. Update the gradient for next time
	- Zeros add $+20$ dB/decade each
	- Poles add $-20$ dB/decade each
7. Repeat for each pole or zero
### Example
$$G(s) = \frac{3(s+2)}{s^{2}+8s+20}$$
First, we know it's a Type 0 system as we can't factor out an $s$ in the denominator, so we know there's a $0$ dB/decade low frequency gradient. 

Setting $s = 0$, we get $K=0.3 \approx -10.45dB$.  So, our first corner point will be at $1\text{rad.s}^{-1}$ at $-10.45dB$. 

From increasing natural frequency, we know there's a zero at $s=-2$, so on the corner frequency will be at $\omega = 2\text{rad.s}^{-1}$. The gain at this point will still be $-10.45dB$ as the previous segment was horizontal. The gradient after this will be $20$ dB/decade, as it's a zero.

The next frequency is a pole pair, at $\omega_{n}=\sqrt{20} \approx 4.472\text{rad.s}^{-1}$, as finding the natural frequency of the denominator is in the equation  $s^{2}+2\zeta\omega_{n}​s+\omega_{n}^{2}​$. Finding the gain is a bit trickier, as we need to calculate the gain since the last corner frequency. So starting at $-10.45dB$, we're increasing $20$ dB/decade, between $\omega=4.472$ and $\omega=2$. Turning that into an equation, we get
$$-10.45 + 20 (\log_{10}4.472 - \log_{10}2) = -3.46dB$$
Which is our new altitude. And since it's a pole, it now goes down at $20$ dB/decade.

With all of this information, we can now draw our Bode plot
![[Disturbance Rejection-3.png]]