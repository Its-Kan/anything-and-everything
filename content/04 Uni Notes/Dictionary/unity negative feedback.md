[Location:: #dictionary/uni]
[Subject:: #uni/electronics #uni/maths]
[Tags::]

---
## Definition
A system in which the output is fed back into, using comparison at a summing junction. If it's zero, then the input and output are the same, and is stable.

![[unity negative feedback.png]]
where:
- $G(s)$ is the [[transfer function|plant]] (where the sensors are)
- $H(s)$ is the controller (where the reacting happens)
- $G(s)H(s)$ is the open-loop system
and
- $Y(s)$ is the output
- $V(s)$ is the input: the set point (desired output)
- $E(s)$ is the error signal (difference between actual output and desired output)
$$
\begin{align}
Y(s) &= G(s)H(s)E(s) \\
E(s) &= V(s) - Y(s) \\
\end{align}
$$
$$
\boxed{T(s) \triangleq \frac{Y(s)}{V(s)} = \frac{G(s) H(s)}{1+ G(s)H(s)}} 
$$
This is the equation for the close-loop [[transfer function|transfer function]] $T(s)$. We want to find an equation for the [[transfer function]] $H(s)$ that has the right properties. 

