[[Year 1]]
# Linear
## Explanation:

OK, as with all components, what does it do? Why do we need it?

Think of it as the gain knob in a guitar amp. The electric signals coming from the guitar pickups are way too small to power the speakers alone, so we have to amplify that signal. In comes the op-amp! It takes the difference between two inputs, and then multiplies that by a gain. Pretty simple! Of course that gain cannot come out of nowhere, so a power supply is connected, which also determines the gain of the op-amp.

## Equation:

The equation for this is $V_{out} = A V_{d} = a(V_{+}-V_{-})$. Wait, it's pretty easy! The output voltage ($V_{out}$) is the difference between the input voltages ($V_{d}$) multiplied by the gain ($A$). 

## Pinout:

Let's look at the pinout real quick. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514195952.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516030730.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514193212.png]]

Et voila! Not all of them are useful, so let's break it down:

- **Inputs:**
	- Pin 2 - $V_{in-}$, the inverting input (the negative one)
	- Pin 3 - $V_{in+}$, non-inverting input (the positive one)
- **Output:**
	- Pin 6 - $V_{out}$, the output
- **Power Supply:**
	- Pin 7 - $V_{CC+}$, positive power supply
	- Pin 4 - $V_{CC-}$, negative power supply


## Properties:

Ideally, they have six properties:

- **Infinite Gain:**
	- it should be able to target all frequencies
- **Perfect Differential Gain:**
	- the output, $V_{out}$, should be 0 when the two inputs, $V_{in+}$ and $V_{in-}$, are equal *(nothing to amplify when the difference is 0)*
- **No current flows into the inputs:**
	- also known as *infinite input resistance*
- **Zero Output Resistance:**
	- Thevenin resistance of the output should be 0
- **Inputs can range from $V_{CC-}$ to $V_{CC+}$**
- **Output can range from $V_{CC-}$ to $V_{CC+}$**
	- the range of the power supply!

Ok wait a minute, *infinite gain* AND *output can range from $V_{CC-}$ to $V_{CC+}$*? How? If the gain is infinite, that surely means the output can be infinite too? But it can't exceed the range of the power supply? Well, when it does reach the limits, we say its **saturated**. Yay.
## Feedback:

Wait a second, infinite gain *must* mean the output is always saturated right? Like, multiplying any input by ideally infinity should always give us the maximum output, right? Well, yes pretty much! But that's not useful is it? So how can we make it useful?

Let's look at the circuit again, but lets loop the output of the op amp back into the non-inverting input. This means there's only one input and one output.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514201358.png]]

Rearranging the equation gets us this:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514201459.png]]

As A tends to infinity, $\frac{A}{1+A}$ tends to 1, therefore this would be $V_{out}=V_{in}$. This, ladies and gentlemen, is negative feedback. This is when we feedback (no shit) the output back into the input, which means the output is never saturated, as the only "stable" state is when $V_{out}=V_{in}$. When $V_{out}$ is too high, the difference between $V_{out}$ and $V_{in}$ decreases, as the inverting input switches the polarity, and then $V_{out}$ decreases. When it's too low, the difference increases, and the output increases. This feedback loop happens until $V_{out}=V_{in}$.

## In Practise:

So if this pretty much just passes a voltage through, what's the point? Why have it over a wire? Remember, the op-amp doesn't pass current through it. Think of it as a break in the circuit, then starts a new voltage that's the same as it's input. That's why it's called a buffer!

Let's take a potential divider as an example. If we have two resistors of the same resistance in series, then the voltage of one would be half of the input voltage. If we placed an op-amp in-between them, then the input voltage would supply all it's voltage to the first resistor, then the op-amp picks up that voltage and transfers it to the second resistor, giving the same voltage. The power supply supplies that missing current.

### Example:

Let's look at a more complicated version of that.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514210334.png]]

AAAAAAAAAAAAAAA OK wait, let's stop and break it down.

Let's see, we have a negative feedback op-amp circuit. Our input is 1V, and our fed-back input is voltage divided. By what? Well, the inverting input *has* to have a voltage of 1V, as it's in equilibrium. As it's a voltage divider, each 1k resistor must be receiving 1V each. This means the output, that isn't voltage divided, *must* be 2V, which we see in the branch with just one resistor.
### Generalised:

