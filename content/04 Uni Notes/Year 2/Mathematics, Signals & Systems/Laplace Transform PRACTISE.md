**Year**: [[Year 2]]
**Subject**: [[Mathematics, Signals & Systems]]
**Topic**: Laplace Transform PRACTISE
**Date Created**: 2025-01-14

---

![[Laplace Transform PRACTISE 1.png]]

First, let's try it by solving the differential equation. Let's use [[Kirchhoff Laws|Kirchhoff's Current Law]] to get the currents. The sum of the currents in all the branches is equal to the current going in, therefore:
$$
i = i_{R}+ i_{L} + i_{C} = \frac{v}{R} + i_{L} + C \frac{dv}{dt}
$$
Let's get all of these currents in terms of one branch; let's use the inductor since it's independent from the other branches. Since voltage is the same for all of the branches, we can use the inductor voltage equation.
$$
\begin{align}
v &= L \frac{di_{L}}{dt} \\
\frac{dv}{dt} &= L \frac{d^2i_{L}}{dt^2}
\end{align}
$$
Inserting these voltage equations into the original, rearrange into a second order differential equation, and then replace the constants gets us:
$$
\begin{align}
i &= \frac{L \frac{di_{L}}{dt}}{R} + i_{L} + LC \frac{d^2i_{L}}{dt^2} \\
\frac{1}{LC} i &= \frac{d^{2}i_{L}}{dt^{2}} +\frac{1}{RC} \frac{di_{L}}{dt} + \frac{1}{LC}i_{L} \\
2 i &= \frac{d^{2}i_{L}}{dt^{2}} +3 \frac{di_{L}}{dt} + 2i_{L} \\
\end{align}
$$
We now have a differential equation we can solve!
1. **Solve auxiliary equation**: $$
s^{2} + 3s + 2 = 0 \Rightarrow s=-2, -1
$$
2.  **Put in complementary function:**
$$
i_{L_{CF}} = A \exp(-t) + B \exp(-2t)
$$
3. **etc**

Let's now do it with the [[Laplace Transforms]] instead. Let's convert them into their [[s-plane]] impedances. As a reminder:

