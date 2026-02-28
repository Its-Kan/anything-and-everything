[[Year 1]]

### Cissoid Recap:
#### $Acos(cot + \theta) = Re(Ae^{j \theta}e^{j \omega t})$ 
 
Adding up the real parts of two cissoids that are conjugates of each other gives you a real cosine oscillation.

### Circuit Analysis

- Use superposition

#### $i_{c} = \frac{V_{out_c-}}{Z_{r}}$

#### Shortcuts:

##### 1:
- The output from the positive frequency and the output from the negative frequency analysis are complex conjugates.
- They *have* to be, as their sum is always real.
- So, just do the positive analysis.

##### 2:
- If taking just the positive frequency cissoid, you'll only get half the amplitude, as adding the complex conjugates of the frequencies add up to the real sinusoid. 
- Use the sinusoidal amplitude instead of the cissoidal one, to avoid multiplying and dividing by 2.

##### 3:
- $x(t) =Acos(\omega t + \theta)$
- converts into $x(t) = Ae^{j\theta}$


### Summary:

1. Replace capacitors with an impedance of $\frac{1}{j\omega C}$
2. Replace inductors with an impedance of $j\omega t$
3. Express sinusoidal inputs in phasor form
4. State the circuit using the phasor representation of the voltages and currents
5. Determine the output by taking the real part of the output phasor and representation using: $V(t) = Re()$

