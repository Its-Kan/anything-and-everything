 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-03-20]

--- 
 The most important design tool for single-input single-output linear control: the root locus diagram.
```table-of-contents
```
---
## Simple Control
In the [[Steady State Error]] lecture, we derived a gain algebraically to control a simple plant:
$$ G(s) = \frac{30}{2s^{2}+17s+30}$$
- This system displays a 10% overshoot to a unit step input using [[unity negative feedback]], and a gain of $K \approx 2.445$.
- The closed loop [[transfer function]] is defined as:
$$\begin{align} T(s) &= \frac{30K}{2s^{2}+ 17s + 30(K+1)} \\
&\approx  \frac{73.36}{2s^{2}+ 17s + 103.36}
\end{align}
$$
## The Root Locus
Let's see what happens to the poles and zeros of the transfer function if we vary the [[DC gain]] 
![[Design by Root Locus.png]]

There are always two poles, either two real ones or a pair of complex conjugates. 
- The open loop poles are both real, and stay real up until $K=0.3$, getting closer together
- And at some point, they become a complex conjugate pair.

So this begs the question, where do the poles go when the gain is varied? Consider the system:
![[Design by Root Locus-1.png]]

We know the transfer function will be $T(s) = \frac{KG(s)}{1+KG(s)}$. Setting the denominator to $0$ (making the  transfer function go to infinity which means a location of a pole), we know there must be a closed-loop pole at $KG(s) = -1$. This is saying a few things:
- $G(s)$ tends to be a complex number, while $K$ is always real. 
	- This means its modulus **must** be 1, $||KG(s)|| = 1 \dots$, known as its [[gain criterion]]
	- Its on the negative real axis, so its argument **must** be an odd multiple of $180 \degree$ $(2n+1)\pi = (2n+1)180 \degree$, known as the [[angle criterion]] 

The [[gain criterion]] $||KG(s)||=1$ is easy to satisfy, by finding the gain using $K = \frac{1}{||G(s)||}$.  As $K$ is real, the [[angle criterion]] depends **only** on $G(s)$.

> [!note] Therefore...
> **The root locus is a plot of all points that satisfy the [[angle criterion]]**

A lil useful trick:
$$\angle (KG(s)) = \sum(\text{angles from zeros}) - \sum\text{angles from poles}$$
### Example
$$G(s) = \frac{s+1}{(s+2)(s+4)}$$
Is the point $-2+2j$ on the root locus?

You could substitute it in for $s$, and see if it is a negative real number. That's long, so let's use the equation above there.

Looking at the zeros, there's one at $s_{z}=-1$. Looking at the poles, there's one at $s_{p1} = -4$ and $s_{p2}=-2$. 

Now, let's calculate the angles each one has from the real axis, to the arbitrary point. Doing it for each one, $\angle s_{z} = 116.57 \degree$, $\angle s_{p1} = 45 \degree$ $\angle s_{p2} = 90 \degree$.

Take away the zero angles from the pole angles and if it adds up to an odd multiple of $180 \degree$, we will have satisfied the [[angle criterion]]. So have we?

**No.**

Brilliant. Aight, let's do this for every point to see where... Let's not do that actually. It's not feasible to scan the entire [[s-plane]] looking for a point that satisfies the [[angle criterion]]. There are two ways we can do this instead:
- Slowly plot the closed-loop poles for very small increments of $K$, and join them with lines (good for MATLAB)
- Develop rules for finding line features, and use these to draw an approximate sketch (good for us!)
## Rules
### 1 to 8
1. The root locus diagram is symmetrical about the real axis.
	- [[Poles and zeros]] always appear in complex-conjugate pairs, hence the mirroring.
2. Loci start at **open-loop** poles and end at **open-loop** zeros.
	- Imagine the loci as a journey of all valid transfer functions when the gain is varied. We start at the open-loop pole when $K=0$, and end at the open-loop zeros when $K \rightarrow \infty$.  
