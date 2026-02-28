[[Year 1]]
## The Concept
For a DC circuit:
- $V_{out} = GV_{in}$

For an AC circuit, we need to use [[Phasors]]:
- $V_{out} = GV_{in}$
- Multiply each term by $e^{j\theta}$, $\mid V_{out} \mid e^{j\theta_{out}}  = \mid G \mid e^{j\theta_{G}} \times \mid V_{in} \mid e^{j\theta_{in}}$. 
- Collect RHS: $\mid V_{out} \mid e^{j\theta_{out}}  = \mid G \mid \mid V_{in} \mid \times  e^{j(\theta_{in} + \theta_{G})}$

But wait, $\theta_{out}$ is the same as $\theta_{in} + \theta_{G}$, so we can cancel out the $e$ terms. this means $\mid G \mid = \frac{\mid V_{out} \mid}{\mid V_{in} \mid}$ or the frequency in .In general, the complex gain, $G$, is a function of frequency, written as $H(j\omega)$.

It turns out, any network that's constructed from resistors, capacitors and inductors, always has a frequency response that can be expressed as the ratio of two polynomials.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518012346.png]]

These coefficients can be used to define a [[frequency response]], and it's certainly easier to store that in a computer. However, what does changing $a_{n}$ actually mean? It's a little too abstract to be useful.  What if you factorised each polynomial, and then factorised out a constant. in the end, it can be expressed as:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518012014.png]]

- The coefficients in the numerator are called zeros. 
	- If $j\omega = z_{n}$ the numerator evaluates to 0.
- The coefficients in the denominator are called poles. 
	-  If $j\omega = p_{n}$ the denominator evaluates to 0.

However, it's possible that some of the roots of the numerator are 0. In that case, it would instead be written as:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518013150.png]]
 
One final step, which makes it look more complicated, but I promise it'll make life easier later. We're going to factor out the minus coefficient from a root. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518014013.png]]
Doing this for every root, then collecting terms, we get:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518014057.png]]

See that fraction with all the constants? Let's define that as G, the gain, as all of those end up being a single constant. And in the end:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518014337.png]]

Phew, a lot of steps, but what does this mean? If $\omega = 0$ (aka DC), then all the terms on the right equal 1. Therefore, at zero frequency, if there's no zeros, then $H(\omega) = G$. If there are zeros, then it has to be approximated to $H(\omega) = G(j \omega)^{N}$. To define a single frequency response, we just need the number of poles, $N$, the gain, $G$, and the value of each pole $p_{N}$.

Ok that's the gain, but what are the physical meanings of the zeros and poles. What do they do to the frequency response? Ok let's consider the amplitude response, expressed in decibels. Let's put that entire equation into the decibel equation. Yay. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518015809.png]]

Long expression, but we can see the gain is $20\log_{10}(G)$, plus the effect of all the poles and zeros. These things affect the amplitude response.

Each zero adds $20\log_{10}(\omega)$ to the gain per decade. When rewriting for frequency, we get $G = 20\log_{10}(f) + 20\log_{10}(2\pi)$. Wahey, another straight line graph, and the gradient is 20dB/decade. 
- At low frequencies, $G \approx 0$. 
- At high frequencies, $G \approx 20\log_{10}(\frac{\omega}{{\mid z \mid}})$ 
	- *sometimes the frequency of zeros can be complex, hence the modulus*

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518030811.png]]

Poles are similar, but they subtract $20\log_{10}(\omega)$.
- At low frequencies, $G \approx 0$. 
- At high frequencies, $G \approx -20\log_{10}(\frac{\omega}{{\mid p \mid}})$ 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518032300.png]]

For both zeros and poles, the modulus of either number is the break frequency, and it dictates when the gain decreases by 3dB. The frequency response is equal to the

In short:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518032839.png]]

If we work out all the poles and zeros, we are able to sketch a frequency response with that information. In essence, we ignore the curvy bits, and focus on the limiting cases.

When we figure out the poles and the zeros, we can find the break frequencies of all the the zeroes and poles.

- First, consider what happens to the graph at 0rad/s.
	- Input into frequency response equation. What happens?
- Then, draw a horizontal line to the first break frequency. 
	- If it's a pole, draw a line downwards at a rate of 20dB/decade, and stop at the next break frequency
	- If it's a zero, draw a line upwards at a rate of 20dB/decade instead
- Stop at the next break frequency 
	- If it's the same, the gradient doubles down, and goes to 40db/decade.
	- If it's the opposite, the gradient cancels out, and it goes back being horizontal.

## The Other Way Round
Ok, so we've learnt how to approximate a Bode plot (with straight lines from poles and zeros, and how to get an amplitude from a frequency response. Cool! How do we go the other way round? If we're measuring the amplitude practically, how do we derive a frequency response from it?

As we know, the total frequency response is the product of the effect of all the poles and zero's effect on the frequency response. 

This is CERTAIN to be in the exam, so make sure you pay attention:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240519192732.png]]

So this method turns a gain, into a frequency response (where gain is calculated through the potential divider formula). 

Alternatively, if there's only one pole, you can see what happens at $\infty Hz$, then that go to the pole.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240519194910.png]]

For example here, simplify the resistor and the capacitor in parallel into one resistor, and then use the other capacitor to create a potential divider. 

Ok, let's say now, we're looking at a frequency response, and we want to estimate the poles or zeros. Well, figure out how many there are. Remember there can be two poles/zeros in one place, so check the gradient; one pole/zero changes the "gradient" by 20dB/decade. There's three ways:
- Draw the two asymptotes, where they meet is the pole/zero's break frequency
- Find where it drops by 3dB
	- To make it easier, find where it drops by 10dB, then divide by 3.
- If it doesn't get to drop by 3dB, find where it drops by half. Since it's a log scale, halfway between is $\frac{\log_{10}(f_{p}) + \log_{10}(f_{z})}{2}$, which nicely simplifies to $f_{p}f_{z} = f_{\frac{1}{2}}^2$.

What if the polynomials have complex roots?
## Things to Remember
- Number of zeros is never greater than the number of poles
- Number of poles is never greater than the number of capacitors + inductors
	- *normally it's equal to*
- Poles/zeros change the gradient by 20dB/decade above their break frequencies

