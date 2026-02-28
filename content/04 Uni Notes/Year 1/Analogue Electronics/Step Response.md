[[Year 1]]

Back to the *what is it* and *why is it useful* and *why are we here* and *just to suffer*.

It's pretty much, the output of a system, when the input is a unit step. Not a constant voltage (DC) or an oscillating one (sine), just a step from 0 to a voltage. It's like the start of a square wave. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240519222141.png]]

The order of a response is based on how many poles it has in its frequency response. 
## Zero-Order Responses

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240519223043.png]]

No poles or zeros, as there's no "reactor"/time-dependent components (inductors and/or capacitors). This means the step response is a weaker version of the input step. 

Calculating it is literally just $V=IR$. Yay.
## First-Order Responses

This means there is one pole, and no or one zero. There are 4 possibilities:
- one pole, no zeros
- one pole, one zero at 0Hz
- one pole, one non-zero zero with $z<p$
- one pole, one non-zero zero with $z>p$

Let's tackle them one by one:

*However,* the process for each of them should be the same:
- Write the equation for the frequency response
	- replace capacitors and inductors with their complex impedances, 
### One Pole, No Zero
- We have a resistor and a capacitor in series. 
- This is just the capacitor charging equation:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240519235339.png]]
### One Pole, One Zero at 0Hz
- We have a capacitor and a resistor in series
- The step response starts at 1V, and decreases after. 
	- As soon as it jumps into 1V, the capacitor still must have 0V, as it hasn't charged. This means the rest of the voltage has to be going into the resistor, which is what $X$ is measuring. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520010254.png]]


### Initial and Final Value Theorems

- the initial value of step response = frequency response at infinite frequency 
- the final value of step response = frequency response at zero frequency

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520011421.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520011534.png]]

### One Pole, One Zero above the Pole

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520011702.png]]

The initial and final value theorems can help us here. Inputting 0 and $\infty$ into the frequency response can give us the initial and final values, and then we can put it in the formula given earlier.

### One Pole, One Zero below the Pole

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520011929.png]]

Same thing happens here! (The resistor and capacitor are in parallel, and then that is in series to the resistor). 
## Second-Order Responses
### Low-pass Filter
- This is a 2nd order response, with no zeros. We can get:
	- two real zeros
	- co-incident zeros
	- two complex zeros
	
Aight, let's look at an RCL circuit. For the frequency response, we use complex impedance. However for step responses, we don't need to use phasors anymore. Back to DC analysis baby. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520032418.png]]

Wahey, it's a second-order linear differential equation. Look back at your notes on how to solve that shit. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520032701.png]]

Comparing this to equation for the poles, it's very similar to the auxiliary equation. The values of $m$ in the auxiliary equations are the poles! Neat!
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520033004.png]]
When we get our general solution, we need boundary conditions to get a particular solution. And we can get those using the initial and final values! Pretty easy, as the capacitor starts at 0V (as it doesn't charge instantly), and eventually, it'll charge up to the step input of 1V. Well, except we just get $1=1$ in the end. Yeesh, that's not a useful boundary condition. Where else can we find a boundary condition?

$\frac{dX}{dt}= 0$ at $t=0$. A second order system has an inductor, which stops the current from changing too quickly, which means that our voltage must start without any movement, and then gradually increase. Welp, that's our boundary condition! Differentiate the general solution, and input!

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520033854.png]]
#### Case 1: Two Real Poles

If two poles are spaced far apart (where $Q<<1$ and $\mid p_{1} \mid >> \mid p_{0} \mid$). Plugging these into $X(t)$, we get $1-e^{p_{0}t}$. This is the dominant pole approximation. 

#### Case 2: Two Complex Poles 

Our poles are complex conjugates, with a negative real part. This means a high value of Q, and we'll get a "ringing" step response

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520034529.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520034600.png]]

#### Case 3: Co-incident Poles 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520034646.png]]

Problem: if two pole break frequencies are the same, then the difference in poles is 0, and you can't divide by 0. We have to go back and try a different solution. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520034724.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520035053.png]]
### Bandpass Filter

Wahey, more stuff that's like an EQ! A bandpass filter. This is where we get two poles, and one zero at 0Hz.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520035723.png]]

However, we can do a shortcut! We know the solutions for the low-pass filter. We can find the current flowing through the whole circuit, regardless of the order of the components. If we differentiate the low-pass filter example, then multiply it by C, then hey we get the current through the capacitor. If we know the current, we can multiply it by R to get voltage. We just need to get RC in terms of the poles. Look at the old equations and yep. In the end, we get:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520040752.png]]
#### Case 1: Two Real Poles
#### Case 2: Two Complex Poles
