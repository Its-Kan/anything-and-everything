 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-02-19]

--- 
When we talk about control, we will talk about [[transfer function]] in an abstract context. We want to analyse physical systems, and develop [[transfer function]] representations. So, where do they come from? We can find them in electrical networks and mechanical systems. 
```table-of-contents
```
---
## Electronic Systems
> [!example] Example: Electrical Networks
> ![[Modelling dynamic systems.png]]
> The transfer function here tells us given any input, what the output will be in the [[s-plane]]. 

The conversions are defined in Semester 1. Here are some reminders on how to do this:
- [[nodal analysis]] 
- [[superposition]] 
## Mechanical Systems
Modelling (linear) physical systems is easy in the [[s-plane]]. Linear, translational mechanical systems usually comprise of three elements:
- Masses
- Springs
- Dampers
Modelling can be done by considering the "impedances" of these components. We can't use current and ratio, so instead we use the ratio of force $F(s)$ acting on it to its physical movement $X(s)$:
$$
Z(s) = \frac{F(s)}{X(s)}
$$

| **Item** | **Law of Motion**                                             | **Impedance** |
| -------- | ------------------------------------------------------------- | ------------- |
| Mass     | $$\begin{align}f(t) &= Ma(t) \\&= M \ddot{x} (t)\end{align}$$ | $$Ms^2$$      |
| Spring   | $$\begin{align}f(t) &= Kx(t)\end{align}$$                     | $$K$$         |
| Damper   | $$\begin{align}f(t) &= Bv(t) \\&= B \dot{x} (t)\end{align}$$  | $$Bs$$        |

> [!question]- Derivations
> ### Masses
> [[Newton's Second Law]] states:
> $$
> \begin{align}
> f(t) &= Ma(t) \\
>  &= M \ddot{x} (t)
> \end{align}
> $$
> Taking the [[Laplace Transforms|Laplace transform]] gets us: 
> $$
> \begin{align}
> F(s) = Ms^{2}X(s) \\
> \frac{F(s)}{X(s)} &= Ms^2
> \end{align}
> $$
>  Therefore the impedance of a mass $M$ is $\boxed{Ms^{2}}$.
> ### Springs
> Springs obey Hooke's Law:
> $$
> \begin{align}
> f(t) = Kx(t)
> \end{align}
> $$
> Taking the [[Laplace Transforms|Laplace transform]] gets us: 
> $$
> \begin{align}
> F(s) &= KX(s) \\
> \frac{F(s)}{X(s)} &= K
> \end{align}
> $$
>  Therefore the impedance of a spring with spring constant $K$ is just $\boxed{K}$.
> ### Dampers
> Dampers are viscous:
> $$
> \begin{align}
> f(t) &= Bv(t) \\
> f(t) &= B \dot{x}(t)
> \end{align}
> $$
> Taking the [[Laplace Transforms|Laplace transform]] gets us: 
> $$
> \begin{align}
> F(s) &= BsX(s) \\
> \frac{F(s)}{X(s)} &= Bs
> \end{align}
> $$
> Therefore the impedance of a damper with damping coefficient $B$ is $\boxed{Bs}$.
> 
### Example
![[Modelling-2.png]]
1. Use [[superposition]]: Take one mass at a time, and assume the other masses are fixed.
2. We now "perturb" that mass in the direction of displacement
	- On mass one:
		- Force pushing on it is $F(s)$
		- Overall displacement in a direction is $X_{1}(s)$
		- The mass resists its own motion, $M_{1}s^{2}X_{1}(s)$ (impedance, times displacement)
		- The spring resists the motion, $KX_{1}(s)$ 
		- The damper resists the motion, $BsX_{1}(s)$
![[Modelling-3.png]]
## Rotational Systems 
These can be analysed in the same way. 
- Force $f$ in $N$ $\rightarrow$ Torque $T$ in $Nm$
- Displacement $x$ in $m$ $\rightarrow$ Angle $\theta$ in $\text{rad}$
- Velocity $v$ in $ms^{-1}$ $\rightarrow$ Angular velocity $\omega$ $\text{rads}^{-1}$
- Tension (torsion) and viscosity work like in the translational mechanical systems, where constant $K$ $\rightarrow$  $Nm \space\text{per rad}^{-1}$
- Mass $M$ in $kg$ $\rightarrow$ Inertia $J$ in $kgm^{2}$

| **Item** | **Translational Impedance $(\frac{F}{X})$** | **Rotational Impedance $(\frac{T}{\theta})$** |
| -------- | ------------------------------------------- | --------------------------------------------- |
| Mass     | $$Ms^2$$                                    | $$Js^{2}$$                                    |
| Spring   | $$K$$                                       | $$K$$                                         |
| Damper   | $$Bs$$                                      | $$Bs$$                                        |
### Gearboxes
[[Rotational Systems]] allow gearing between parts of the system, however only linear [[gearbox]] effects can be modelled. We assume no inertial mass, friction or elasticity (which can be modelled outside of the [[gearbox]] itself), and is specified in terms of gear ratios. A gearbox divides angle (and speed and acceleration) and multiplies torque by the gear ratio. 
- $T_{J} = \theta_{J}Js^{2}$ . Force (now torque) equals displacement (now angle) times mass (now inertia).
- Torque becomes $T_{J}= GT$, where $G$ is the gear ratio
- Angle of the mass becomes $\theta_{J} = \frac{1}{G}\theta$. 
- Substituting gets us $\frac{T}{\theta} = (\frac{1}{6})^{2}Js^{2}$. The impedance gets divided by the square of the gearbox ratio.

So. What do we do when we encounter one?
- Move all components to the input side of the [[gearbox]] 
- Multiply moved displacements by the gearbox ratio
- Divide moved impedances by the square of the gearbox ratio

![[Modelling.png]]

The gear ratio is $\frac{2000}{20} = 100$. 
- The spring, mass and damper get divided by $100^{2}=10000$ 
- The rotation gets multiplied by $100$

![[Modelling-1.png]]

