 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-08-07]

--- 
Implementing PD, PI and PID controllers is problematic. Differentiators don't actually exist, and integrators present problems if an error persists for longer than expected.

To solve this, we'll use passive compensation. 
```table-of-contents
```
---
## Differentiation 
A [[differentiator]] is bad for noise performance. Noise on $Y(s)$ will appear on $E(s)$ and will be amplified by the [[differentiator]]. To help this problem we could either:
- Filter the measured output signal $Y(s)$
- Filter the error signal $E(s)$
- Filter the differentiated error signal $\frac{dE(s)}{ds}$
Option 2 is the simplest, and also helps with the [[PD Control#Problems|set-point kick]] problem. If we use a simple low-pass filter, it's the same as adding another pole at $s = -p_{f}$ to the controller $H(s)$. 

With the filter, the PD controller structure becomes
$$H(s) = \frac{K(s+z_{pd})}{s+p_{f}}$$
- where $p_{f} > z_{pd}$ because the filter pole is chosen to be fast.

This is no longer a PD controller, this is a **phase-advance network**, or PAN. It's simply a [[PD control|PD controller]], with a low-pass filter. 


| **Advantages**                                                         | **Disadvantages**                                                                                                                   |
| ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| Reduced noise problems compared with PD                                | Doesn’t reduce the excess of poles, so asymptotes are more likely to cross the imaginary axis                                       |
| More realistic – tends to work better when implemented in real systems | More complex design procedure, as both the pole and the zero must be placed                                                         |
| Completely passive implementation (if the required gain K < 1)         | Available ‘power’ (angle contribution) reduced, so some specifications might be achievable<br>for a PD controller but not for a PAN |
The compensator pole and zero positions are linked. Together, they must contribute the correct angle to satisfy the angle criterion at the desired pole location.

If the zero moves to the left, the pole must move to the left, and vice-versa. We start the design by arbitrarily choosing a zero position. A good first guess is often to *place the compensator zero underneath the desired pole location*. Then:
- Calculate the compensator pole to satisfy the angle criterion at the desired closed-loop pole location
- Find the gain, close the loop, check the step response
- If it is not satisfactory, work out why not
- Move the zero to the left or right as necessary, and try again
### Example
*Design a [[unity negative feedback]] control system using a phase-advance network for the system*
$$G(s) = \frac{100}{2s^{2}+5s}$$
*where there's:*
- *less than $10\%$ overshoot to a unit step input* 
	- Closed-loop poles left of $\frac{4}{\alpha} = \frac{-4}{3}$
- *a settling time $T_{s} \leq 3s$* 
	- $\zeta \approx 0.5912, \cos^{-1} \approx53.75\degree$

Let's choose arbitrary poles at $s=-2 \pm 2j$

![[Phase-Advance Networks.png]]

The total angle is $\sim -121\degree$, so our compensator pole must add approximately $-59\degree$. Using $\tan$ again, we find that pole is at
$$p \approx 3.2$$
The monic form gain is $K_{m}\approx \frac{2.83 \times 2.33 \times2.06}{2}\approx 6.8$, so the additional required gain is $\frac{6.8}{50}\approx0.136$. That gets us this root locus:

![[Phase-Advance Networks-1.png]]