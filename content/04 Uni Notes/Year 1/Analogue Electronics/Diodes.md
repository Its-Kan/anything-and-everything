[[Year 1]]

Remember when we stuck together a p-type semiconductor and an n-type semiconductor, and it made it's own electric field? It's like it made itself a slide, and a depletion region, where there's no movement in electrons cause of the electric field. If we run current the wrong way (up the slide), the depletion region grows, the electric field gets stronger as there are more electrons on one side than the other, and it opposes the current. If it goes in the other way however, the existing electric field adds to the current, more electrons are able to go down the slide, and current can flow normally. Woah, that's a diode! 

Yeah just look at the diagram
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516213706.png]]

Diodes don't obey Ohm's law, but they do obey the Shockley equation!
# Shockley Equation: $I = I_{s}(e^{\frac{qV}{kTn}-1})$ 
- At room temp, $\frac{q}{Kt} \approx 40 = \frac{1}{25mv}$
- $I$, current
- $I_{s}$, saturation current. It's the current that would get through in the reverse bias
- $V$, voltage
- $e$, charge of an electron
- $k$, the Boltzmann constant
- $n$, a new variable added, it takes into account imperfections

Ideally, it would look like this: (that bottom current it floors to is the saturation current!)

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516220321.png]]

# Resistance

However, the equation doesn't take into account resistance! Of course, that doesn't actually exist. However, we can add a resistor before the ideal diode (not in practise! It's like the internal resistance of a battery), to make it act more like the experimental data!

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516221344.png]]

The equation now becomes:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516221639.png]]
- $R_{S}$, resistance of the resistor
- $V_{D}$, voltage through the diode

In examples where we don't know the voltage through the diode (most times sadly, as most times we're given the saturation current and $n$), we'll have to equate the currents of the resistor and the diode, estimate a voltage across the diode, then do iteration to get the current. Fun.

Remember you can do the spiral thing with the two lines and then get it.

# Zener Diode

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516231404.png]]

That's uh. Weird. It suddenly starts letting through a current when you force it hard enough? For positive values, it's similar to a normal diode, and is $I = I_{0}(exp(\alpha V)-1)$, where $I_{0}$ and $\alpha$ are constants for a diode. A lot of the time, they're used in reverse bias. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516232202.png]]

# Piecewise Linearity

It pretty much approximates the performance of a system, just by using straight lines. It's not accurate at all, but it makes the maths easy, and focuses on the parts that have the I-V characteristic. 

# Energy

Lights! Pretty lights! These happen when electrons jump the band gap, and that energy gets released as a photon. Wavelength is calculated through our favourite equation, $E=Hf=\frac{hd}{\lambda}=eV_{gap}$. 