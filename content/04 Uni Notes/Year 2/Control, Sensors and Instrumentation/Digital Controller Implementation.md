 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-08-09]

--- 
Now we know about [[PD Control]], [[PI Control]], and [[PID Control]], let's implement them digitally. Digital systems have some limitations, such as sampling/sample rates, and the fact we need to approximate integration and differentiation. 
```table-of-contents
```
---
In standard parallel form, a PID controller is specified as:
![[PID Control-2.png]]

$$H(s) = \frac{C(s)}{E(s)} =  K_{p}+ \frac{K_{i}}{s} + K_{d}s$$
In the time domain, it becomes
$$c(t) = K_{p}e(t) + K_{i} \int^{t}_{0} e (\tau) d \tau + K_{d} \frac{de(t)}{dt}$$
- PD and PI controllers can be seen a partial versions of PID controllers, with $K_{i}=0$ or $K_{d}=0$ respectively.
How can we implement this controller algorithmically?

## Digital PID
### Sampling
The error signal must be sampled at regular intervals. This gives readings of the error signal $e(t)$ at discrete time intervals $t = nT, n \in {0} \cup \mathbb{Z}$ 
- This means were looking at discrete time intervals of $T$, where our "position" $n$ is $0$, or an integer.
We must choose the sample rate carefully, at least double the highest frequency to satisfy Shannon's Law. We'll denote $e_{n}$ to represent $e(t)$ (the [[error signal]]) at time $t=nT$.
### Derivative Term
There are many ways to approximate the local slope of a curve. The simplest (first order) is the backwards difference approximation.
$$\frac{de(t)}{dt} \biggr\rvert_{t = nT} \approx \frac{e(nT) - e\big((n-1)T\big)}{T} = \frac{1}{T} \left( e_n - e_{n-1} \right)$$
Simply, we're using the differentiation by first principles, using the smallest possible time step and the previous term to find the local slope. 
### Integral Term
There are many ways to approximate the area under a curve, but the simplest is rectangular approximation. The sampled value is assumed not to have changed over the previous sample period
$$\int^{t}_{0} e(\tau) d \tau \approx \sum^{n}_{k=1}e_{k}T$$
Next simplest is trapezoidal approximation, where the sampled value is assumed to have changed linearly.
$$\int^{t}_{0} e(\tau) d \tau \approx \sum^{n}_{k=1}(\frac{e_{k} e_{k-1}}{2}T)$$The integral term can be expressed as a recurrence relation. For the rectangular approximation
$$\begin{align}
\text{if} \\
i_{n} &= \sum^{n}_{k=0} e_{k}T \\
\text{then} \\
i_{n} - i_{n-1} &= e_{n}T \\
i_{n}&= i_{n-1} + e_{n}T
\end{align}$$
- where $i_{0}=0$

For the trapezoidal approximation:
$$\begin{align}
\text{if} \\
i_{n} &= \sum^{n}_{k=0} \frac{e_{k}+ e_{k-1}}{2}T \\
\text{then} \\
i_{n} - i_{n-1} &= \frac{e_{k}+ e_{k-1}}{2}T \\
i_{n}&= i_{n-1} + \frac{e_{k}+ e_{k-1}}{2}T
\end{align}$$
- where $i_{0}=0$
## Algorithm
Putting these terms together gives a simple algorithm for digital [[PID Control]].
1. Initialisation:
	- Set $e_{n-1} = i_{n-1} = 0$
2. Every sample:
	- Read $e_{n}$
	- Compute the derivative $d_{n} = \frac{1}{T}(e_{n} - e_{n-1})$
	- Update the integral $i_{n} = i_{n-1} + e_{n}T$ or $i_{n} = i_{n-1} + \frac{T}{2}(e_{n}+e_{n-1})$
	- Compute the controller output $c_{n} = K_{p}e_{n} + K_{i}i_{n} + K_{d}d_{n}$
	- Store $i_{n-1}=i_{n}$ and $e_{n-1}=e_{n}$

## Sample Rate
Increasing the sample rate brings several advantages
- Derivative and integration approximation becomes more accurate
- Delays are reduced, so the system [[#phase margin]] is eroded less
However, a high sample rate also brings problems
- Increased computational effort 
- Greater problems from numerical precision and rounding [[error signal]] 
- Greater susceptibility to noise in the derivative calculation.
## Phase margin
This is a measure of how close a system is to being unstable, and is related to the damping ratio. Even if the processing delay is negligibly small, the controller cannot respond to changes in the system output until the next sample instant, therefore the average response delay is $\frac{T}{2}$, plus any processing delay. 
## Other Digital Controllers 
It's possible to implement other structures, such as PANs and [[phase-advance networks]], digitally. To do this:
- Start with a controller [[transfer function]] 
- Express it as the ratio of the controller output $C(s)$ to the error signal $E(s)$
- Rearrange to eliminate the fractions
- Multiply out all the brackets 
- Substitute sampled signals and suitable derivative approximations
- Rearrange to find recurrence relations

