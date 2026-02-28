 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-07-18]

--- 
This is the start of basic control! We'll look at analytic control for some simple systems, as well as [[steady-state error]]  and [[error constants]].
```table-of-contents
```
---
## [[unity negative feedback|Unity Negative Feedback]]
As a reminder, here's the equation for a [[closed-loop transfer function]], $T(s)$
![[unity negative feedback.png]]
$$
\boxed{T(s) \triangleq \frac{Y(s)}{V(s)} = \frac{G(s)H(s)}{1+G(s)H(s)
}} 
$$
If we write the [[plant]] and the controller in terms of its zeros and poles, we get:
$$
T(s) = \frac{\frac{Z(s) Z_c(s)}{P(s) P_c(s)}}{1 + \frac{Z(s) Z_c(s)}{P(s) P_c(s)}} = \frac{Z(s)Z_c(s)}{P(s)P_c(s) + Z(s)Z_c(s)}
$$
> [!note]
> For a general $G(s)$ (plant) and $H(s)$ (controller), where is **no way** to determine analytically the roots of the denominator of $T(s)$ (transfer function). 
> 
> Roots of $Z(s)$ are also the roots of $Z(s)Z_{c}(s)$, so under feedback, the zeros are **invariant**. If you know the zeros of the individual components, you know the zeros of the final system.
## Gain
Let's look at the simplest possible controller: the simple gain, $H(s) = K$. If the [[error signal]] is large, then we multiply the signal by $K$, like a car stepping on the throttle proportionally to the amount it slows down. Substituting into the equation we get either:
$$
\begin{align}
T(S) &= \frac{KG(S)}{1+KG(S)} \\
&= \frac{KZ(S)}{P(s)+KZ(S)}
\end{align}
$$
This gives us a quick method for finding the [[closed-loop transfer function]]  when a simple gain is used.

> [!example]
> Using the analogy of a plane:
> - The [[plant]], $G(s)$, output is the plane's current altitude.
> - The external input (the output we want) is an altitude demand.
> - The system input (the thing we want to change) is the angle of the wing flaps
> - When the flaps rise, the angle of attack will increase, so lift will increase and thus the altitude will increase.
> - The amount of elevator movement for a given altitude error (the change we want) is the **controller gain**
> - Having more controller gain (higher $K$) can mean the system responds/settles quicker, but will introduce overshoot/oscillating behaviour, ergo less stability. Inversely, less controller gain (lower $K$)
## Simple Control
For [[plant|plants]] with simple [[transfer function|transfer functions]] it's possible to derive a gain algebraically. 

$$G(s) = \frac{30}{2s^{2}+17s + 30}$$
Setting $G(s) = 0$ to find how it settles, we get poles at $s=-6$ and $s=-2.5$. 
- As both poles are negative, we know the system is stable, and will eventually settle to 0.
- As both poles are real, we know the system won't oscillate, and will decay exponentially.

Now, let's say the system has a 10% overshoot when given a unit step. Using the overshoot percentage formula, we find that $\zeta \approx 0.5912$.    

As we know, $T(s) = \frac{KZ(s)}{P(s)+KZ(s)}$ for $G(s) = \frac{Z(s)}{P(s)}$, we multiply the numerator by the DC gain, then add the numerator to the denominator. For our system, we can write it as:
$$
\begin{align}
&\frac{30K}{2s^{2}+17s+30+30K} \\
= & \frac{30K}{2s^{2}+17s+30(K+1)}
\end{align}
$$
Let's calculate $K$ now. We know the general formula of the denominator can be written as $s^{2}+2 \zeta\omega_{n}s + \omega_n^2$, so we could equate it to our denominator, however the second order terms aren't equivalent, so we can multiply it all by $2$, to get
$$2s^{2}+17s + 30 (K+1) = 2s^{2}+4\zeta \omega_{n}s + \omega_n^2$$
Comparing the coefficients, we can equate $4 \zeta \omega_{n}=17$ to get $2\omega_{n}^{2} \approx 103.36$, and $30(K+1) \approx 103.36$ to get $K \approx 2.445$. Substituting this back into the equation, we get
$$T(s) \approx \frac{73.36}{2s^{2}+16s +103.36}$$
We can now accurately calculate DC gain, poles and settling time!