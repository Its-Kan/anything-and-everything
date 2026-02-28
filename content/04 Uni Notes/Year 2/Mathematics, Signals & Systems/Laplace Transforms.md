---
share_link: https://share.note.sx/8hys6hml#8HR8+oLPGSvsNSSOzCdVN3i7ig4OTcSxlTTEWc5DtxU
share_updated: 2025-11-18T00:24:19+00:00
---
**Year**: [[Year 2]]
**Subject**: [[Mathematics, Signals & Systems]]
**Topic**: Laplace Transforms
**Date Created**: 2024-12-19

--- 
```table-of-contents
```

---
## Differential Equations
Ok to start, let's go over things we know, and then we can relate them to this new topic. 

[[Differential Equations]] are of course, equations with differentials in them. We can see these in circuit theory; the properties of idealised capacitors and inductors are described by linear differential relationships:

- $i = C \frac{dv_0}{dt}$
- $v_{L}= L \frac{di}{dt}$

When we have a bunch of these components, we'll get a large, complicated set of coupled linear differential equations, which relate the outputs to the inputs. When we have multiple differential equations to model an engineering process, we call it a [[dynamic system]]. These are very common all over engineering, whenever any form of energy is stored, dissipated and/or propagated. 

Let's look at an example circuit.

![[RLC Circuit with Thevenin Power Source.png]]

The inductor ($L$) and capacitor ($C$) store energy in this circuit, and is the source of its [[dynamic response]], as these components store energy based on the variation in time (due to the derivative in their equations). $v_L$ is the time-varying inductor voltage, and $v_C$ is the same for the capacitor. If we want to write an equation for this circuit, we'll get:

- $\frac{d^{2}v_{c}}{dt^{2}} + \frac{R}{L} \frac{dv_{C}}{dt} + \frac{1}{LC}v_{C} = \frac{1}{LC}v_{S}(t)$ 

The source voltage, $v_{S}(t)$ is our input, and the capacitor's voltage $v_{C}(t)$ is our output. If we were to name this type of differential equation, it could be called a *second-order, linear, differential equation with constant coefficients.* 
- We are assuming **R**, **L** and **C** don't change, explaining the *constant coefficients* part. 
- Since the equation is linear, the [[superposition]] principle holds, and we can find the answer using a complementary function and particular integral. 

> [!tip] Reminder
> Refer to the **second-order non-homogenous linear** branch in [[Differential Equations]] to work it out

Let's look at another example.

![[LR Circuit with Thevenin Power Source.png]]

$v_{s}(t)$ is our driving input, and the resistor voltage is the output. Let's consider when the inductor is initially unfluxed, and the input is in the form $v_{s}(t) = kt$ for $t \ge0$, for some constant $k$. Using [[Kirchhoff Laws|Kirchhoff's Voltage Law]] gets us:
$$v_{s} = L \frac{di}{dt} + Ri$$
And since $i = \frac{v_{R}}{R}$, we can substitute and get 
$$\frac{L}{R} \frac{dv_{R}}{dt}+ v_{R}= v_{S} = kt$$

This is a first-order linear differential equation, and once again we can solve it. The particular solution turns out to be:

$$v_{R} = \frac{kL}{R} \exp\left(\frac{-Rt}{L}\right) + kt - \frac{kL}{R}\space \text{for}\space t \ge 0$$ 
- The complimentary function part, $\frac{kL}{R} \exp\left(\frac{-Rt}{L}\right)$, represents the *free, transient* or *natural* behaviour of the system.
- The particular integral, $kt - \frac{kL}{R}\space$ represents the *driven, forced* or *steady state* output.

Here are some plots on what the solution looks like for various values of **R** and **L**.

![[R and L plot.png]]

System such as the two above, which can be described by *ordinary linear differential equations with constant coefficients* are classed as **[[LTI systems|continuous linear time-invariant (LTI) systems]]**. They're quite common, but it would be good to have a tool which simplifies their description, and gives specific insights into their physical properties. 
## Transforms
Solving differential equations using [[time domain]] approaches can be difficult or even impossible for more complicated equations.

Let's simplify:
- "4 miles" is much easier to think about rather than 253,440 inches. Converting 4 miles to 253,440 inches is a transform.
- A unit circle in polar coordinates with $r=1$ is easier to think about than the same circle in Cartesian coordinates, $x^{2}+y^{2}=1$. Switching between the two coordinate systems is a transform.
- Taking a logarithm is a transform, translating a difficult operation (multiplication) into an easier one (addition) ![[Logarithm Transform.png]]
- The use of a semi-log graph transforms an exponential function to a straight line.
- Log-log graphs transforms a power relationship to a straight line