3. If there are more open-loop poles than zeros (an "excess of poles"), the remaining loci tend towards asymptotes.
4. These asymptotes have angles
	- $$\theta_{A}= \frac{(2n+1) \cdot 180 \degree }{\text{excess of poles}}, n \in \mathbb{N}$$
	- This is the angle in which
		- **One** excess pole means the angle is $180\degree$, so one branch travels left along the real axis
		- **Two** excess poles gives us $90\degree$ and $270\degree$, so two branches travel straight up and down.
		- **Three** excess poles gives us $60\degree$, $180\degree$ and $300\degree$, radiating three lines one to the left, and two at $120\degree$ above and below the real axis. An equilateral triangle!
5. The asymptotes all meet at the **centre of gravity**
	- $$s_{cg} = \frac{\sum \text{poles} - \sum \text{zeros}}{\text{excess of poles}}$$
	- Those asymptotes meet the real axis at the same point, like the middle of a polygon.  
6. The real axis forms part of the loci at any point p where the total number of open-loop poles and zeros to the right of $p$ is odd
	- Take a point on the positive real axis, and check how many poles or zeros are to the right of that point. If it's not odd, keep going left. When you cross a pole or zero, start drawing a locus. When you cross a pole or zero again, stop drawing.  
7. When loci arrive at or leave the real axis, they do so at $90 \degree$
8. The points at which loci arrive at the real axis (**break-in** points) or leave the real axis (**break-away** points) are given by:
	- $$\sum_{i=1}^{m} \frac{1}{s-z_{i}} = \sum_{i=1}^{n} \frac{1}{s-p_{i}}$$
	- Or
	- $$\frac{dG(s)}{ds} = 0$$

These aren't all of them, but we will come back to them later. As for plotting
- If the rules contradict each other, something's gone wrong
- Aim for smooth curves
- Asymptotic loci never cross their asymptotes
- Most non-asymptotic curves tend to be **parts of circles** for simple systems
#### Example 1
Let's look at the same example again.
$$G(s) = \frac{30}{2s^{2}+17s+30}$$
- **Rule 2:** There are two poles, therefore two start points at $s=-2.5$ and $s=-6$. No poles, so no end points, therefore we have 2 excess poles, and therefore two of the lines will be asymptotes.
- **Rule 4:** Let's look at the asymptote angles. We have two excess poles, so plugging it into the equation we get $90\degree$ and $270\degree$.
- **Rule 5:** We know these asymptotes meet at the centre of gravity of the poles and zeros. No zeros, so it becomes $\frac{-6-2.5}{2} = -4.25$.
- **Rule 6:** Using the method, we know there's a real-axis segment between $-2.5$ and $-6$.
- **Rule 8:** Let's find the break-aways, differentiation looks simple here. We find that $s=-4.25$
![[Design by Root Locus-2.png]]

What does this show us? Well, we can choose any point (corresponding to a closed-loop pole) on the locus, and there would be some gain that allows us to have that. Or the other way round, if we vary gain, the poles can lie anywhere on this locus.
#### Example 2
Let's look at
$$G(s) = \frac{s+10}{2s^{2}+17s +30}$$
 - **Rule 2:** We have two start points at ($s=-2.5$, $2=-6$); one end point ($s=-10$, 1 excess pole, so 1 asymptote)
 - **Rule 4:** We have 1 asymptote, which  goes to the left to infinity (angle is $180 \degree$)
 - **Rule 5:** Only one asymptote, that's always on the real axis, so no need for a centre of gravity
 - **Rule 6:** Using the method, there's a segment between $-2.5$ and $-6$, and then an infinite line from $-10$. This is in line with **Rule 4**!
 - **Rule 8:** Time to find break-aways/break-ins. The first equation looks easier, and we get $s \approx -15.477, -4.523$. So, we have a break-away between the two poles and then a break-in to the left of the zero (as we start from poles, end at zeros). How do we connect these? Occam's Razor, the easiest shape tends to be the easiest, in this case, a circle.
 ![[Design by Root Locus-3.png]]

### 9 and 10
If there are complex open-loop poles, the start points aren't on the real axis, so don't necessarily enter at $90 \degree$. How do we calculate this?

