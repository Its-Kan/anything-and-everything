**Year**: [[Year 2]]
**Subject**: [[Mathematics, Signals & Systems]]
**Topic**: Multivariable Integration
**Date Created**: 2024-12-19

--- 
Ok, so we've covered differentiation, onto integration!
```table-of-contents
```
---

> [!tip] Reminder
> As a reminder, here's [[Integration I]], [[Integration II]] and [[Integration III]] from last year.

Single integrals integrate under a curve. [[multiple integrals]] integrate functions over areas, volumes or hypervolumes (more than three variables). 

As always let's simplify. The simplest type of multiple integral is a [[double integral]], where we integrate functions such as $f(x,y)$ over some region on a plane or surface. In fact, can do this when we do single-variable integral. 

$\int^{a}_{b} x \, \mathrm{d}x$ is the area enclosed under the upper limit (the function) and the other limits (the verticals lines at $x_1$ and $x_2$). However, we can also calculate this area not just using the vertical strips, but also horizontal ones.

![[Area elements of size dxdy.png]]

Dividing the area into both vertical slices (of width $\mathrm{d}x$) and horizontal slices (of height $dy$) gets us a bunch of lil' squares, whose area is size $dxdy$. We can sum the elements in the $y$ direction first, then in the $x$ direction, or vice versa. Either way, we can calculate the area using:

- $A = \int^{x_2}_{x_1} \int^{y_2}_{y_{1}} f(x,y) \, \mathrm{d}y \mathrm{d}x = \int^{y_2}_{y_{1}} \int^{x_2}_{x_{1}} f(x,y) \, \mathrm{d}x \mathrm{d}y$ 

Focus on the inner integral first, and then the outer one, and treat the other variable as a constant and sub in the values. Then calculate the last integral. Either way, we call the switching between the two viewpoints [[reversing the order of integration]].

If we have an integral in the form:
- $I = \int^{x_2}_{x_1} \int^{y_{2}(x)}_{y_{1}(x)} f(x,y) \, \mathrm{d}y \mathrm{d}x$
or, when two lines intersect, then we have two more limits to focus on, meaning we can get the area of a shape without one of the limits being the x-axis. 

![[Double Integral of an Enclosed Shape.png]]

> [!NOTE] Note
> In the example above, we could've reversed the order of integration, but this would've produced a much more complicated upper and lower limit, as focusing on the horizontal stripes would make the areas more complicated. Reversing the order of integration can complicate the calculation, but could also simplify it. Always consider the bounds.

## Change of Variables

When dealing with multivariable functions, we might need to convert out $xyz$ coordinate system, and view it in a different coordinate system: $uvw$, where $x$, $y$ and $z$ are functions of $u$, $v$ and $w$. (or $x(u,v,w)$, $y(u,v,w)$ and $z(u,v,w)$ The same pattern is true when $u$, $v$ and $w$ are the functions). The problem itself doesn't change, but how we view it does. Why? And what does this new system look like? That will come up later.

![[Partial Derivative in New Coordinate System.png]]

Huh, this looks like a 3 systems of equations problem. This means... matrices!  We can factor out the $\frac{\partial f}{\partial x}$, $\frac{\partial f}{\partial y}$, and $\frac{\partial f}{\partial z}$ to get:

![[3 Systems of Partial Derivative Equations.png]]

To translate it back to the $xyz$ coordinate system, we simply multiply both left sides by the inverse matrix.

![[Inverse Matrix.png]]

![[3 Systems of Partial Derivatives - xyz.png]]
## 2D Coordinate Systems
### Cartesian Coordinates
Of course, this is simple to visualise: along the corridor, up the stairs. We normally define these with $\hat{i}$ and $\hat{j}$ vectors. We know most of this, so let's move on.
### Polar Coordinates
We also know the conversion between Cartesian and polar coordinates:$$\begin{align*}
\begin{rcases}
x = r \cos(\theta)\\
y = r \sin(\theta) 
\end{rcases}
\quad \text{and} \quad
\begin{cases}
r = \sqrt{x^2 + y^2} \\
\theta = \arctan\left (\frac{y}{x}\right)
\end{cases}
\end{align*}$$Polar coordinates also have unit vectors to represent the unit case, $\hat{e}_{r}$ and $\hat{e}_{\theta}$, in the directions of increasing $r$ and increasing $\theta$.
![[Multivariable Integration basis vectors.png]]
where $$\hat{e}_{r} = \frac{\delta\underline{r}}{\delta r} \quad \text{and} \quad \hat{e}_{\theta} = \frac{\delta\underline{r}}{\delta \theta}$$