#### Non-inverting
In general terms, this is called a non-inverting amplifier. It will change its output until the two inputs are the same, and then amplify it based on the voltage divider between the two resistors. What a guy.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514215401.png]]

If the op-amp can't get the two inputs to match, the op-amp is said to be *saturating*, and the output will try and get as close as possible.

The gain $(1 + \frac{R_{1}}{R_{2}})$ is called the *closed-loop gain*, and since it's based on the ratio between the two resistances, it's typically much less than the open-loop gain ($A$).

#### Inverting

This time, we have an inverting amplifier. Let's break it down.

Our non-inverting input is 0V, plain and simple. As the inputs *have* to match, the inverting input must also be 0V. We're gonna call it the virtual ground, cause while it's not actually connected to ground, it's being forced at 0V. Ok cool, so what's happening with $V_{in}$? The op-amp ensures the current in both resistors are the same, as no current flows through it. 

These two resistors' currents, can be defined differently though. As $V_{d}$ is 0, $R_{1}$'s voltage is $V_{in}$, and $R_{2}$'s voltage is $-V_{out}$ (as current is the opposite direction of $V_{out}$). Equating both and re-arranging gives us that equation!

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240514221211.png]]

#### Comparing both...
Let's compare the equations. First we have $V_{out} = V_{in} (1+\frac{R_{1}}{R_{2}})$, the non-inverting amplifier. No matter what the ratio is between the resistors, it will never go below a gain of 1. For the inverting amplifier, $V_{out} = V_{in} (-\frac{R_{2}}{R_{1}})$, our ratio can be whatever gain we want, however it will always be negative.

#### Summing 
OK, let's add more inputs with more resistors. The non-inverting input is at 0V, so the inverting input must be around 0, another virtual ground! 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516040505.png]]


Aaaaand this is the general form of a differential amplifier

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240516045302.png]]

# Non-linear
So, linear op-amps have it's output directly proportional to the input(s); it's multiplied by a constant. But, we can make circuits that have non-linear behaviour. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520164908.png]]

Let's look at a simple one. A comparator (LIKE FROM MINECRAFT)

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520170112.png]]

There's no feedback, almost always in saturation. It outputs the maximum or minimum voltage, based on which is higher. If inverting (-) is higher, then it outputs the negative voltage, and then the other way round for the non-inverting one.

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520184018.png]]

When $V_{in} = 0$, the circuit will shoot up to either the maximum positive, or maximum negative. This depends on the most recent $V_{in}$, whether it was positive or negative. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520190929.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520191032.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520191041.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520191110.png]]

Rectifiers determine the amplitude of sinusoidal signals, as the negative signals are blocked by a diode.  

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520191319.png]]
![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520192151.png]]

The problem with both of these passive circuits, is that diodes don't act in accordance to Ohm's law. There's a voltage drop at low currents, and then it starts increasing. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520192310.png]]

Active circuits solve this! However the new problem is the slew-rate of the op amp, as it can't change the voltage instantly. 

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520193207.png]]

These circuits can store the peak value of the incoming signal. There's a charging time constant (set by the )
# Non-Ideal
Sadly, all these equations and theories are for ideal op-amps

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520195908.png]]

Let's tackle them one by one:

## Bias and Offset Currents

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520200316.png]]

As we don't infinite impedance, $R_{in}$ has some current through it. That one doesn't matter as much, but another current is needed for the inputs to work, which is independent to the input signal. These currents are called bias currents. Analysing the circuit again, while assuming the currents get processed is:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520201206.png]]

To get rid of that offset, we need:

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520204400.png]]

## Offset Voltage

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520204459.png]]

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520204545.png]]
These can be fixed with the adjustment pins on the single op-amp.

## Output Impedance

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520204729.png]]
## Finite Open-Loop Gain

![[04 Uni Notes/Year 1/Analogue Electronics/xPasted Images/Pasted image 20240520204743.png]]