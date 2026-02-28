 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-07-22]

--- 
Different applications have different steady-state error requirements.
```table-of-contents
```
---
## [[Steady State Error]] 
To specify all these different types of steady-state errors, we describe the response of a system to several different input types:
- A unit **step** to represent **position demand**
- A unit **ramp** to represent **velocity demand**
- A unit **parabola** to represent **acceleration demand**

The [[final value theorem]] states that $f(\infty) = \lim_{s \to 0} sF(s)$. So...
$$
\begin{align*}
e(\infty) &= \lim_{s \to 0} sE(s) \\
&= \lim_{s \to 0} \frac{sV(s)}{1 + G(s)H(s)}
\end{align*}
$$
where $e(\infty)$ is the [[steady state error]]. At infinity means it perfectly tracks without any errors

Notice from the following examples, the error constants $K$ are properties of the **open-loop** transfer function (just the plant and controller). The [[steady state error|steady state errors]] $e(\infty)$ are for the closed-loop equivalents. 
### [[Step Input]]
For a step input, the steady state error is multiplied by $\frac{1}{s}$
$$
\begin{align*}
e(\infty) &= \lim_{s \to 0} \frac{s \cdot \frac{1}{s}}{1 + G(s)H(s)} \\
&= \frac{1}{1 + \lim_{s \to 0} G(s)H(s)}
\end{align*}
$$
We define $\lim_{s \to 0} G(s)H(s) \triangleq K_{p}$, where $K_{p}$ is called the [[position error constant]]. 
$$\boxed{e(\infty)_{\text{step}} = \frac{1}{1+K_{p}}}$$
If you know your plant transfer function $G(s)$ and you've designed a controller $G(s)$, you can calculate
### Ramp Input
For a step input, the steady state error is multiplied by $\frac{1}{s^2}$
$$
\begin{align*}
e(\infty) &= \lim_{s \to 0} \frac{s \cdot \frac{1}{s^{2}}}{1 + G(s)H(s)} \\
&= \lim_{s \to 0} \frac{1}{s + sG(s)H(s)} \\
&= \frac{1}{\lim_{s \to 0} sG(s)H(s)}
\end{align*}
$$We define $\lim_{s \to 0} sG(s)H(s) \triangleq K_{v}$, where $K_{v}$ is called the [[velocity error constant]]. 
$$\boxed{e(\infty)_{\text{step}} = \frac{1}{K_{v}}}$$
### Parabolic Input
For a step input, the steady state error is multiplied by $\frac{1}{s^3}$
$$
\begin{align*}
e(\infty) &= \lim_{s \to 0} \frac{s \cdot \frac{1}{s^{3}}}{1 + G(s)H(s)} \\
&= \lim_{s \to 0} \frac{1}{s^2 + s^2G(s)H(s)} \\
&= \frac{1}{\lim_{s \to 0} s^2G(s)H(s)}
\end{align*}
$$We define $\lim_{s \to 0} s^{2}G(s)H(s) \triangleq K_{a}$, where $K_{a}$ is called the [[acceleration error constant]]. 
$$\boxed{e(\infty)_{\text{parabola}} = \frac{1}{K_{a}}}$$
## System Type
Let's look at a closed feedback look transfer function. As we know, it will always be a ratio of two polynomials, and it can be rewritten in this form:
$$G(s)H(s) \triangleq \frac{K_{g}(1+T_{a}s)(1+T_{b}s) \dots}{s^{m}(1+T_{1}s)(1+T_{2}s)\dots}$$
- $K_g$ is the gain constant 
	- It's **not** [[DC gain]], as it's undefined when $s=0$. It never has a steady state, inputting a constant will get us a ramp.
- $T$ is the pole's/zero's [[time constant]], where its location is defined by $s = -1/T$
- $m$ represents the number of integrators (poles on the origin) present in the open loop 
	- This number

When $s =0$, the value of each bracket will go to $1$, allowing us to get the [[DC gain]]. We call it

If the system has one or more poles, then $m$ will be non-zero, meaning we can factor out one or more $s$ terms from the denominator. 
### Type 0 
If we have an open-loop system with **no [[integrator|integrators]]** (no poles on the origin, when $m=0$) we have a **type 0 system**.
$$G(s)H(s) = \frac{K_{g}(1+T_{a}s)(1+T_{b}s) \dots}{(1+T_{1}s)(1+T_{2}s)\dots}$$
Let's look at the error constants for a **type 0 system**:
* $K_p = \lim_{s \to 0} G(s)H(s) = K_g \text{ so } e(\infty)_{\text{step}} = \frac{1}{1+K_p} = \frac{1}{1 +K_g}$
	* it settles with an error of $\frac{1}{1+K_{g}}$