So, how can we transform a differential equations?
## Laplace Transforms
The Laplace transform simplifies differential equation, whether an individual one or a large set of them. It's defined by:
$$ F(s) = L[f(t)] \triangleq \int^{\infty}_{0}f(t) e^{-st}dt$$
- in English: 
	- $F(s)$ is $f(t)$, with the Laplace transform applied to it. 
	- This is defined by ($\triangleq$) the infinite integral from infinity to 0, of $f(t)$ multiplied by $e^{-st}$ in terms of $t$.
- It's assumed that $f(t) = 0 \space \text{for} \space t<0$. This means we call it a [[single-sided Laplace transform]].
- $s$ is a complex variable. This transform changes our viewpoint from a (real) [[time domain]] function $f(t)$, to one in a (complex) [[s-plane]] $F(s)$.
- $s = \sigma + j \omega$ is known as the [[complex frequency variable]] or the **Laplace variable**.
### Laplace Transform of Simple Signals
From the definition, it's possible to work out the [[s-plane]] versions of a range of common time-domain functions.
#### The unit impulse (Dirac delta function)
The limits of a finite pulse of decreasing width, but constant (unit) area gives us a way to visualise the **Dirac delta function**. This helps us model impulses whose area is 1. It's denoted by $\delta(t)$.

![[Dirac Delta Function Graph.png]]

It's defined by two properties:
1. $\delta (t - \tau) = 0$ when $t \ne \tau$
	- $\tau$ is a moment in time
	- When $t = \tau$, then that is where the impulse is.
2. "shifting property" $\int^{\infty}_{-\infty} f(t) \delta (t - \tau) = f(\tau)$ 
	- When we multiply a function by the impulse, it will be 0, and then the value of the function at a single point at the impulse. 

We can apply the [[Laplace Transforms]] to this function:
- $L[\delta(t)] = \int^{\infty}_{0}\delta(t)c^{-st}dt = 1$, hence $L[\delta(t)] =1$.
Therefore, the **inverse Laplace transform** can be written as:
- $L^{-1}[1] = \delta(t)$
#### Unit step (Heavyside step function)
It's defined by:
$$  
\begin{align}  
u(t) = 1 && t \ge 0\\  
= 0  && t < 0
\end{align}  
$$So, applying the Laplace Transform to this gives us:
![[Step Function with Laplace.png]]

> [!tip] Convergence...
> It's assumed that $e^{-st} \bigg|_{t = \infty} = 0$. But $s = σ +jω$ is a complex variable. It's necessary to use complex analysis. The Laplace transform of $u(t)$ is hence defined for all values of $s$, except $s=0$.  
### Exponential Function
![[Exponential Laplace Transform.png]]
#### $cos(\omega t)$ and $sin(\omega t)$ 
It's easy to confirm from the definition that the Laplace transform is linear:
$$ L[af(t) + bg(t)] = aF(s) + bG(s)$$
So, if write the trig functions as their exponential forms, we can apply the [[Laplace Transforms]] on that.

![[cos and sin Laplace Transform.png]]

We've now derived the following time-domain to [[s-domain]] pairs.

| **Name**    | **Time-domain**      | **s-domain**                      |
| ----------- | -------------------- | --------------------------------- |
| Impulse     | $\delta(t)$          | 1                                 |
| Unit        | $u(t)$               | $\frac{1}{s}$                     |
| Exponential | $e^{-st}u(t)$        | $\frac{1}{s+a}$                   |
| Cos         | $cos(\omega t) u(t)$ | $\frac{s}{s^{2}+\omega^{2}}$      |
| Sin         | $sin(\omega t) u(t)$ | $\frac{\omega}{s^{2}+\omega^{2}}$ |
### Properties
The transform itself has several important fundamental properties: 
#### Differentiation
What happens if we want to evaluate the Laplace transform of the derivative of a signal: $L[\frac{df}{dt}]$? We can use **integration by parts** (setup a $u, u', v$ and $v'$ table, where $u=e^{-st}$ and $dv=df$). 
![[Differential Laplace Transform.png]]
If we do this, we get:
$$ L\left[\frac{df}{ft}\right]= sF(s) - f(0)$$
The Laplace transform has the property of turning time-domain calculus into [[s-domain]] algebra. How handy! 
#### Integration
Aight, other way around now, what if we want to get the Laplace transform of an integral? Again doing by parts where $u = \int^{t}_{0}f(\tau)d \tau$, and $dv = e^{st}$, we can do:
![[integral Laplace Transform.png]]
And we get:
$$ L\left[\int^{t}_{0}f(\tau)d \tau\right]= \frac{1}{s}F(s)$$

