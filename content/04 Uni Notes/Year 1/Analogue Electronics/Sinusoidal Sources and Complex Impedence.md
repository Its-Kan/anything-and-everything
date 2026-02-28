[[Year 1]]
# Introduction
Aight, let's look at a circuit, with a sinusoidal voltage source. The voltage changes via the equation $V_{0}sin(\omega t)$:  
- $V_{0}$ is the voltage amplitude
- $\omega$ is the angular frequency of the oscillation
- $t$ is time
A pretty basic sin wave formula! 

Ok now we know that, let's not get overwhelmed and slowly work through a basic circuit with that as the power source.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515023131.png]]

Let's do a nodal analysis! Let's hope to fuck you remember that you twat. Rewrite the circuit by selecting a point to be ground, then label each node. Now make an equation for each component.
- Resistors obey Ohm's law, which is $V=IR$. Current is the same everywhere, so it would be $V_{0}sin(\omega t) - V_{C} = IR$. 
- Capacitors have the equation $I = C \frac{dV_{c}}{dt}$. Remember $V_{C}$ is a function of $t$.

Subbing both of these in and simplifying for $V_{C}$ gets us (I don't want to write this out in LaTeX):
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515025107.png]]

# Limiting Cases
Looks hard to understand, but let's break it down in terms of limiting cases.  
## Slow sine waves, where $\omega << \frac{1}{RC}$
- If $\omega$ is waaayyyy smaller then $\frac{1}{RC}$, then $\omega RC$ is pretty much 0. This means $(\omega RC)^{2}$ tends to 0, and $tan^{-1} (\omega RC)$ also tends to 0. This means we can simplify the equation to:
	- $V_{C} \approx V_{0}sin(\omega t)$
- As the time period is much greater than the time constant, the capacitor can "keep up", and charge according to the sine wave.
## Fast sine waves, where $\omega >> \frac{1}{RC}$
-  If $\omega$ is waaayyyy bigger then $\frac{1}{RC}$, then the 1 in $1 + \omega RC$ is negligible, and in $tan^{-1} (\omega RC)$, a very large number tends towards $90\degree$. So, the equation can be simplified to:
	-  $V_{C} \approx \frac{V_{0}}{\omega RC} sin(\omega t)$
- The time period this time is much smaller than the time period. The capacitor lags behind by $90\degree$. When the voltage source is positive, the capacitor is charging, and it discharges as soon as it becomes negative. It can't charge quick enough, so the amplitude is far less than the input voltage. 
## Break frequency sine waves, where $\omega = \frac{1}{RC}$
- Ok, so the break frequency is when the angular frequency is the inverse of the time constant. At this frequency, the output is 3 dB below the input signal. The phase difference is also $45\degree$.
	- $V_{C} = \frac{V_{0}}{\sqrt{2}} sin(\omega t - 45\degree)$

# Recap

## Resistors:
- Ohm's law, where current is proportional to the potential difference. 
	- *Ohm's law can be used for capacitors and inductors, but only for very few special signals (cissoidal signals)*
## Capacitors:
- $C=\frac{Q}{V}$, capacitance is the ratio of charge to potential difference between the plates
- $\Delta Q = C \Delta V$ 
- $I = \frac{dQ}{dt} = C \frac{dV}{dt}$, current is the rate of flow of charge
## Inductors:
- $e = L \frac{dI}{dt}$, inductance is the ratio of emf (across the inductor) to rate of change of current through inductor.
- $I = \frac{1}{I} \int e\, dt$  

# Nodal Analysis:
No fun way to do this, just have to go through each node and each component, and form components for each of them.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515034401.png]]

And those equations are:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515034428.png]]

In order:
1. Voltage at node A, is a function of time from the sinusoidal source
2. Kirchhoff's Current law at the junction at B
3. The inductor equation
4. Ohm's law across the resistor
5. The capacitor equation

After this, we gotta solve some simultaneous equations! To make this easier, we can differentiate all terms in equation 2 by t, and substituting in gets us some values. Yippee.

# The Easier Way
Get baited my boy, there is an easy way, where we can get those components to obey Ohm's law.

Let's model a sin wave as focusing purely on the vertical component of a point rotating on a circle. 

Let's do this on the imaginary plane, so it would be written as $z = Ae^{j\theta}$. What happens if we differentiate it? $\frac{dz}{dt}= Aj\omega e^{j\omega t}$ which, when substituted with the original equation, gets us $\frac{dz}{dt}= j\omega z$. Huh. Multiplying a point by $j\omega$ is the same as differentiating it. Well, let's do that instead!

Looking at the capacitor equation, $V_{C} = V{0}e^{j\omega t}$, differentiating it gives us $\frac{dV_{C}}{dt}= j\omega V_{C}$. How easy! $I_{C} = C \frac{dV_{C}}{dt}= j\omega C V_{C}$, which simplifies into $V_{C} = \frac{1}{j\omega C} I_{C}$. Huh, that looks like Ohm's law, just with a more complicated resistance.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515040901.png]]

Wait... this only applies if voltages and currents are complex cissoids. But... all voltages and currents are real. How can we use this to apply in the real world?

# Complex Impedance

AAAAAAAAAAA that's a long and scary thing with long and scary stuff. OK, remember, we want everything to act like it's obeying Ohm's law. If we use the classic equations for it, then it's a little cringe.
# Cissoids

A cissoid, well the the one we're looking at, you can think of as a rotating circle, stretched out over time. A corkscrew!

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515174922.png]]

As we just proved in the previous section, finding the differential of this curve is as easy as multiplying it by $j\omega$, and through the same logic, the integral of the curve is dividing by $j\omega$. Cool! If we had a source that's cissoidal, that means the components will look like this:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240515175908.png]]

HOLY SHIT IT'S SO MUCH EASIER! And for the record, *impedance* is the ratio of voltage to current of components, that aren't just resistors. *Resistance* implies a real number, while *impedance* can be complex.

But again, voltages and currents aren't imaginary, so what's the point? Well, Joseph Fourier figured out a funny thing:
- "Any real signal can be expressed in terms of a weighted sum of a large number of cissoids"

Wait, that means we can get real signals, out of cissoids! For sinusoidal signals, it ends up being

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516045538.png]]

Impedance is the ratio of the voltage cissoid, and the complex cissoid. Since the part that depends on time cancels out, impedance is a value of the component, not due to time.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516045621.png]]

**C.I.V.I.L.** Remember it. It stands for "Capacitors, Current, Voltage, Current Inductors".

For **capacitors**, the **current** is $90\degree$ ahead of the **voltage**
The **voltage** is $90\degree$ ahead of the **current** for **inductors**

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516045914.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516045943.png]]