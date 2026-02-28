[[Year 1]]

Let's define it again! An active filter that has gain as an integral part of the filter. A filter just means anything that changes gain based on frequency response. Passive filters rely on the inherent properties of the passive components (resistors, capacitors and inductors) to introduce impedances at specific frequencies. Active filters introduce active components (op-amps) to amplify or attenuate signals, with more control over the characteristics. Let's look at an example: 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520143131.png]]
Looks like a normal inverting op-amp, with a capacitor attached in parallel to the feedback resistor. We can do a regular frequency analysis, to find the break frequency, and then a op-amp analysis to find the gain:

- Let's focus on the feedback impedance first. This would be equal to the product of the two impedances, divided by the sum of the two impedances. This gets us $\frac{R_{2}}{1+j\omega R_{2}C}$. 
- As we don't just have resistors anymore, the inverting gain for the circuit is the input *impedance*, over the feedback *impedance* (and then multiplied by -1): $- \frac{R_{f}}{R_{in}}$. We just calculated the feedback impedance, so putting that over the input impedance gets us the working gain. This simplifies to $\frac{ -\frac{R_{2}}{R_{1}} }{1+j\omega R_{2} C  }$. Getting a 1 in the denominator is important, as it's easier to identify the pole, which is $p = \frac{-1}{CR_{2}}$. Inputting out values in, we get $-10^{5}rad/s$.  
- If we have a negative voltage gain, use $10\log_{10}(VoltageGain^2)$. 

So, why have this rather than the passive filters?
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520152521.png]]

We can get a passive two-pole filter with only resistors and capacitors. With this, it's impossible to get a Q-factor of more than a half:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520153145.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520153711.png]]

So what if we want a Q-factor more than a half? Well, we can turn this into an active version:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520154029.png]]

The resonant frequency is $\frac{1}{RC}$ and the Q-factor is $3- \frac{R_{1}+R_{2}}{R_{2}}$. This implies that the circuit *always* has a value of Q greater than 0.5. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520154218.png]]

# Tone Control
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520154230.png]]

Tone control circuits need to have adjustable characteristics. But variable capacitors and inductors are expensive. Variable resistors are not. How can we make a circuit that can vary gain at either high or low frequencies, while keeping the other half unchanged. only with variable resistors. Some nerd called Peter Baxandall solved this in the 50s, and almost every tone control circuit uses it. 

POG IT'S EXACTLY LIKE AN EQ NOW

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520161554.png]]

At high frequencies, the capacitor acts like a wire, which will short the circuit and it'll go through the left loop without feeding back. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520162343.png]]

At low frequencies, the capacitor acts like a break in the circuit, so the right loop will feedback into the circuit, and will act like a non-inverting op-amp. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520162124.png]]

When the potentiometer is midway, the voltage on both sides is the same, so no current flows through the capacitor, so we can just read it as a break in the circuit.

For mid-range frequencies, we have to do a full circuit analysis. Painful.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520163356.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520163715.png]]

Now, what if we want to target high frequencies or low frequencies? There are two forms a Baxandall tone control circuit:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520163848.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520163907.png]]