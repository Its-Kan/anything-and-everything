[[Year 1]]

Sadly, real op-amps don't behave like ideal op-amps. They *should* act the same at all frequencies, but in real life, that doesn't happen.

# Bandwidth
But before that... Alright I'll come out and say it. What is bandwidth?

Simply put, it's the range of frequencies within a certain amount of the maximum gain.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518035536.png]]

For example:
- the 3dB bandwidth are the range of frequencies from it's max dB, to 3dB.
- the 10dB bandwidth has a larger range of frequencies 

# Dependent Sources
- So far, all voltage and current sources have been constant. They don't change, so they're independent sources
- Dependent sources do exist, and are drawn with a diamond. They depend on other sources

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518035844.png]]

Op-amps can be modelled as a dependent source, but only at low frequencies:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518035946.png]]

At higher frequencies, we need to update the model. It looks scary, but hold on:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518040036.png]]

Let's break it down!
- The first diamond is a voltage dependent current source $I_{B} = B \times V_{d}$. 
	- $B$ being an arbitrary 
- That current goes through a resistor and a capacitor
- The total impedance is $\frac{R}{1+j\omega RC}$ (multiply impedances, divide by sum of impedances)
- $V_{out} = V_{d}$
	- $= I_{B} \times \frac{R}{1+j\omega RC}$
	- $= V_{d} \times \frac{BR}{1+j\omega RC}$ 

Aha! This model is frequency dependent, unlike the ideal op-amp equation ($V_{out} = AV_{d}$). If we set $\omega = 0$, then it turns out $BR = A_{DC}$. So, looking at the gain as a function of frequency gets us $A(\omega) = \frac{A_{DC}}{1+j\omega RC}$, or in hertz, $A(f) = \frac{A_{DC}}{1+j2\pi fRC}$. If replace $f_{d}$ with it's other formula ($\frac{1}{2\pi RC}$), then we'd get $\frac{A_{DC}}{1+j \frac{f}{f_{d}}}$. Huh. It looks like what a single pole is. The op-amp is introducing a pole!

Let's take a look at an actual op-amp open loop bandwidth. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240518043726.png]]

Uh, it starts decreasing at higher frequencies. Why? It keeps it stable. If there's a system that has negative feedback, it still need to be negative feedback. But as you can see, the component introduces a phase shift. If the phase shift gets to $180\degree$, the gain will start oscillating. 

# Gain as a Function of Frequency
So as we've discussed, gain changes based on the frequency, manipulated by poles and zeroes. For a single pole, the break frequency is $f_{p} = f_{d} \times \frac{A_{DC}}{G_{DC}}$. 

The 3-dB bandwidth 

