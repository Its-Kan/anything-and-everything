**Year**: [[Year 2]]
**Subject**: [[Mathematics, Signals & Systems]]
**Topic**: Multivariable Differentiation
**Date Created**: 2024-12-19

--- 
```table-of-contents
```
---
Many laws or system work are controlled by a single variable, e.g. $y = f(x)$. We can differentiate to get the gradient function, or integrate to get the area under the curve; all stuff we know. But the real world isn't that simple, and we most likely have multiple variables controlling an output, generalised as $w = f(x_{1}, x_{2}, ... x_{r})$. These expressions extend our graphs into multiple dimensions, and we can't use the same skills from last time.
## Functions of Two Variables

Let's do the simplest form of multivariable calculus, two inputs with one output: $z = f(x,y)$. $x,y,z$ was chosen as the variable names, to emphasise the geometric viewpoint of this form, as we can view this equation as a 2D surface in a 3D graph. 

![[3D Graph Examples.png]]

Ok, let's try to differentiate this. How?

To define a "slope" on a surface, we need to define a direction to focus on. This will be a **[[cutting plane]]**, that will focus on a cross-section of the graph. This will translate into a 2D graph, which just focuses on the slice that intersects the 3D graph. We call the line this produces the **[[intersection curve]]**.

![[Cutting Plane.png]]
![[Intersection Curve.png]]

Now this is a graph we can differentiate! We can now find a slope along a single curve on a 3D graph. This is the geometric visualisation behind **[[partial differentiation]]**.
## Partial Differentiation

> [!tip] Reminder
> - As a reminder, here's [[Differentiation I]] and [[Differentiation II & Parametric]] from last year.

[[partial differentiation]] of $f(x,y)$ is defined by:

![[Partial Derivative First Principles.png]]

Yes, very annoying, but in short, this calculates the gradient of a curve where $x$ changes, but $y$ doesn't affect the graph, and is effectively a constant. Of course, the same is true when it's the other way round, for $\frac{\partial f}{\partial y}$. We can use the same methods of single variable calculus here, but we just treat the other variable as a constant. 

> [!Example]
> 
> $\frac{\partial f}{\partial x} = 2yx$
> - we are differentiating in terms of $x$, so $y$ is treated as a constant
> - $x$ differentiates into 1
> - $y$ is unaffected
> $= 2y$

If we look at the 3D graph from above, we can see in which direction the partial differential is acting in.

When we have more variables, this idea can be extended further, however we can't visualise them in a graph. For example for $f(x,y,z)$, we can focus on one variable, and treat the rest as constants, and then partially differentiate. 

## Higher Order Partial Differentiation
### Second Order

Similar to ordinary differentiation, partial differentiation is an operation. $\frac{d}{dx}$ is analogous to $\frac{\partial}{\partial x}$. And as with being an operation, you can stack them to get higher orders of partial differentiation. For second order, you can partially differentiate twice along the same variable, or twice with different variables. 

![[Mixed Derivatives.png]]

When you partially differentiate with different variables, we call those are called **[[mixed derivates]]**. Order matters here; $\frac{\partial^{2}f}{\partial x \partial y}$ is different to $\frac{\partial^{2}f}{\partial y \partial x}$. To remember this, look at the bottom part of of the partial derivative, and read from right to left. So a second order partial differential that has a $\partial y \partial x$ means $f(x,y)$ is partially differentiated with respect to $x$ first, then with respect to $y$. 

These are cool, but hard to visualise. $\frac{\partial^{2}f}{\partial x \partial y}$ means *the rate of change in the $x$ direction of the derivative measured in the $y$ direction*. I don't know what the fuck that means.

If the graph is continuous (which most are), it's safe to say $\frac{\partial^{2}f}{\partial x \partial y} = \frac{\partial^{2}f}{\partial y \partial x}$. 
### Third and Higher Order

We can define higher order derivatives, with any number and order of partial differentials.

We can have:
$f_{xxx}$ and $f_{yyy}$, then $f_{xxy}$, $f_{xyx}$, $f_{yxx}$. And so on. This goes on for a while, but the same pattern repeats for all higher derivatives. 

> [!Example]
>
![[Example Higher Order Differentials.png]]
## Small Changes in Multivariable Functions

If you remember in single-variable calculus, getting the gradient at a point was done by getting the gradient between two points that are practically at the same place, or having a small change between them. We see this in the First Principles equation. 

When we add a new dimension, $x$ and $y$ can both change when there's a small change in a dimension. That means the total change is the the sum of effects of the variables (minus the original to isolate the change):

- $\Delta f = f(x+ \Delta x,y + \Delta y) - f(x,y)$

Using m a t h s, we can rewrite this as:

- $\Delta f \approx \frac{\partial f}{\partial x} \Delta x + \frac{\partial f}{\partial y} \Delta y$ 

> [!NOTE]
> In English, we can word this as:
> - The change in height due to $x$ and $y$ changing is approximately equal to the change of height in the $x$ direction ($\frac{\partial f}{\partial x} \Delta x$) plus the change of height in the $y$ direction ($\frac{\partial f}{\partial y} \Delta y$).