* $K_v = \lim_{s \to 0} sG(s)H(s) = 0 \text{ so } e(\infty)_{\text{ramp}} = \frac{1}{K_v} = \frac{1}{0} = \infty$
	* it grows forever
* $K_a = \lim_{s \to 0} s^2G(s)H(s) = 0 \text{ so } e(\infty)_{\text{parabola}} = \frac{1}{K_a} = \frac{1}{0} = \infty$
	* it grows forever

In short a **type 0 system** can only track position/step inputs, and will settle with a finite, constant error. With velocity/ramp or acceleration/parabola inputs, the error will tend towards infinity.
### Type 1
If we have an open-loop system with **one [[integrator]]** (one pole on the origin, when $m=1$), we have a **type 1 system**.
$$G(s)H(s) = \frac{K_{g}(1+T_{a}s)(1+T_{b}s) \dots}{s(1+T_{1}s)(1+T_{2}s)\dots}$$
Let's look at the error constants for a **type 1 system**:
* $K_p = \lim_{s \to 0} G(s)H(s) = \infty \text{ so } e(\infty)_{\text{step}} = \frac{1}{1+K_p} = 0$
	* it settles perfectly, without error
* $K_v = \lim_{s \to 0} sG(s)H(s) = K_{g} \text{ so } e(\infty)_{\text{ramp}} = \frac{1}{K_v} = \frac{1}{K_g}$
	* it settles with an error of $\frac{1}{K_v}$
* $K_a = \lim_{s \to 0} s^2G(s)H(s) = 0 \text{ so } e(\infty)_{\text{parabola}} = \frac{1}{K_a} = \frac{1}{0} = \infty$
	* it grows forever

In short a **type 1 system** will track a position/step input perfectly, and a velocity/ramp input with some error. Only an acceleration/parabola input, the error will tend towards infinity.
### Type 2
If we have an open-loop system with **two [[integrator]]s** (two pole on the origin, when $m=2$), we have a **type 2 system**.
$$G(s)H(s) = \frac{K_{g}(1+T_{a}s)(1+T_{b}s) \dots}{s^{2}(1+T_{1}s)(1+T_{2}s)\dots}$$
Let's look at the error constants for a **type 2 system**:
* $K_p = \lim_{s \to 0} G(s)H(s) = \infty \text{ so } e(\infty)_{\text{step}} = \frac{1}{1+K_p} = 0$
	* it settles perfectly, without error
* $K_v = \lim_{s \to 0} sG(s)H(s) = \infty \text{ so } e(\infty)_{\text{ramp}} = \frac{1}{K_v} = 0$
	* it settles perfectly, without error
* $K_a = \lim_{s \to 0} s^2G(s)H(s) = 0 \text{ so } e(\infty)_{\text{parabola}} = \frac{1}{K_a} = \frac{1}{K_g}$
	* it settles with an error of $\frac{1}{K_a}$

In short a **type 2 system** will track a position/step and velocity ramp input perfectly, and a acceleration/parabola input with some error.
### Type 3+
Step, ramp and parabola will track perfectly.
### Examples
$$G(s) = \frac{s+6}{s(s+2)}$$
- Type 1 (degree of factored out $s$ in the denominator is $1$)
- 2nd order system (highest degree of multiplied out denominator is $2$)
$$G(s) = \frac{(s+2)(s+6)}{s^{2}(s+3)(s+4)(s+5)(s+7)}$$
- Type 2 (degree of factored out $s$ in the denominator is $2$)
- 6th order system  (highest degree of multiplied out denominator is $6$)
## Error Performance
Using the plant from last time, with a gain of $K = 2.445$.
$$G(s) = \frac{30}{2s^{2} + 17s +30}$$
We can't factor out an $s$, so this is a **type 0 system**.
- Without the gain, we have $K_{g}=1$ (will settle at $1$)
- Adding the gain, $K_g$, and therefore $K_p$ for a type 0 system, we can find the error constant to be
$$e(\infty)_{\text{step}} = \frac{1}{1+K_{p}} \approx 0.291$$

Let's do a different example.
$$KG(s) = \frac{s+6}{s(s+2)}$$
We know it's:
- Type 1 (factored out one $s$)
- $K_{p} = \infty$ so $e(\infty)_{\text{step}} = 0$
- $K_{v} = \lim_{s \to 0} sKG(s) = \frac{6}{2} = 3$, so $e(\infty)_{\text{ramp}} = \frac{1}{K_{v}}=\frac{1}{3}$
Reminder, to get from an open-loop to a closed-loop transfer function with a constant gain, we put it in the equation
$$T(S) = \frac{KG(S)}{1+KG(S)}$$Inputting $KG(s)$ into the equation, we can eventually simplify into 
$$T(s) = \frac{s+6}{s^{2}+3s+6}$$