> [!example] Unit Ramp
> ![[Laplace Transform of a unit ramp.png]]

> [!example] LR circuit with Thévenin power source
> ![[LR Circuit with Thevenin Power Source.png]]
> 
> 
> 
> We know this equation describes the circuit:
> $$ \frac{L}{R} \frac{dv_{R}}{dt} + v_{R}=kt $$
> If we take the Laplace transform term by term gives us:
> $$ \frac{L}{R}[sV_{R}(s)-v_{R}(0) ] + V_{R}(s) = \frac{k}{s^{2}} $$
> And since $v_{R}(0) = 0$, rearranging gives:
> $$V_{R(s)}= \frac{k}{s^{2}(\frac{sL}{R}+1)}$$
> 
> 

This is the s-domain version of the particular solution. It contains the same information as the complementary function, the particular integral and initial conditions. But if we want to get it into a form we can understand (time-domain output), we need to carry out the [[inverse Laplace transform]]. 

It's possible to work out the inverse Laplace transform using integrals, but fortunately for us, we can use a table of signals to do the work for us! Sadly most s-domain outputs won't appear in our table, but we can use **partial fractions** to simplify them down to parts.

![[Laplace Transform partial fractions.png]]

The basic idea is to translate differential equations, to an s-domain equation using Laplace transforms, and then use algebra to get an s-domain solution, and then use the inverse Laplace transform to get back to a t-domain solution.

![[Laplace Transform shortcut.png]]

Both the transform and the inverse transform stages can be shortcut with the use of tables. Our workflow becomes:
1. Use the Laplace transform table on a differential equation
2. Rearrange the equation to obtain the solution
3. Rearrange the solution using partial fractions
4. Use the inverse Laplace transform table to convert to the t-domain solution.

> [!example] Example
> ![[Laplace Transform circuit.png]]
> If we use [[Kirchhoff Laws|Kirchhoff Voltage Law]], we get
> $$ f \frac{di}{dt}+5i + \int^{-t}_{0} i(\tau) d \tau + v_{C}(0) = Eu(t)$$
> - $f \frac{di}{dt}$ is the inductors voltage
> - $\int^{-t}_{0} i(\tau) d \tau + v_{C}(0)$ is the capacitor voltage (by rearranging $i = C \frac{dv}{dt}$)
> - $5i$ is the resistor voltage
> 
> Since $v_{C}(0) = 0$, the Laplace transform of the equation is:
> $$ 4[sI(s) - i(0)] + 5I(s) + \frac{1}{s}I(s) = E \frac{1}{s}$$
> ![[Laplace Transform example 2.png]]
### Laplace Transforms for Circuit Components
It's quite straightforward to write down the differential equation for a circuit, and then use the Laplace transform to "switch our viewpoint". To do it even quicker, we can visualise the properties in the s-domain
#### Resistors
In the [[time domain]], the resistor is viewed as:
$$
v(t) = Ri(t)
$$
- Voltage as a function of time equals resistance times current as a function of time.

However in the [[s-domain]], we have:
$$
V(s) = RI(s)
$$
- Voltage as a function of s equals resistance times current as a function of s.
#### Capacitors
Similarly:
$$
i(t) = C \frac{dv(t)}{dt} \quad \text{or} \quad v(t) = \frac{1}{C} \int_{0}^{t} i(\tau) d\tau + v(0)
$$
If we were to apply the Laplace transform, and then simplify, we get:
$$
\begin{align}
I(s) &= C \left[ sV(s) - v(0) \right] \\
\Rightarrow V(s) &= \frac{1}{sC}I(s) + \frac{v(0)}{s}
\end{align}
$$
Looking at the voltage equation, we can model an [[s-domain]] charged capacitor as a capacitor with capacitance $\frac{1}{sC}$ and a voltage source with voltage $\frac{v(0)}{s}$ in series. Here, we say the *Laplace impedance* of a capacitor is $\frac{1}{sC}$.
#### Inductor
And again similarly:
$$
i(t) = L \frac{di(t)}{dt} \quad \text{or} \quad i(t) = \frac{1}{L} \int_{0}^{t} v(\tau) d\tau + i(0)
$$
Again, applying the Laplace transform gives us:
$$
I(s) = \frac{1}{sL}V(s) + \frac{i(0)}{s}
$$This time, the [[s-domain]] model is an inductor of inductance $sL$, in parallel with a current source of current $\frac{i(0)}{s}$. $sL$ is the Laplace impedance of an inductor.

