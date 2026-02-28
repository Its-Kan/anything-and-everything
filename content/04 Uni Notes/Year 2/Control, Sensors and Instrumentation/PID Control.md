 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-08-05]

--- 
So in [[PI Control]] we improved steady-state error using an integrator which increased system type while have roughly the same closed-loop performance of a simple gain controller. Then in [[PD Control]] we reshaped the root locus by adding a zero to achieve a better dynamic response. 

Can we combine both?
```table-of-contents
```
---
## PID Control 
Basically, yes! This is a **PID** (Proportional-Integral-Derivative) controller. This consists of an integrator and two zeros: one is the PD zero for the transient response, the other is the PI zero near the origin. 

We could design a PI controller first, then design a PD controller to improve its transient response. 
- The poles can be placed precisely (good)
- The change of gain will affect the speed and residue of the PI pole near the origin (bad)
Or, we could design a PD controller first, then add a PI controller to improve the [[steady-state error]]. 
- The PI controller can be tuned accurately (good)
- The designed closed loop poles will probably move a bit (bad)

The second option is generally better. We want to:
1. Design a PD controller using the procedure in [[PD Control#Steps|Lecture 16]] for the desired transient performance
2. Design a PI controller using the procedure in [[PI Control#Steps|Lecture 17]] where the transient performance changes as little as possible. 

The PI design process is iterative, and that the transient response will change when the PI controller is added. In general, it will **increase settling time** and **reduce overshoot** because of the additional slow pole, so the PD controller should be designed with this in mind. 
- (exam questions will be the other way round: the PI part will be pre-designed, so the question will ask you to design the PD part)
### Example
$$G(s) = \frac{1}{2s^2+4s+3}$$
*Design a unity negative feedback controller to satisfy the following requirements*
Ok, let's see what we have. Open-loop poles at $-1 \pm \frac{\sqrt{2}}{2}j$, with no zeros and system type of $0$.
- *No more than 10% [[overshoot]]*
	- Implies $\zeta \geqq 0.5912$ or $\cos^{-1}\zeta<53.75\degree$  
-   *[[Settling time]] 2s or less*
	- As $T_{s}\approx \frac{4}{\alpha}$, we expect closed-loop poles left of $-2$
	- This means we'll need [[PD control]] as the open-loop poles are to the right of $-2$
- *Zero [[steady-state error]] to a unit step input*
	- We have a type 0 system, as you can't factor out an $s$ in the denominator
	- So, we need [[PID control]] to increase the system type.

So, how do we start designing?

We know the closed-loop poles have to be left of $-2$, as well as needing to have a damping angle of less than $53.75\degree$. Let's focus on each part at a time:
- For damping:
	- When we design the PD controller, we add a zero. This tends to increase the overshoot, so our damping ratio should be conservative, $\zeta >0.5912$
- For the settling time:
	- When we design the PI controller, it will tend to increase the settling time, so our settling time should also be conservative, $T_{s}<2s$

What value we choose for a desired pole **is an educated guess**. To fulfil both conditions, let's choose $-3\pm3j$. Two nice integers. Let's once again use the [[angle criterion]] to see if it's a valid location. Plugging into the equation, we find that the poles add up to $-249.4\degree$. So, to get the angle to add up to an odd multiple of $180\degree$, we need to place a zero $z$ that's $69.4\degree$ to satisfy the criterion. Looking at the diagram:
![[PID Control.png]]

$z$ can be calculated using trigonometry 
$$\begin{align}
\tan(69.4\degree) &\approx \frac{3}{z-3}\\
z &\approx 4.125
\end{align}
$$
Cool! Let's find the gain to make up for it. Monic form gain is
$$K_{m} \approx \frac{3.04 \times4.21}{3.20} \approx 4$$

Since the monic form gain of $G(s)$ is $\frac{1}{2}$, so the required gain is approximately $K=8$. Our root locus looks like:
![[PID Control-1.png]]

![[PID Control-2.png]]
- This is a PID (Proportional-Integral-Derivative) controller.

It's very widely used, often deployed without even considering the system or requirements.

- If [[steady-state error]] is not a problem, a PD controller is better
- If [[transient response]] is not a problem, a PI controller is better
- Always check whether a simple gain will do!
- It's not usually possible to "tune" a PID controller by messing with the gains individually