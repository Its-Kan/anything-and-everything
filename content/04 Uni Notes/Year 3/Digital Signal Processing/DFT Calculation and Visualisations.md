---
dateCreated: 2026-02-11 15:54
---
[Module:: [[Digital Signal Processing]]]

As a reminder, the [[Discrete Fourier transform]] assumes a signal of finite length is periodic with period length $N$, where frequencies are sampled at $\omega_{k} = \frac{2\pi k}{N}$
**DFT:**
$$X[k] = \sum^{N-1}_{n=0} x[n] \exp\frac{-{j2 \pi k n}}{N}$$
**IDFT:**
$$X[k] = \frac{1}{N} \sum^{N-1}_{n=0} X[k] \exp\frac{{j2 \pi k n}}{N}$$
where:
- $x[n]$ is the [[signal]] in the [[time domain]] 
- $X[k]$ is the [[signal]] in the [[frequency domain]] 
- $N$ is the total number of samples
- $n$ is the time index (the current sample we're looking at), ranging from $0$ to $N-1$
- $k$ is the frequency index (the current frequency bin we're looking at), also ranging from $0$ to $N-1$
```table-of-contents
```
---
## Calculation

> [!example]
> **Calculate DFT of $x[n] = [3,2,-1,1]$** 

Simple as putting the variables into the equation.
- We have 4 samples, so $N=4$
- The frequency and time index will range from $n, k = [0, 1, 2, 3]$ 

![[DFT Calculation and Visualisations-1.png]]

For the final step, we substitute $k = [0, 1, 2, 3]$ into the final equation to get the final vector. 

This is. A little long! We can substitute the constants into its own value:
$$W_{n} \triangleq \exp(\frac{-j2\pi}{N})$$
So, the equation becomes:
$$X[k] = \sum^{N-1}_{n=0} x[n]W_{N}^{{kn}}$$
Turns out, $W_{n}$ is the Nth root of unity formula: $(W_{N})^{N} = 1$. The exponential of the DFT (the kernel) can be computed as integer powers of a single complex number. Which of course, we can visualise as a locus of points around the origin on an Argand diagram. A circle!

So for example, for $N=8$, we would have $W_{8} = \exp(\frac{-j2\pi}{8})$. Then, we raise it from powers of $kn$, which means $7^{2} = 49$ jumps around the circle. But if we go around 8 times, we're back to the start and those factors double up, so we only have to look at $0$ to $N-1= 7$. 

![[DFT Calculation and Visualisations-2.png]]

So, we can see:
- $W_{N}^{kn}$ divide the unit circle into $N$ segments 
- $W_{N}^{kn}$ are periodic $W_{N}^{k(n+N)} = W_{N}^{kn}$
- $W_{N}^{kn}$ exhibit conjugate symmetry $W_{N}^{N-k} = W_{N}^{k*}$

We can express this as a matrix to quickly multiply then sum these terms. The first column/row represents $n,k = 0$, second represents $n,k = 1$, etc. 

![[DFT Calculation and Visualisations-4.png]]

![[DFT Calculation and Visualisations-5.png]]

We can use a [[Phasors|phasor]] to represent the "rotation" of each vector. 

![[DFT Calculation and Visualisations-6.png]]

## Discrete frequencies, k
How do we know what $n, k$ represent in a physical sense?
- We know $n$ is the sampling interval $\Delta t$, where we can calculate the discrete times $t_{n}$
- We need to determine $k$ to find the number of discrete frequencies $f_{k}$ or $\omega_{k}$

[[Discrete Fourier transform]] is defined on a set of discrete frequencies $f_{k}$, where $k$ is the frequency bin number. For a period of length $N$, $f_{k}$ are defined by the sequences with integer $k$ number of cycles within one period. The fundamental frequency $f_{1}$ would be one cycle within the period, and the following discrete frequencies are just integer multiples of the fundamental.

![[DFT Calculation and Visualisations-7.png]]

However since our signals are discrete, there is a limit to how fast the frequencies can be before we lose too much information. We've seen this before, it's the [[Nyquist frequency]], which is merely just half of the sampling rate.
$$\begin{align}
f_{s} &= \frac{1}{\Delta t} [\text{Hz}] \\
f_{Nq} &= \frac{f_{s}}{2} = \frac{1}{2 \Delta t} [\text{Hz}]
\end{align}$$
And with the DFT, the Nyquist frequency is $f_{k}$ where $k = \frac{N}{2}$
$$f_{Nq} = f_\frac{N}{2}[\text{Hz}]$$
