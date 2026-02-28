 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-04-17]

--- 
We'll look at the effect of complex poles, most simply exhibited in 2nd order systems, as well as introducing some of the terminology around the location of poles. 
```table-of-contents
```
--- 
## Reminder
In [[System Properties - First Order]], we saw that poles affect the system modes, and zeros affect the residues. In order to be stable (aka the system is decaying), the poles must be in the left half of the s-plane. These poles are either real, or in a complex conjugate pair. 

From the exponential form of cos and using the [[Laplace Transforms|Laplace transform]] :
$$\begin{align}
\cos \omega t &= \frac{1}{2} \left( e^{j\omega t} + e^{-j\omega t} \right) \\
\mathcal{L} \left[ \cos \omega t \right] &= \mathcal{L} \left[ \frac{1}{2} \left( e^{j\omega t} + e^{-j\omega t} \right) \right] \\
&= \frac{1}{2} \left[ \frac{1}{s - j\omega} + \frac{1}{s + j\omega} \right] \\
&= \frac{s}{s^2 + \omega^2}
\end{align}$$
Where are the poles in this equation? Seeing from the third line or from factorising the fourth line, we can get $s=\pm j \omega$ as the poles. This would where the poles be if a system has the impulse response of $\cos (\omega t)$.

> [!hint]- Why?
> The [[transfer function]] of a system is the [[Laplace Transforms|Laplace transform]] of it's impulse response, and vice versa.

This implies complex poles indicate oscillations.

If we have this system, and complete the square to get it into a form that looks like a form in the Laplace tables we get: 
$$\begin{align}
G(s) &= \frac{9}{s^{2} + s + 9} \\
&= \frac{18}{\sqrt{35}} \cdot  \frac{\frac{\sqrt{35}}{2}}{(\frac{s+1}{2})^{2} + \frac{35}{4}}
\end{align}$$
We find in the tables there's a form where the numerator has the square root of the trailing coefficient in the denominator. This is why we factor out a $\frac{18}{\sqrt{35}}$ to get it into this form. We find it has the impulse response of:
$$ g(t) = \frac{18}{\sqrt{35}} e^{\frac{-t}{2}}\sin (\frac{\sqrt{35}}{2} t)$$

Analysing this, we can find the poles by solving $s^{2} + s + 9$, which turns out to be $s \approx -0.5 \pm 2.98j$. The exponential decay in $e^{\frac{-t}{2}}$ has a time constant of $2s$. And it appears to oscillate every $\frac{\sqrt{35}}{2} t$, or around $2.98 \text{rads}^-1$. We get an impulse response that looks like this:

![[System Properties - Second Order.png]]
## General Form
It's a bit messy, but we can break it down:

$$G(s) = \frac{K_{dc} \omega^{2}_{n}}{s^{2} + 2 \zeta \omega_{n} s + \omega ^{2}_{n}
}$$
- $K_{dc}$ is the [[DC gain]] 
- $\zeta$ is the [[damping ratio]]
- $\omega_{n}$ is the **undamped natural frequency**
	*Notice there are no zeros in the standard form as the numerator is a scalar.*

Using the quadratic formula, we can calculate the poles:
$$s = - \zeta \omega_{n} \pm j \omega_{n} \sqrt{1-\zeta^2}$$
Let's define some more things to simplify this a little
$$\begin{align}
\text{let} \quad s &\triangleq - \alpha + j \omega_{d}\\
\text{where} \quad \omega_{d} &= \omega_{n} \pm \sqrt{1- \zeta^{2}}
\end{align} $$
- $\omega_{d}$ is the **damped natural frequency**
- $\alpha$ doesn't really have a name, it's just the real part of the pole location

> [!success]+ Remember this diagram
> ![[System Properties - Second Order-1.png|508]]
## [[Step Response]] 
As a reminder, the [[Step Response|step response]] is simply the transfer function multiplied by the unit step ($\frac{1}{s}$) in the [[s-plane]]. 
$$\begin{align}
Y(s) &= G(s)U(s) \\
&= \frac{\omega^{2}_{n}}{s(s^{2}+ 2 \zeta \omega_{n} s + \omega^2_n)}
\end{align}$$
- We can fix the DC gain of 1 here. In this module, all of the systems are linear, so if the DC gain is different, we can just scale it.