If we have three or more variables, $f(x,y,z,...$), we just keep adding the partial derivative times the change in the corresponding variable. This is the basis of multivariable calculus. 

When we take the limits of $\Delta x\to\infty$ and $\Delta y\to\infty$, we get the basis to differentiation, and our approximations become exact. Turning the equations into their **infinitesimal form** makes $\Delta f$ turn into $df$, as well with all the other Deltas. Doing this gets us:

-  $df \approx \frac{\partial f}{\partial x} dx + \frac{\partial f}{\partial y} dy + \frac{\partial f}{\partial z} dz +\ldots$

$df$ is called the **[[total differential]]** of the function. But what does this mean?

## The Total Derivative
### Two Variables, where $x(t)$ and $y(t)$
Let's focus on two variables just for simplicity. Let's look at the case when $x$ and $y$ are parametric, and are both controlled by a third variable $t$. So, our function $z$ would be written as $z = f(x(t), y(t))$. Differentiating $z$ gets us $\frac{dz}{dt}$, which turns out to be our total differential! 

Looking at the graph, the **[[intersection curve]]** turns out to be a curve instead of a linear line. 

![[Parametric Curve on a Plane.png]]

Differentiating each term with respect to $t$ gets us:

$$\frac{dz}{dt}= \frac{\partial z}{\partial x} \frac{dx}{dt} + \frac{\partial z}{\partial y} \frac{dy}{dt}$$

This is the **[[total derivative]]** of $f$ with respect to $t$, which represents the slopes of the function when the variations in $f(x,y)$ are plotted in a plane against $t$. 

To check if your answer is right, substitute in $t$ to eliminate $x$ and $y$, then differentiate normally. 
### Two Variables, where $y(x)$

In this case, we can calculate the derivative with the expression:

$$\frac{df}{dx}= \frac{\partial f}{\partial x} + \frac{\partial f}{\partial y} \frac{dy}{dx}$$

> [!NOTE]
> Just as a reminder, $\frac{df}{dx}$ and $\frac{\partial f}{\partial x}$ are different things.
> - $\frac{df}{dx}$ is the partial derivative, and it's the gradient along an intersection curve embedded on the surface
> - $\frac{\partial f}{\partial x}$ is the total derivative, and it's the gradient solely in the $x$ direction
> 

In general the equation above is correct, but when $\frac{df}{dx}= 0$, (where $f(x,y) = K$ and $K$ is a constant). When substituting in, we get:

![[When dfdx = 0.png]]

Looking at this on a graph, this case becomes a contour curve based on the constant height. 

![[Contour Lines.png]]

For problems that are one-dimensional problems embedded with a two-dimensional one (a.k.a. parametric equations), we can do the layered operation again. However to do this, we will need to put our original equation into operator form:

- $\frac{d}{dt}= \frac{dx}{dt} \frac{\partial}{\partial x} + \frac{dy}{dt} \frac{\partial}{\partial y}$

This is the **[[total derivative operator]]** with respect to $t$. Practically, this can "convert" the process of ordinary differentiation (along the curve within the surface) and partial differentiation on the surface along two independent directions. 
## Multivariable Taylor's Series Expansions

God damn that is uh. Not a nice phrase. 

Just to recap, a Taylor Series is an infinite sum of orders of $x$ that is able to define a function of a single variable, around some point $a$. 

![[Taylor Series.png]]

We can extend this definition to apply to two or more dimensions!

Again let's just simplify the case to just two variables $x$ and $y$ to $f(x,y)$ that are also controlled by a variable $t$. Let's also assume $x$ and $y$ are linear equations:

- $x = a+ht$
- $y = b+kt$ 

We do this because we want to start at a point $(a,b)$ on the surface, and then move radially outwards based on $h$ and $k$. Ok, what?

Think back to 1-variable Taylor Series for a sin wave for example. Let's look at a point and add variable by variable to our approximation. The more we add, the closer this point gets to the true value of the function. 

![[Taylor Approximation for a Sin Wave.gif]]

We're doing the same thing, but now there's two variables that get closer to the "true" value.

![[Taylor Approximation for a 3D Sin Wave.gif]]

And then we can use the operand form of the total derivative to get our other terms of the Taylor series! This particular form of the total differential operator is sometimes called the $D$ operator:

- $D = h \frac{\partial}{\partial x} + k \frac{\partial}{\partial y}$

So we can shorten $\frac{df}{dt}$ into $Df$, and $\frac{d^{2}f}{dt^{2}}$ into $D^{2}f$, and so on.

> [!Example] Example
>
![[Taylor's Series Expansion of sin(xy).png]]
## Stationary Points

So, for single-variable functions, stationary points were either local maxima, minima or point of inflection.

It's a lil' more complicated in 3D:
![[Multivariable Differentiation stationary points.png]]
- For a point to be a maximum, it must be a stationary point in every direction, but also a peak (negative second derivative) in every direction as well,
- For a point to be a minimum, it must be a stationary point in every direction, but also a minimum (in every direction as well)
- For a point to be a saddle point, the first-order derivates equal to 0, but is a minimum in one direction, and a maximum in another.
