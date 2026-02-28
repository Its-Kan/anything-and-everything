 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-08-05]

--- 
With [[PD Control]]  we reshaped the root locus using a zero. We can place poles, almost anywhere we like, however the system response might not be as we want it, with zeros or dominant poles, or the steady-state error might not meet our specification. 

> [!note]
> This can't be on the exam specifically, as we need to plot it accurately for it to work, however it needs to be understood for [[PID Control]]
```table-of-contents
```
---
## Adding an [[integrator]] 
When we add a zero, the [[Design by Root Locus|root locus]] can change dramatically. 

![[PI Control.png]]

There will be a [[steady-state error]] present as $\frac{1}{(s+1)(s+2)(s+10)}$ is a type $0$ system. So to reduce the error, we must increase the system type! Let's add an integrator to $H(s)$, the PD controller, to make it
$$H(s) = \frac{1}{s}(129.6 + 48s) = 48+ \frac{129.6}{s}$$
![[PI Control-1.png]]

This is! Not ideal! The integrator has affected the root locus, so we need to redesign the PD controller for the new type 1 system. Let's leave the zero in the same place, but keep the integrator. 

![[PI Control-2.png]]

Now that's better!

The PD zero ensures that the excess of poles is still 3, despite the integrator, so the asymptote angles are the same. The centre of gravity and complex branches have moved to the right. However, our desired poles at $-5 \pm 5j$ aren't achievable. Can we move the zero to get this? Let's look at the angle criterion again! 
$$\sum \text{zero angles} - \sum\text{pole angles} = (2n+1)180\degree$$
The [[integrator]] has added $-135\degree$, so we need to add $+135\degree$ to the angle sum, which means putting [[differentiator]] on the origin. Wait, this will just cancel each other out, how about moving the zero *reaaallyyyy close* to the origin instead? Maybe like, $s=-0.01$?

![[PI Control-3.png]]

That's a little better, the centre of gravity has shifted left a little! The fact that the integrator and zero are so close means the gain they contribute is almost negligible. Let's keep moving it left until it's closer to the first pole, but not close enough to cancel it out, around $s=-0.95$

![[PI Control-4.png]]

This gives us a nicer step response without affecting the root locus too much! We get $~4.7\%$ overshoot, and $T_{s}\approx 4.7s$. Now we have the same performance of a simple gain controller, but with zero steady-state error to a unit step!
## PI Control

![[PI Control-5.png]]
- This is a **PI** (Proportional-plus-Integral) controller. 
	- It takes an error signal in, multiplies it by $K_{p}$, then multiplies its integral by $K_{i}$ 

### Steps
1. Find a simple gain using the root locus diagram
2. Place a pole on the origin
3. Place a zero close to it
4. Test closed loop system behaviour
5. If slow pole dominates, try moving the zero further left
6. Repeat until performance is achieved or zero cannot move further