We can simplify by completing the square
$$= \frac{\omega_{n}^{2}}{s((s+ \alpha)^{2)}+ \omega_{d}^{2}}$$
We can then use partial fractions to get it in the form, and then splitting the fraction to get it into a form that's in the tables.
$$ Y(s) = \frac{1}{s} - \frac{s + \alpha}{(s+ \alpha)^{2} + \omega^{2}_{d}} -\frac{\alpha}{(s+ \alpha)^{2} + \omega^{2}_{d}}$$
However as we said earlier, the tables want the numerator to be the square root of the trailing coefficient in the denominator. We can multiply by $\frac{\alpha}{\omega_d}$, getting us
$$ Y(s) = \frac{1}{s} - \frac{s + \alpha}{(s+ \alpha)^{2} + \omega^{2}_{d}} - \frac{\alpha}{\omega_{d}}\cdot\frac{\alpha}{(s+ \alpha)^{2} + \omega^{2}_{d}}$$
And then finally, using the tables to convert back to the time domain gets us
$$y(t) = 1 - e^{-\alpha t} \cos(\omega_{d}t) - \frac{\alpha}{\omega_{d}} e^{\alpha t} \sin(\omega_{d}t)$$
Doing uh. Maths. To gather the cos and sin into one using the $\omega_d$ definitions gets us
$$\begin{align}
y(t) &= 1 - \frac{e^{\zeta \omega_{n} t}}{\sqrt{1-\zeta^{2}}} \sin (\omega_{d} t + \phi) \\
\text{where} \quad \phi &= \tan^{-1}(\frac{\sqrt{1-\zeta^{2}}}{\zeta})
\end{align}$$
Ok. Why would you do this? The equations show us a decaying sinusoid.
- $\zeta$, the [[damping ratio]], dampens the decay. The higher the damping ratio, the faster the system will decay.
## [[rise time|Rise Time]]
For second order systems, we can't find the [[rise time]] algebraically, but there is a table of rise times available. If we do want to use algebra, the best we can do is make a conservative (over)estimate for underdamped systems only. 

Looking at the [[Step Response|step response]] equation again, we're going to try to find the time it takes to get from 0 to 100% the first time.
$$
\begin{align}
y(t) &= 1 - \frac{e^{\zeta \omega_{n} t}}{\sqrt{1-\zeta^{2}}} \sin (\omega_{d} t + \phi)
\end{align}
$$
We can set $y(t) = 0$ and $1$ to find these values. Starting with substituting $1$, we can subtract that from both sides and bring the $\sin$ component over, and then divide the constant, leaving us with
$$0=\sin(\omega_{d}T_{r} + \phi)$$
We know $\sin$ repeats every $\pi n$ rad. $\phi$ is between $0$ and $\pi$ rad, so the solution can't be $0$, so we can set it to the next value of $\pi$
$$\pi = \omega_{d}T_{r} + \phi$$
Rearranging for $T_{r}$, then substituting $\phi$ for it's definition finally gets us
$$\boxed{T_{r} = \frac{\pi - \tan^{-1}(\frac{\sqrt{1-\zeta^{2}}}{\zeta})}{\omega_{d}}}$$
- **YOU DON'T NEED TO REMEMBER THIS!**

This will be an overestimate of rise time, but it's not bad for small values of $\zeta$.
## [[settling time|Settling Time]]
More useful measure than rise time. As outputs can oscillate, we need to adjust the definition a little, to the time taken for the system output to reach $\pm 2\%$ of its value and stay there. Again, we can't get an exact answer, but we can find a conservative estimate.

