 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-08-05]

--- 
What if we want pole locations that aren't on the [[Design by Root Locus|root locus]]? The only thing we can do is to **change the shape** of the root locus. We can't move the open-loop poles and zeros, but we can add to them!
```table-of-contents
```
---
Let's say we have an open-loop system of
$$G(s) = \frac{1}{(s+1)(s+2)(s+10)}$$
with a damping ratio of $0.707$.

The root locus will look like:
- There are three poles, no zeros, so three asymptotes centred around $\frac{-13}{3}$
- Real-axis segments from $-1$ to $-2$, and left of $-10$
- Break-away somewhere between $-1$ and $-2$
- Axis crossing points somewhere inside $\pm 7.5j$

To achieve a damping ratio of $0.707$ (which is around $4\% OS$), we need a gain of around $19$. This gives a closed loop system of 
$$T(s) = \frac{19}{s^{3}+13s^{2}+32s+39}$$
- Complex poles are at $s \approx -1.38 \pm 1.38j$
- Real pole at $s \approx -10.25$
	- Settling time is around $\frac{4}{\alpha} \approx 2.9s$

Pretty good, but what if we want it quicker? Let's try adding a pole to the system, let's say at $s\approx1.5$. Instead, we have
$$G(s)H(s)=\frac{K(s+1.5)}{(s+1)(s+2)(s+10)}$$
Doing the same process again, we get $T_{s} \approx 0.69s$. That's better! Since the zero at $s=1.5$ is so close to the real pole at $-1.46$, they almost cancel each other out, making the complex poles exhibit [[dominance]]. This should mean a faster settling time!

Ok, we could keep testing random values for a pole. Kinda cringe. How do we find a zero to get a certain settling time? We need to re-shape the root locus so the closed-loop poles that lie at a specific point. We must move around the zero until this happens.

Remember the [[angle criterion]]? The angle to a 
$$\sum \text{zero angles} - \sum\text{pole angles} = (2n+1)180\degree$$
Input the poles, and solve for the zero angle, and find the point on the real axis that makes that angle with the desired pole. For our desired poles at $s=-5 \pm 5j$, the zero angle turns out to be at $114.62\degree$, which turns out to be $z\approx2.7$. We now need to find the gain, using [[Design by Root Locus#12|Rule 12]] to find the monic form gain by dividing the product of pole distances by the product of zero distances, which is $48$ for this. We need a controller that will change the zero location based on the [[error signal]] of the system. So, putting the gain and zero together, we get
$$H(s)=48(s+2.7)$$
So, making this a closed loop structure gets us;
$$T(s)=\frac{48s+129.6}{s^{3}+13s^{2}+80s +149.6}$$
The closed loop complex poles are at $s \approx -5.01\pm5j$, and the real pole is at $s=-2.99$. Yippee! 
## PD Control
![[PD Control.png]]
- This is a **PD** (Proportional-plus-Derivative) controller.
	- It takes an error signal in, multiplies it by $K_{p}$, then multiplies its derivative by $K_{d}$ (as multiplying by $s$ is taking a derivative in the [[time domain]]).
### Steps
1. Plot open loop [[poles and zeros]] 
2. Establish desired closed loop pole positions
3. Place on [[s-plane]] plot
4. Draw lines from one desired pole position to all system [[poles and zeros]] 
5. Establish angles and distances from known [[poles and zeros]] 
	- If there's a repeated pole or zero their angle and distances get multiplied by each instance. 
	- $\text{e.g.} \frac{(s+3)^{3}}{(s+2)^{2}}$, there are $3$ repeated zeros and $2$ repeated poles. The zero angles/distances get multiplied by $3$, and the pole angles/distances get multiplied by $2$.
6. Use the [[angle criterion]] to establish controller zero angle to desired pole location
	- If the required angle for the zero is negative, there isn't a valid location for the zero. Either something has gone wrong, or another controller should be used.
7. Establish controller zero position using trigonometry
8. Use [[Design by Root Locus#12|Rule 12]] to establish controller gain
9. (If it's not in an exam) Test closed loop system behaviour
### Problems
It has problems! The added zero will increase [[overshoot]]. Differentiators adds problems too, as you can't actually differentiate a live signal. Even if it could, there would be problems:
- A PD controller has a single zero and no poles, which means it's unchanging (invariant) under feedback. Gain increases by 20dB/decade above the zero frequency compared with a simple gain, which has a significant effect on noise rejection and the signal-to-noise ratio.
- The desired output $V(s)$ is sometimes known as the set point. A Step change to $V(s)$ will result in a step change to $E(s)$

The fix is to. Not use PD control! However, it's still widely used.