9. The locus leaves a complex starting point $p_{1}$ at an angle given by
	- $$\theta_{p_{1}}=\sum^{m}_{i=1} \theta_{z_{i}} - \sum^{m}_{i=2} \theta_{p_{i}} \pm 180 \degree$$
	- Where $\theta_{p_{i}}$ is measured anticlockwise from the positive real axis
	- $\theta_{p_{2 \dots n}}$ and $\theta_{z_{1 \dots n}}$ are the angles from the other poles and zeros to the one we're looking at, measured in the same way.
		- Draw a line from every other pole and zero, and calculate their angles from the real axis to the drawn line. Take away the pole angles from the zero angles, then add or take away $180$ to limit it between $180$ and $-180$. 
10. The locus leaves a complex starting $z_{1}$ at an angle given by
	- $$\theta_{z_{1}}=\sum^{n}_{i=1} \theta_{p_{i}} - \sum^{m}_{i=2} \theta_{z_{i}} \pm 180 \degree$$
		- Same process as **Rule 9**. 
> [!info]
> Remember: **zero = poles - zeros**, or **pole = zeros - poles**. 

#### Example
$$G(s) = \frac{(s+1)(s+2)}{s^{2}+6s+10}$$
Let's go through some rules!
- **Rule 2:** Starting points at the pole $-3 \pm j$, end points at the zero $-1$ and $-2$
- **Rule 3:** No asymptotes, as there's no excess poles 
- **Rule 6:** Moving our pen right to left, we see there's a real axis segment between $-1$ and $-2$
- **Rule 8:** Differentiating looks annoying, so putting it into the equation we get $s \approx -1.61$, $s \approx -3.72$ for the break-in points.
	- Only one of these values line on the real axis segment ($s \approx -1.61$ ), so we ignore the other value.
- **Rule 10:** Since the loci is symmetrical, let's just look at the top pole, at $-3+j$. 
	- ![[Design by Root Locus-4.png]]

And so we get:

![[Design by Root Locus-5.png]]

### 11
How do we find where the locus branches crosses the imaginary axis? 

11. Imaginary axis crossings are found by using a [[Routh array]] and the [[Routh-Hurwitz stability criterion]].

That's. A lot of new shit. Let's break this down.
#### The [[Routh Array]]
If all the system poles lie in the left-half of the [[s-plane]], then we say it has [[absolute stability]]. This can be determined using the **denominator** of a closed-loop [[transfer function]], and a [[Routh array]]. But what is that?
##### Stage 1
Write down the **characteristic polynomial** $C(s)$, which is just the denominator of the transfer function.
$$a_{0}s^{n} + a_{1}s^{n-1} + a_{2}s^{n-2} + \dots + a_{n-2}s^{2} + a_{n-1}s + a_{n}$$
In order to be stable, all the coefficients $\{ a_{i} \}$ must have the same sign for stability (all positive or all negative.) It's necessary, but only a part of it
##### Stage 2
Form a [[Routh array]]. What?

1. In the left column, write the $s$ terms in descending powers. Write the last one as $s^{0}$. 
2. In the second column, write all the even coefficients in one row, then all the odd coefficients below it. 
	- Remember, $a_0$ is the coefficient of the largest $s$ term.
3. Fill in the third row now. 
	- $b_{0}$ is like calculating the determinant of the matrix (made with the 2x2 square of the coefficients), then dividing by the bottom left number.
	- $b_{1}$ do the same, but right side of the matrix shifts to the left by one. 
	- $b_{2}$ and so on keeps shifting the right side to the left by one.
- Fill in the remaining rows.
	- $c_{0}$ is the same, but now we move the matrix down one, and do the same. 
	- Eventually, the coefficients will start computing to $0$, and they will start encroaching from the right. 
![[Design by Root Locus-6.png]]
##### Stage 3
Now, bin the rest of the table, except the first and second column. A stable system will have **no sign changes** in the second column. Every sign change indicates one right-half [[s-plane]] (unstable) pole.

#### Example 1
![[Design by Root Locus-7.png]]
- No sign changes in the first column, so the system is stable 
#### Example 2
![[Design by Root Locus-9.png]]
- Two sign changes ($1$ to $-8$, then $-8$ to $\frac{61}{8}$), so the system is unstable, with two right-hand plane poles.  

#### Complications
If the left-hand column contains a zero, it means we're going to divide by $0$ at some point. However, dealing with this is not needed for this module.