As a second order system is an exponential term multiplied by a sinusoidal term, the sinusoid can't exceed $\pm 1$, otherwise the response wouldn't decay. This means it relies on the exponential term to get close to the final output, so once it's decayed below $2\%$, the product of both terms won't ever be greater than that. So, let's equate the exponential term with $0.02$.
$$\frac{e^{\zeta \omega_{n} t}}{\sqrt{1-\zeta^{2}}} = 0.02$$
We kinda need to bodge this to get $\zeta$ as the subject. If $\zeta$ is small, then $\zeta^{2}$ is even smaller. That means $1-\zeta^{2}$ is probably close to one. Square rooting that again gets it even closer to one. Therefore, we estimate (assuming $\zeta$ is small)
$$\sqrt{1-\zeta^{2}} \approx 1$$ This means the denominator disappears, and we can rearrange for $T_{s}$ again
$$\boxed{T_{s} = \frac{4}{\zeta \omega_{n} } = \frac{4}{\alpha}}$$
## Percentage Overshoot
Underdamped second-order systems exhibit [[overshoot]] of their final values. To find how big this [[overshoot]] is, we need to derive the time where the biggest overshoot occurs, called the **time to peak overshoot** $T_{p}$. This is the time from 0 to the peak of the overshoot.

The peaks and troughs are stationary points (gradient = 0) in the [[step response]]. However remember that the step response is the integral of the impulse response, and therefore the impulse response is the derivative of the step response.

We can take the inverse Laplace transform of the transfer function to get the impulse response (which again, is the derivative of the step response). 
$$\frac{dy(t)}{dt} = \mathcal{L}^{-1} \left( \frac{\omega_{n}^{2}} {s^{2} + 2 \zeta \omega_{n}^{2} + \omega_{n}^{2}} \right)$$
- where $y(t)$ is the step response

Solving this should get us
$$\frac{dy(t)}{dt} = \frac{\omega_{n}e^{- \zeta \omega_{n} t}}{\sqrt{1-\zeta^{2}}} \sin (\omega_{n} \sqrt{1-\zeta^{2}} \cdot t)$$
To find the stationary points, we set it equal to 0. The exponential terms will never hit 0, so let's only equate the sinusoidal part.
$$\begin{align}
0 &= \sin\left( \omega_{n} \sqrt{1 - \zeta^{2}} \cdot T_{p} \right) \\
\omega_{n} \sqrt{1- \zeta^{2}} \cdot T_{p} &= n \pi, \space n \in 	\mathbb{Z}
\end{align}$$
The first overshoot is at $n = 1$, so we can solve and find 
$$\boxed{T_{p} = \frac{\pi}{\omega_{n}\sqrt{1-\zeta^{2}}}=\frac{\pi}{\omega_{d}}} $$
It's fairly easy to find the overshoot not. In the response function, substitute $t = T_{p} = \frac{\pi}{\omega_{d}} = \frac{\pi}{\omega_{n} \sqrt{1-\zeta}}$. Simplify, and we get
$$y(T_{p}) = 1  + e^{\frac{-\zeta \pi}{\sqrt{1-\zeta^{2}}}}$$
Where:
- 1 is the final value
- $e^{\frac{-\zeta \pi}{\sqrt{1-\zeta^{2}}}}$ is the [[overshoot]]  
We normally express this as a percentage to nullify [[DC gain]]
$$\boxed{\%OS = 100 e^{\frac{-\zeta \pi}{\sqrt{1-\zeta^{2}}}}}$$
## Dominance
It's possible to factorise any polynomial with real-values coefficients into first- and second-order components, with real coefficients. Any arbitrary transfer function can there be treated as a cascaded combination of simple building blocks:
- A gain (DC gain of a constant multiplier $K$)
- 1st-order poles and zeros (on the left- and right-half of the [[s-plane]])
- Poles on the origin where $s=0$ ([[integrator]])
- Zeros on the origin ([[differentiator]])
- 2nd-order pole and zero pairs (on the left- and right-half of the [[s-plane]])

How do these components interact with each other?

> [!note]
> **Poles near the origin are slow, poles further from the origin are fast**

