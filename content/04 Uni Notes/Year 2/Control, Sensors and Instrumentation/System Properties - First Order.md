 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-03-19]

--- 
We'll look at first-order systems, looking at:
- DC gain
- Settling time
- Rise Time
- Effect of zeros 
```table-of-contents
```
---
## First-order poles 
This is a system that has one pole in its [[transfer function]] (one solution for the denominator) in the form:
$$G(s) = \frac{A}{s+a}$$
- where $G(s)$ is the [[plant]] 
- $A$ is the scaling factor or gain
- $a$ is the pole
- $s$ is the complex frequency variable

And from the [[final value theorem]], the [[DC gain]] of the system is:
$$K_{dc} = \lim_{s \rightarrow 0} [G(s)] = \frac{A}{a}$$

We can get it's response to a unit step simply by multiplying it by $\frac{1}{s}$:
$$Y(s) = \frac{1}{s} G(s) = \frac{A}{s(s+a)}$$
Where $Y(s)$ is the output of our system.

We can then do partial fractions to get A in a form where we can use the integration lookup tables to convert back to the time domain. We get:
$$ A = \alpha (s+a) + \beta (s)
$$
and then:
$$\begin{align}
A &= \alpha A \\
B &= \frac{-A}{\alpha} 
\end{align}$$
Substituting those back into the partial fractions gets us
$$Y(s) = \frac{A}{a}(\frac{1}{s} - \frac{1}{s+a})$$
which using the lookup tables converts to
$$
y(t) = \frac{A}{a} (1- e^{-at})
$$
The [[time domain]] output shows us that applying a unit step doesn't get us a unit step, but it shows where it settles to. 
- If $a$ is large, the pole is far into the left-half $s$-plane and the exponential decay will be fast
- If $a$ is small, the pole is near the imaginary axis and the exponential decay will be slow
- If $a$ is negative, the pole is in the right-half $s$-plane and the exponential term will not decay (it will increase)
## [[settling time|Settling Time]] 
Let's rewrite the equation in terms of a [[DC gain]] and a time constant.
$$G(s) = \frac{A}{s+a} = \frac{K_{dc}}{1+s \tau}$$
where $K_{dc} = \frac{A}{a}$ is the [[DC gain]] and $\tau = \frac{1}{a}$ is the time constant of the system. What can we do with this?

Well if we went through the same process as last time, and convert to the t-domain again we get:
$$y(t) = \frac{A}{a}(1-e^{-at}) = K_{dc}(1-e^\frac{-t}{\tau})$$
As $s = \sigma + j \omega$, and $\omega$ has Hz units, that means the resulting $\tau$ must have units too. This means we can normalise time in terms of time constants instead of seconds. We will *always* get this graph by doing this. Moving the pole will make this result the same. It takes around 4 time constants for the output to settle to 98% of its final value. This is what we call the [[settling time]]. 

![[System Properties - First Order.png]]
## [[rise time|Rise Time]]
This is the time taken for the output to rise from 10% to 90% of its final value. Substituting again, we get:

$$
\begin{equation*}
\begin{aligned}
0.9 &= 1 - e^{-aT_{90\%}} \\
\ln(0.1) &= -aT_{90\%} \\
T_{90\%} &\approx \frac{2.303}{a}
\end{aligned}
\qquad
\begin{aligned}
0.1 &= 1 - e^{-aT_{10\%}} \\
\ln(0.9) &= -aT_{10\%} \\
T_{10\%} &\approx \frac{0.105}{a}
\end{aligned}
\end{equation*}
$$
Subtracting one from the other gets us the [[rise time]] 
$$T_{r} = T_{90\%} - T_{10\%} \approx \frac{2.2}{a} = 2.2 \tau$$
## Modes and Residues
Let's look at the impulse response (which is just the differential of the step response) of this system. It is technically a second order response, however we can look at it as two first order responses, convolved together (which is just multiplication in the s domain).
$$G(s) = \frac{1}{(s+2)(s+4)}$$
Using partial fractions, we can rewrite this and then convert to the t-domain:
$$\begin{align}
G(s) &= \tiny\frac{1}{2} \normalsize\frac{1}{s+2} - \tiny\frac{1}{2} \normalsize\frac{1}{s+4} \\
g(t) &= \tiny\frac{1}{2} \normalsize e^{-2t} - \tiny\frac{1}{2} \normalsize e^{-4t}
\end{align}$$
- The poles $s = -2$ and $s = -4$ define the time constants of the exponential **modes** ($e^{-2t}$ and $e^{-4t}$).
- The weights of the two modes in the response ($\frac{1}{2}$ and $\frac{-1}{2}$ are the **residues**).

Ok, let's add a zero at let's say $s = -1$
$$G(s) = \frac{s+1}{(s+2)(s+4)}$$
Doing the same steps again gets us $A = \frac{-1}{2}$ and $B = \frac{3}{2}$. Adding a zero keeps the modes the same, but the residues change. Stability is therefore dictated by the poles, and not the zeros. As long as the exponential terms decay, then the system will be stable. 

> [!note]
> **Poles define the modes, zeros change the residues.**

- **Poles** tell you **what kind of behaviours** (modes) the system has (e.g., exponential decay, oscillation).
- **Residues** tell you **how much of each behaviour** is present in the final output.