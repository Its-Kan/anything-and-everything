[[Year 1]]
[[AC Circuit Analysis I]]

Uhoh. Buckle up, this might be long.

So cissoids don't exist. Bummer. But, adding two cissoids can give us a cosine! They will have to be in complete antiphase though, so the imaginary parts cancel out, and we just get an oscillating real part: a cosine wave.

Take this circuit:



Unless we do some very long nodal analysis, we can't do this. Unless, we replace each source with two cissoidal sources! Then, we can use [[superposition]] on each source! Neat!



As we want to focus on voltage, we'll just do the [[superposition]] process on the current sources. We'll treat the voltage sources as a wire, and the current sources as breaks in the circuit, and then calculate the voltage through the resistor from each current source, then add them together.




Add them together:



Imaginary voltages and currents don't exist in the real world, so the result *has* to be real.

We can do this quicker. The output from the positive frequency analysis and the negative frequency analysis are complex conjugates. This means their real parts are the same, and we need to double it.

However, we needed to halve the sinusoidal source when we separated it into two cissoids. To make it even quicker, create a cissoid with a positive frequency, and an amplitude equal to the real sinusoidal source. Then solve it!

Ok, remember when we cancelled out all the $exp(j \omega t)$ when doing nodal analysis? We can do the same here as well, so *for the calculations*, the sinusoid goes from $x(t) = Acos(\omega t + \theta)$ to a cissoid, $x(t) = Aexp(j\theta)$.  



Crazy thing, almost everything works! Kirchhoff's current and voltage laws, Thevenin and Norton's Theorems, Linearity and Superposition, Passive Components in Series and Parallel, and Nodal Analysis! *Shockley's equation doesn't work since it's not linear.* 

Replace real numbers with phasors, and complex impedance instead of resistance! 

Remember the phasor representation is just $Aexp(j\theta)$. Convert all sources into it! 