Something we could see is if there's a **whole row** of zeros, something interesting happens. A zero row indicates **a subset** of the poles are also symmetrical about the imaginary axis. To find this, we need to get the auxiliary polynomial $A(s)$. It's read out from the zero two and the row above, exactly the same as $C(s)$, with the zigzag pattern. For example:
![[Design by Root Locus-10.png]]

We then differentiate $A(s)$, replace the zero row with the coefficients, then continue doing the [[Routh array]] process.

If there's a **zero row**, some of the poles are symmetric about the real and imaginary axis. If so, *and* we know for certain that none of them are in the right half of the plane, then it won't be on the left half plain, so *must* be on the imaginary axis.

Or, as $A(s)$ is a factor of $C(s)$, we know the roots of $A(s)$ must be a subset of the system poles. So, setting $A(s) = 0$ will find us the poles symmetric about the origin, horizontally and vertically.

If a root locus branch crosses the imaginary axis, then:
- For some gain value, the closed-loop system will be marginally stable
- This means some poles are located symmetrically about the origin
- So a **zero row** will be present in a Routh array for the closed-loop system.

Let's say we have a [[closed-loop transfer function]], with a variable gain $K$. This means we will have a [[Routh array]], where some rows could be 0 at certain values of $K$. Finding this value of $K$ that creates a zero row finds us the poles that are exactly on the imaginary axis.
### 12
The last rule allows us to find the value of the gain at any point on a branch.

12. The overall **monic form** gain (gain when the coefficient of the highest-degree term is $1$) $K_{m}$ for any point on the root locus is found by
	- $$K_{m} = \frac{{\prod \text{finite pole lengths}}}{{\prod \text{finite zero lengths}}}$$
	- Or, pick a point on a branch where a closed-loop pole would sit.
		- Measure the distances from the **open-loop** poles and zeros.
		- Multiply all the pole lengths, and divide by the product of all the zero lengths to get $K_{m}$. 
	- *You'll have to guesstimate the pole locations if their on a curved line, and then use trigonometry to calculate distances!*

It returns the **monic form** gain, which isn't really useful for us, as we want the **additional required** gain we need to get to the poles to their desired locations. Problem is, that the root locus shape doesn't depend on open-loop gain. For example, $\frac{1}{s^{2}+2s+5}$ and $\frac{100}{s^{2}+2s+5}$ look the exact same. So, we have to simplify the equation into its **monic form**. How? Let's say we have:
$$G(s) = \frac{2}{3s^{2}+s+2}$$
- Using the equation, we get $K_{m} = 25$
- We can convert the original equation into its monic form, to get its gain. This would be $\frac{2}{3} \times \frac{1}{s^{2} + \frac{1}{3} s + \frac{2}{3}}$, and we can see the monic form gain is $\frac{2}{3}$.
- So, we divide $K_m$ by the current gain to get the required additional gain. So, $25 \div \frac{2}{3} = 37.5$.
#### Example 
$$\frac{2}{(s-1)(s^{2}+6s+10)} = \frac{2}{s^{3}+5s^{2}+4s-10}$$
- Poles at $+1, -3 \pm j$ (unstable due to the positive pole).
- Real axis segment left of $+1$
- Three extra poles, so three asymptotes, with a centre of gravity at $\frac{-5}{3}$
- Break-in and break-away at $s \approx-0.46, s \approx-2.87$
- Angle of departure is $-90 - 166 +180 = -76 \degree$. 
- Axis crossing points by converting to a closed-loop transfer function (multiply $K$ to the numerator, then add the numerator to the denominator), then forming a Routh array. This would look like:
$$T(s) = \frac{2K}{s^{3}+5s^{2}+4s+(2K-10)}$$
![[Design by Root Locus-11.png]]

Getting us:

![[Design by Root Locus-12.png]]

Now, the question asks us to *"Find $K$ such that the dominant system dynamics are $2^{nd}$-order with a [[damping ratio]] of $\zeta \approx 0.707$."* How should we go about this?
## Unmodelled Dynamics
Root locus plotting rules depend on open-loop pole and zero locations. Due to [[dominance]], we tend to ignore 