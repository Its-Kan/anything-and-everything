[[Year 1]]

Ok, let's look at a circuit we do knows: an RC circuit! Y'know? A resistor-capacitor circuit? Charges and discharges? Yep.

Remember decibels? The unit that tells us how much bigger one value (power or voltage) is to another, through powers of ten, (*well, convert to bels first, then the difference to the power of 10 is the gain*)? Gain specifically targets in input and output voltage, usually due to a component. 

Frequency response 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240517214242.png]]

Ok, let's plot how the voltage changes (in dB) based on the frequency of the source.

Just another quick definition: a decade is a power of 10. So for example, for a frequency against gain graph, 20dB/decade means for every magnitude of 10 in frequency (e.g. 100Hz to 1kHz), the decibels decrease by 20dB. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240517215610.png]]

Huh that's neat, there's two very obvious places when the change in dB is linear, right at the start and at the end. Remember back when we first looked at this circuit, and saw how higher frequencies meant the capacitor couldn't "catch up" in it's charging when the voltage oscillated? This shows that change!

Ok, so when does it start to lose gain more than maintain a constant one? If we draw the asymptotes for both sections when it becomes linear, the frequency at which they meet is called the **break frequency**. At this frequency, the gain is -3dB. Exactly? Why?

We'll have to analyse it sadly. We have an input voltage, a resistor, a capacitor, and an output voltage across the capacitor. This is just a potential divider! In a DC circuit, that would be $V_{out} = V_{in} \times \frac{R_{C}}{R_{T}}$. However, we're using sinusoidal sources, so we must translate this using [[Sinusoidal Sources and Complex Impedence]] and phasors. The impedance of the capacitor is $\frac{1}{j\omega C}$. The impedance of the resistor stays the same. So, it would get translated into $V_{out} = V_{in} \times \frac{\frac{1}{j\omega C}}{R+\frac{1}{j\omega C}}$, then simplifies into $V_{in} \times \frac{1}{1+j\omega RC}$. Yummy.

So, let's find an equation based on the frequency: our frequency response, the ratio of the voltages, $\frac{V_{out}}{V_{in}}$.  Using the previous equation, this is just $\frac{1}{1+j\omega RC}$! This is a complex number, where the magnitude is amplitude of the wave, and the argument is the phase. Ok, lets focus on the magnitudes: the numerator's magnitude is 1, and then use Pythagoras to get the denominator's magnitude. This makes the modulus $\frac{1} {\sqrt{1+(\omega RC)^2}}$. Ok, now the argument. Argument of 1 is 0. Using trigonometry, the argument of the bottom is $\arctan (\omega RC)$.  

Put them together into exponential form, we get:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240517231419.png]]

This is the equation for the frequency response! What does that mean? Well:
- The magnitude is the gain as a function of frequency
	- Or, the amplitude response: the modulus of the frequency response
	- $= \mid V_{out}/V_{in} \mid$
	- = $\frac{1} {\sqrt{1+(\omega RC)^2}}$
- The argument is the phase as a function of frequency
	- Or, the phase response, the argument of the frequency response
	- $=\theta_{out}-\theta_{in}$ 
	- $=\arctan (\omega RC)$

Ok, let's relate this to the the circuit. How does this link to the Bode plot?

Let's see the "limits" on the frequency response for the amplitudes. 
- If $(\omega RC)^2$ is much less than 1 (a low frequency), so much so that we can ignore it, which makes the amplitude is 1. 
	- Converting this to decibels ( as it's $\frac{V_{out}}{V_{in}}$, it would just be $20\log _{10}\mid H(\omega) \mid$ ), it's just 0. This is the flat part of the graph. 
- If $(\omega RC)^2$ is much larger than 1 (a high frequency), then the +1 can be ignored, which makes the amplitude $\frac{1}{{\omega RC}}$.
	- Converting $\omega$ to $2\pi f$ , then to decibels, then separate out the $f$, you would get $20\log _{10}\mid H(\omega) \mid = -20\log _{10}(f) - 20\log _{10}(2 \pi RC)$. 
	- Wait, this is the linear relationship! $y=mx+c$ and all that. That's the other part of the graph.
		- $m = -20 dB/decade$ 

Let's talk about the break frequency, $f_{b}$ then. Setting the magnitude of each linear line equal to each other get us $f_{b} = \frac{1}{2\pi RC}$, or $\omega_{b} = \frac{1}{ RC}$. As we saw, we can replace $RC$ in $\frac{1} {\sqrt{1+(\omega RC)^2}}$ with the break frequency, which would be $\frac{1} {\sqrt{1+(\frac{\omega}{\omega_{b}})^2}}$ (and the $\omega$ can be replaced with $f$). When at the amplitude is at the break frequency, then it would be $\frac{1}{\sqrt{2}}$. Converting that to decibels turns out to be around -3dB! This is why the break frequency is often referred to as the 3dB point.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518005151.png]]
If the resistor and capacitor swap places, then the analysis is the same, but we have an additional term on the numerator. 

For any circuit, analyse the limiting cases, and derive frequency response equations for both.  

# Second-Order Frequency Responses

Let's look at an RLC (resistor, inductor, capacitor) circuit. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520013045.png]]

To get the frequency response, just voltage divide all their complex impedances. We find it has two poles and no zeros. 

Since there's two poles, we have a quadratic! Plug into the quadratic equation to get values of $j\omega$ that make the denominators equal to 0. Also known as poles! In the end, we get: $j\omega = \frac{-R \pm \sqrt{R^{2} - \frac{4L}{C}}}{2L}$.

This is cringe. There's better ways to do this. Knowing where the two poles are doesn't help us with the frequency response. We need to introduce quantities that can help us.

For two poles or two zeros, we can replace the denominator of the general formula with:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520014656.png]]

We are characterising our system with two more variables: the resonant frequency and the quality factor. We're not analysing it with poles, it's either this or that. Why these two values though?

## Resonant Frequency
- it's the product of the two poles, but that's not really useful
- Let's analyse the general form at both low and high frequencies.
	- at low frequencies, we can ignore the variable parts, and it simplifies to 1
	- at high frequencies, we can ignore the $1+\frac{j\omega}{Q\omega_{0}}$ term, and it simplifies to $\frac{\omega_{0}^2}{\omega^2}$
	- The frequency at which these two frequencies meet, is when they're both equal. This means the resonant frequency, is the break frequency!
- This is also the frequency where the impedance of the capacitor and the inductor cancel out
	- $\omega_{=} \frac{1}{\sqrt{LC}}$
- And the frequency at which the maximum current flows in the circuit

## Q-factor
- Tells us the gain at the resonant frequency.  
- It's dependant on the resistor, while the resonant frequency doesn't
- IT'S LIKE THE THING ON AN EQ

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520024752.png]]

It's important to get the poles from the resonant frequency and Q-factor. If we input the denominator into the quadratic equation, you get two poles! 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520025526.png]]

We can make some approximations though:


![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520025259.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520025714.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520025739.png]]

To summarise:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520025803.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520030451.png]]

At a Q-factor of $\frac{1}{\sqrt{2}}$, something cool happens. They gain is always less than or equal to 0dB; there isn't an increase in gain.   

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520031255.png]]


![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520031433.png]]