> [!example] Example
> ![[Laplace Transform example 3.png]]
> Total impedance is $\frac{10^{6}}{s}+ 3 \times 10^{6}$. Substituting values into $I(s) = V\frac{s}{R}$ gives us:
> $$
> I(s) = \frac{-\frac{5}{s}}{\frac{10^6}{s} + 3 \times 10^6} = \frac{-\frac{5}{3} \times 10^{-6}}{s + \frac{1}{3}}
> $$
> And then finding the [[inverse Laplace transform]] using tables gets us:
> $$
> i(t) = -\frac{5}{3} e^{-\frac{t}{3}}\mu A
$$
### Lumped Components and Network Functions
In the examples, we are looking at idealised models of physical characteristics that may be distributed throughout a circuit. In general, resistance, inductance and capacitance may be spread continuously and unevenly along wires, but we instead summarise their cumulative effects at particular points, called [[lumped components]]. 

They give a good approximation in a wide variety of circuit applications, and gives us a straightforward model of large, multi-loops networks. If we combine this, with Laplace techniques, we can simplify even more with [[network functions]]! These are [[s-domain]] expressions that contains the information of values of various circuit components, but also their relative positions in a network.

> [!EXAMPLE] Example
> ![[Laplace Transform example 4.png]]

This transforms the circuit into an *input-output relationship*, where $v_{1}(t)$ or $V(s)$ is the input and $i(t)$ or $I(s)$ is the output. Divide $V_{1}(s)$ on both sides, and we get another network function called the **driving point input impedance** (since voltage and current are measured at the same place). 

Similarly, we can make another equation based off the relationship between the two voltages:

![[Laplace Transform 5.png]]

All of the [[network functions]] for [[lumped components]] circuit networks are rational functions in the [[s-domain]] with real coefficients. In general, they will have the form:
$$
H(s) = \frac{a_n s^n + a_{n-1} s^{n-1} + a_{n-2} s^{n-2} + \cdots + a_1 s + a_0}{b_m s^m + b_{m-1} s^{m-1} + b_{m-2} s^{m-2} + \cdots + b_1 s + b_0}
$$
Which can be factored into:
$$
H(s) = G \frac{(s - z_1)(s - z_2)(s - z_3) \cdots (s - z_{n-1})(s - z_n)}{(s - p_1)(s - p_2)(s - p_3) \cdots (s - p_{m-1})(s - p_m)}
$$
Which looks awfully similar to [[Poles and Zeros]]! As a reminder, $\frac{a_{n}}{b_{m}}$is the gain constant, poles are the roots of the denominator and the zeroes are the roots of the numerator. A network function is *completely* characterised by these three characteristics.

![[Laplace Transform input output function.png]]

$X(s)$ is the Laplace input, $O(s)$ is the Laplace output, and $H(s)$ is the [[system function]] that relates the output to the input.  

![[Laplace Transform s domain.png]]
### [[Frequency Response]] of a System
To establish the frequency response (sinusoidal response) of a system $H(s)$, we have to apply an input function $x(t) = sin (\omega t)$, and consider the output:
$$
O(s) = H(s)X(s)
$$
and if $x(t) = sin(\omega t)$, then $X(s) = \frac{\omega}{s^{2}+\omega^{2}}$.

If $H(s)$ has the form:
$$
\begin{align}
H(s) &= G \frac{(s - z_1)(s - z_2)(s - z_3) \cdots (s - z_{n-1})(s - z_n)}{(s - p_1)(s - p_2)(s - p_3) \cdots (s - p_{m-1})(s - p_{m)}} 
\\
&= G \frac{\prod_{i=1}^{n} (s - z_i)}{\prod_{j=1}^{m} (s - p_j)}
\end{align}
$$
- Big pi is similar to a summation, but instead of adding, it's multiplying. 
Then we can carry out a partial fractions expansion of the output. Let's not.
### Plotting [[Poles and Zeros]] 
### [[convolution|Convolution]] 