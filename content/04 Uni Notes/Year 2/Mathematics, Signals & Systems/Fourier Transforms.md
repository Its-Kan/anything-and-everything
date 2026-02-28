---
share_link: https://share.note.sx/7v0n6ku2#bO9qSE3XI8PI10NR5nPPzYYZcmXhU4gOkPoFtWeCXeU
share_updated: 2025-11-18T00:24:58+00:00
---
**Year**: [[Year 2]]
**Subject**: [[Mathematics, Signals & Systems]]
**Topic**: Fourier Transform
**Date Created**: 2025-01-01

--- 
As we know, transforms help us see problems in a different light, making it easier to manipulate or understand. Logarithms help us see data over larger scales, represented through [[Bode Plots]]. [[Laplace Transforms|Laplace Transforms]] help us see [[Differential Equations]], represented in the [[s-plane]]. The [[Fourier series]] and [[Fourier transform]] helps us see what frequencies are present in a signal.
## Review
As a reminder, the [[single-sided Laplace transform]] is defined by:
$$ F(s) = L[f(t)] \triangleq \int^{\infty}_{0}f(t) e^{-st}dt$$
Where:
- $f(t) = 0 \quad \text{for} \space t<0$
- Converts time-domain functions so s-domain functions, where $s = \sigma + j \omega$
- The lower limit at $0$ allows a signal to start at $t = 0$, or at a delayed time. 
### Orthogonality and Normalisation
One important use of the dot product is to establish if two vectors are perpendicular (or orthogonal if they're at right angles but not touching). Using the dot product on two of the same vector gives us the vector squared, and we can also normalise a vector to its unit length

Turns out, the same rules are valid for a new concept called [[inner product|inner products]]. This is their notation: 
$$\langle f, g \rangle = \int^{z_2}_{z_{1}} \overline{f(x)} g(x) \space dx$$ Where:
- $\overline{f(x)}$ is the complex conjugate
- the interval is $[x_1, x_2]$

With it being analogous to vectors, then the functions:
- are orthogonal over the interval, then the above is $=0$. 
- are the function squared if both of the functions are the same
- can be normalised using $\hat{f} (x) \frac{f(x)}{\sqrt{\int^{z_2}_{z_{1}} \overline{f(x)} f(x) \space dx}}$
- are equal to 1 when the functions are both unit. 
## Sinusoidal Basis Functions
Sinusoids are defined by frequency, amplitude and phase. If we restrict it to just sines and cosines, then we just have frequency and amplitude. This means sinusoids can be used to describe signals in an interpretable fashion, using the relative amounts of different frequency components it might contain.
### Cosines
Let's consider the integral: 
$$\int^{\frac{T}{2}}_{\frac{-T}{2}} \cos(m \omega_{0}t) \cos(n \omega_{0}t) \space dt$$ Where:
- $\omega_{0} = \frac{2\pi}{T}$
- $m$ and $n$ are positive integers

We have two real functions, so no need to use the complex conjugate. Each function represents a number of complete cosine cycles over the time interval, where $m$ and $n$ determine the number of cycles.

Ok let's try and solve it.

![[Fourier Transform cos deriv 1.png]]
![[Fourier Transform cos deriv 2.png]]
![[Fourier Transform cos deriv 3.png]]
### Summary
![[Fourier Transform sinusoid summary.png]]In short, it turns out any mixture of cosines and sines gives us an orthogonal set (think of an axis and how it has 3 perpendicular lines. All three values are independent of each other, but putting them together gives us a unique value). This means we can represent any signal using these functions!
## Fourier Methods
The previous results can be applied to provide a [[frequency domain]] representation of a signal, but only over a restricted time interval of length $T$. This is the basis of the [[Fourier series]].
### (A)periodic functions
So, as said before, sinusoids can form an orthogonal set of functions over a restricted time interval of length $T$. [[Fourier series]] are the tool we use on *periodic functions*, like sin, triangle, square or sawtooth waves.
![[Fourier Transform periodic waves.png]]
However, there is a distinction between period and frequency. They have the same period, but only the sin wave has a specific, definable frequency. The other waves are the sum of multiple frequencies.  

*Aperiodic functions*, of course, don't have regular patterns. This could be a damped oscillation, an oscillated overshoot step response, or a sigmoid curve.
### Sine-Cosine Fourier Series
In general, for a periodic function of period $T$, a [[Fourier series]] represent a single period of a *piecewise continuously differentiable periodic function, $x(t)$*, as an infinite series of sine and cosine functions of specific frequencies. 
$$x(t) = a_{o} + \sum^{n=\infty}_{n=1}(a_{n} \cos(n \omega_{0}t) + b_{n} \sin(n \omega_{0}t))$$Where $\omega_{0}= \frac{2\pi}{T}$ and the Fourier coefficients depend on the function's period.
$$\begin{align}
a_{0} &= \frac{1}{T} \int_{\langle T \rangle} x(t) \space dt \\
a_{n} &= \frac{2}{T} \int_{\langle T \rangle} x(t) \cos(n \omega_{0}t) \space dt \\
b_{n} &= \frac{2}{T} \int_{\langle T \rangle} x(t) \sin(n \omega_{0}t) \space dt
\end{align}$$

![[Fourier Transform coefficientrs.png]]The $a_n$ and $b_n$ coefficients in these sinusoidal basis functions control the amounts of each function is in the infinite sum. The $a_0$ coefficient is a special case which reflects the average value over the entire period, and is a constant offset.

To find the values of the coefficients, we can multiply out the series expansion of $x(t)$ by any basis function, and then integrate over that period. For example, to establish the value of the coefficient $a_n$, we can evaluate:
![[Fourier Transform evaluate coefficients.png]]Hence
$$\begin{align}
a_{n} &= \frac{2}{T} \int_{\langle T \rangle} x(t) \cos(n \omega_{0}t) \space dt
\end{align}$$
The specific criteria for a [[Fourier series]] expansion to be valid are:
- $x(t)$ must be a single valued function
- $x(t)$ must have only a finite number of maxima and minima
- $x(t)$ must be absolutely integratable over one period (which means the integral is less than infinity)

In short:
- Fourier series are the appropriate tool for the frequency continuous-time function - by as an infinite sum of sinusoidal functions. 
- The signal/function is assumed to be infinitely long and perfectly periodic
- The period of the signal/function defines the particular set of for the Fourier series expansion. 
- The function $x(t)$ can have multiple discontinuities in its value, gradient, or higher derivatives. 
- The coefficients of the infinite series expansion can be integrating the function over one period after multiplying (modulating) it by any chosen basis function.

> [!EXAMPLE] Example
> ![[Fourier Transform EXAMPgE 1.png]]
> So, our signal $x(t)$ is periodic, where $T = \pi$,  so our angular frequency is $\omega_{0}= 2 \space \text{rad} \space \text{s}^{-1}$. So the set of frequencies for [[Fourier series]] expansion is $n \omega_{0} = 2n \space \text{rad} \space \text{s}^{-1}$, where $n = 1, 2, 3, 4 ...$
> So, putting it into the [[Fourier series]] expansion equation gets us $x(t) = a_{0} + \sum^{n=\infty}_{n=1}(a_{n} \cos(2nt) + b_{n}sin(2nt))$.
> Now, we need to find the Fourier coefficients, $a_0$, $a_n$ and $b_n$ by plugging it into the equations before. Turns out, we get: $$ \begin{align}
> a_{0}&= \frac{2}{\pi} \\
> a_{n}&= \frac{1}{\pi} \frac{4}{1-4n^{2}} \\
> b_{n}&= 0
\end{align} $$
> and then we put it back into the general formula to get
> $$x(t) = \frac{2}{\pi} + \sum^{n=\infty}_{n=1} \frac{1}{\pi} \frac{4}{1-4n^{2}}\cos(2nt)$$
 
> [!example] Example
> ![[Fourier Transform example 2.png]]
> So now, we have a piecewise periodic function. Our period is $T = 2\pi$, so let's set the interval to $[ 0,2\pi ]$, with an angular frequency of $\omega_{0}= 2 \space \text{rad} \space \text{s}^{-1}$, and $n \omega_{0} = n \space \text{rad} \space \text{s}^{-1}$, where $n = 1, 2, 3, 4 ...$
> Let's calculate each coefficient:
> Since $a_{0}$ is the average DC signal for the entire function, we can plug it in. We get
> $$ a_{0}= \frac{1}{\pi}$$
> However, turns out when $n$ is odd, $a_{n}$ evaluates to 0. 
> When $n$ is even, we get  
> $$ a_{2n} = \frac{2}{\pi} \frac{1}{1-n^{2}}$$
> For $b_{n}$ we have a special case when $n=1$, where
> $$ b_{1} = \frac{1}{2}$$
> However for the rest of $b_{n}$, it also evaluates to 0.
> <br>
> Adding the initial term $a_{0}$, the special case of $b_{1}$, and the infinite summation of the even values of $a_{2n}$, we get:
> $$x(t) = \frac{1}{\pi} +\frac{1}{2}\sin(t) + \sum^{n=\infty}_{n=2,4,6,8} \frac{2}{\pi}\frac{1}{1-n^{2}} \cos(nt)$$
>

When the function is either **even**, where $f(x) = f(-x)$ and the $-ve$ can disappear, or **odd**, $f(-x) = -f(x)$ where the $-ve$ can be moved out, we can simplify the process.
- When the function is even, then $b_{n} = 0$. This means the function is comprised of only cosine functions.
- When the function is odd, then $a_{n} = 0$. This means the function is comprised of only sine functions
However the first harmonic may still need to be evaluated.
### Amplitude-Phase (Harmonics) Form of Fourier Series
In general, it's possible to write a mixture of a cosine and a sine signal as a single sinusoidal frequency, but scaled in amplitude and shifted in phase. Remember, we did this in A-level.
$$ \begin{align}
&A \cos(\omega t) + B sin(\omega t) \equiv C \sin(\omega t + \phi) \\
\text{where} \quad &C = \sqrt{A^{2}+B^{2}}, \quad \sin(\phi) = \frac{A}{C}, \quad \cos(\phi)=\frac{B}{C}
\end{align}$$
Applying this to the [[Fourier series]], we can get a form that purely focuses on amplitude and the phase with one Fourier coefficient: $$\begin{align}
&x(t) = a_{0} + \sum^{n=\infty}_{n=1} A_{n} \sin(n \omega_{0} t + \phi_{n}) \\
\text{where} \quad &A_{n}= \sqrt{a_{n}^{2}+b_{n}^{2}}
\end{align}$$This is sometimes called the **harmonics form** of a [[Fourier series]], which stresses the fact that the signal is represented as the linear sum of a weighted set of sinusoids with frequencies that are integer multiples of the fundamental angular frequency.
### Exponential Fourier Series
As we can define $\sin$ and $\cos$ in their exponential forms to get a new expression for our general [[Fourier series]] expansion: 
$$\begin{align}
\sin(\theta) &\triangleq \frac{e^{j \theta} - e^{-j \theta}}{2j}\\
\cos(\theta) &\triangleq \frac{e^{j \theta} + e^{-j \theta}}{2j}
\end{align}$$ Which turns into the **complex exponential form**, which we call the **Fourier synthesis**:
$$\begin{equation*}
x(t) = \sum_{n=-\infty}^{\infty} c_n e^{jn\omega_0 t}
\end{equation*}$$
where$$\begin{align*}
c_n &= \frac{1}{2}(a_n - jb_n) \quad \text{for positive } n \\
c_{-n} &= \frac{1}{2}(a_n + jb_n) = \overline{c_{n}}\\
c_0 &= a_0
\end{align*}$$
We can find the Fourier coefficients in one step, called the **Fourier analysis**:
$$c_{n}= \frac{1}{T} \int_{\langle T \rangle} x(t) \exp (-jn \omega_{0}t) \space dt$$In summary, all of the forms of Fourier series are equivalent
$$\begin{align}
x(t) &= a_{0} + \sum^{n=\infty}_{n=1} (a_{n} \cos(2\pi nt) + b_{n}\sin (2\pi nt)) \\
&= a_{0} + \sum^{n=\infty}_{n=1} A_{n} \sin(n \omega_{0}t + \phi_{n}) \\
&= \sum^{n=\infty}_{n=- \infty} c_{n} e^{jn \omega_{0}t}
\end{align}$$
## Line Spectrum of a Periodic Signal 
We can find a measure of the total amount of each sinusoid contained within the original signal at each specific frequency, so we can visualise what frequencies are present in the original signal on a graph. We can do this by finding the moduli of the **Fourier coefficients**.$$
\begin{align}
|c_{n}| = \frac{1}{2} \sqrt{{a_{n}}^{2} +{b_{n}}^{2}} \quad &\text{in complex exponential form} \\
A_{n} = \sqrt{{a_{n}}^{2} +{b_{n}}^{2}} \quad &\text{in amplitude-phase form}
\end{align}
$$Doing this for each set of Fourier coefficients gets us a graph with discrete values of frequencies and their amplitudes:![[Fourier Transform line spectra.png]]
### Spectral Energy and Parseval's Theorem
The spectrum is discrete and not continuous due to the periodic nature of the original function, as the basis functions need to fir the repeat interval precisely. However a consequence of this is that the signal has infinite energy (as it repeats), however the signal energy over a single period is finite. This is called a **power signal**.
In general, the **instantaneous power** for a signal is:
$$P(t) = |x(t)|^{2}$$and the **total energy** over a single period is: $$E = \int_{\langle T \rangle} |x(t)|^{2} \space dt$$
And therefore the **average power** is:$$P = \frac{1}{T} \int_{\langle T \rangle} |x(t)|^{2} \space dt$$Then replacing $x(t)$ with the general Fourier exponential series expansion, we can find:$$E= T \sum^{n=\infty}_{n= - \infty} |c_{n}|^{2}$$Isn't that interesting. The average power over a single period is directly equivalent to the sum of the squares of the coefficients. We call this [[Parseval's Theorem]].$$
\frac{1}{T} \int_{\langle T \rangle} |x(t)|^{2} \space dt = \sum^{n=\infty}_{n = - \infty} |c_{n}|^2
$$Mathematically, this shows us that the Fourier series is a **unitary transformation**, there is no gain/scaling associated with the transformation between the time and frequency domains. The energy over a period is the same whether  we're in the time or frequency domains.
Using the trigonometric [[Fourier series]] expansion, we can translate [[Parseval's Theorem]] into:
$$\frac{1}{T} \int_{\langle T \rangle} \vert x(t) \vert^{2} \space dt = {a_{0}}^{2} + \frac{1}{2} \sum^{n= \infty}_{n=1} ( {a_{n}}^{2} + {b_{n}}^{2})$$Physically, we can interpret this in terms of power being dissipated within a resistor, which is our handy power equation:
$$P=\frac{V^{2}}{R}$$
for a perfect component. If a purely sinusoidal voltage of amplitude $A$ was applied to a $1 \ohm$ resistor, then the mean power dissipated would be $\frac{A^{2}}{2}$. For a cosine signal, [[Parseval's Theorem]]  states that the total dissipation is the sum of the power dissipated by each separate frequency component, which means: $$\frac{1}{T} \int_{\langle T \rangle} \vert x(t) \vert^{2} \space dt= {a_{0}}^{2}+ \frac{1}{2} \sum^{n=\infty}_{n=1} {A_{n}}^2$$
### Signal Shifts and Symmetries 
We've covered the odd and even function symmetries, but there are other types of symmetries and structures that can lend us some shortcuts and patterns in the Fourier series expansion.
#### Odd Half-Wave Symmetry
This is applicable to periodic signals where the second half of the period is the negative of the first half (or mirrored in the x-axis). In maths:$$x(t) = -x(t+ \frac{T}{2})$$Where shifting the second half of the signal through half of a period, and then flipping it gives us a zero result. Overall:
- A function with odd half-wave symmetry can be constructed from **only odd harmonics.**
#### Quarter-wave symmetry
##### Even
This is when a signal is half-wave symmetric, and also has odd or even symmetry about a quarter-period point ($\frac{T}{4}$ from an end or the centre), and in maths:$$
\begin{align}
x(t) &= -x\left(t+ \frac{T}{2}\right)\\
x(-t) &= x(t)
\end{align}
$$![[Fourier Transform quarter wave symmtery.png]]
Overall:
- A function with even quarter-wave symmetry can be constructed from **only odd cosine harmonics.**
##### Odd
Similar to even, but:$$
\begin{align}
x(t) &= -x\left(t+ \frac{T}{2}\right)\\
x(-t) &= -x(t)
\end{align}
$$![[Fourier Transform odd quarter wave.png]]
Overall:
- A function with even quarter-wave symmetry can be constructed from **only odd sine harmonics.**
## The Fourier Transform
So, the Fourier series can only handle continuous-time periodic functions, which then produces a discrete line spectrum with a fixed spacing of $\omega_{0} = \frac{2\pi}{T} \space \text{rad} \space \text{s}^{-1}$. Functions with longer periods have closer lines. So, what if the period can be arbitrarily large ($T \rightarrow \infty$)? Well, the lines will get closer together, until the discrete spectrum becomes continuous. The previously discrete angular frequencies $n \omega_{0} = \frac{2\pi n}{T}$ becomes a continuous variable $\omega$, and the infinite sum turns into an integral. $$
x(t) = \frac{1}{2\pi} \int^{\infty}_{- \infty} e^{j \omega t} \int^{\infty}_{- \infty} x(\tau) \exp(- j \omega \tau) \space d \tau \space d \omega
$$Which becomes our definition of the [[Fourier transform]]!$$\mathscr{F} [x(t)] = X( \omega) = \hat{x}(\omega) \triangleq \int^{\infty}_{- \infty} x(t) \exp (- j \omega t) \space dt$$Which changes the viewpoint from an infinite, non-periodic continuous-time signal $x(t)$ to an infinite non-periodic, continuous-frequency spectrum $X(\omega)$.

The Inverse [[Fourier transform]] reverses the process, switching from frequency back to time: $$x(t) = \frac{1}{2\pi} \int^{\infty}_{- \infty} X(\omega) e^{j \omega t} \space d \omega$$
 Similar to [[Fourier series]] expansion, there are mathematical criteria for a Fourier transform to exist, but the dominant one is that the signal must be absolutely integrable, where$$\Vert x \Vert_{1} = \int^{\infty}_{- \infty} \vert x(t) \vert \space dt < \infty$$ $\Vert x \Vert_{1}$ is called the *L1 norm*, and is a measure of the total size of the signal. 
### Properties of the Fourier Transform
The [[Fourier transform]] looks similar to the two-sided [[Laplace transform]], which looks like:$$F(s) = L[x(t)] \triangleq \int^{\infty}_{- \infty} x(t) e^{-st} \space dt$$In signal processing and control theory, it's assumed that $f(t)= 0$ for $t<0$, and the [[single-sided Laplace transform]] is used. However, there are times when the signal may be non-zero for negative time. The two-sided Laplace transform can be used for this, however we can get the [[Fourier transform]] from this by setting $s=j \omega$, which means the basic properties of both transforms mirror.

**Linearity**: Can be "multiplied out" $$\mathscr{F}[ax(t) + by(t)]=a \mathscr{F}[x(t)] + b \mathscr{F}[y(t)] = aX(\omega) = bY(\omega)$$**Scaling**: Compressing a signal in time stretches the transform in frequency$$\mathscr{F}[x(at)] = \frac{1}{|a|} X \left(\frac{\omega}{a}\right)\quad \text{if} \space a \neq0$$**Time Differentiation**: The Fourier transform of a differentiated function over time is the same as the Fourier transform times $j \omega$ $$\mathscr{F}\left[\frac{dx}{dt}\right]= j \omega X(\omega)$$**Frequency Differentiation**: The Fourier transform of a differentiated function times time is the same as the differentiated Fourier transform over angular frequency, times $j$ $$\mathscr{F}[ tx(t) ]= j \frac{dX}{d \omega}$$**Time Shifting**: Shifting a signal in time shifts the Fourier transform is multiplied by a complex exponential $e^{j \omega_{0} t}$ $$\mathscr{F}[x(t-t_{0})] = e^{-j \omega t_{0}} X( \omega)$$**Frequency Shifting**: Multiplying a signal by a complex exponential $e^{j \omega_{0} t}$ shifts the Fourier transform in frequency  $$\mathscr{F}[e^{j \omega_{0}t} x(t)] = X(\omega - \omega_{0})$$**Time Integration**: $$\mathscr{F}\left[\int^{t}_{- \infty} x(\tau) \space d\tau\right]= \frac{X(\omega)}{j \omega} + c \delta (\omega) \qquad \text{where} \space \int^{\infty}_{- \infty} (x(t) - c) \space dt = 0$$**Duality**:
$$\mathscr{F}[X(t)] = 2\pi x (- \omega)$$**Time Reversal**:$$\mathscr{F}[x(-t)] = X(- \omega)$$**[[Parseval's Theorem]]**: Shows the total signal energy can be calculated whether the signal is viewed in the time or frequency domains$$E_\text{total} = \int^{\infty}_{-\infty} |x(t)|^{2} \space dt = \int^{\infty}_{-\infty} |X(\omega)|^{2} \space d \omega$$
### The Fourier Transform of Specific Signals
#### The unit impulse (Dirac delta function)
Identical to the Laplace result:$$\mathscr{F}[\delta(t)] = 1$$
#### Unit step (Heavyside step function)
Odd case since it doesn't satisfy the $\Vert u(t) \Vert_{1} = \int^{\infty}_{- \infty} \vert u(t) \vert \space dt < \infty$ requirement, however since we can obtain the function from the unit impulse by integrate it, we get the: $$\mathscr{F}[u(t)] = \frac{1}{j \omega} + \frac{1}{2} \delta(\omega)$$which is similar to the Laplace result of $L[u(t)] = \frac{1}{s}$. However there's an added term of half of a unit impulse, which represents the average value of 0.5 when averaged over the minus infinity to infinity range.
#### Constant Function
Defined as $x(t)=1$, we can construct it as the sum of a step function, and its reversed version, so $$\mathscr{F}[u(t)+u(-t)]= \delta(\omega)$$This satisfies the duality principle, as the Fourier transform of a constant in the time domain is an impulse in the frequency domain.
#### Rectangular Pulse
The rectangular pulse $\text{rect}(\frac{t-T}{\tau})$ is a function with unit height, width $\tau$ and is centred around the point $t=T$, where $$
\text{rect}(\frac{t}{\tau}) 
\begin{cases}  
1 & \text{if} -\frac{-\tau}{2}<t< \frac{\tau}{2} \\ \\
0 & \text{otherwise}
\end{cases}
$$Finding the [[Fourier transform]] can be found using the definition, or by building the pulse as the difference between two shifted unit steps.

> [!NOTE]
> The function $\text{rect}\left(\frac{t}{\tau}\right)$ is a model for a perfect low-pass filter, so $\text{sinc}(x) = \frac{\sin x}{x}$ arises a lot in signal processing.  
> ```functionplot
> ---
> title: sinc(x)
> xLabel: x
> yLabel: y
> bounds: [-20,20,-0.4,1.2]
> disableZoom: true
> grid: false
> ---
> y = sin(x)/x
> ```
> 
#### Complex Exponential
Since $\mathscr{F}[1] = \delta(\omega)$ the frequency shifting theorem gets us:$$\mathscr{F}[\exp(j \omega_{0}t)] = \delta(\omega - \omega_0)$$
#### Cosine and Sine
Using the complex exponential forms of both:$$
\begin{align}
\mathscr{F}[\cos(\omega_{0}t)] & = \frac{1}{2}(\delta(\omega-\omega_{0}) + \delta(\omega+\omega_{0})) \\
\mathscr{F}[\sin(\omega_{0}t)] & = \frac{1}{2j}(\delta(\omega-\omega_{0}) - \delta(\omega+\omega_{0}))
\end{align}
$$
#### Sinusoidal Modulation
If a signal $x(t)$ is modulated (multiplied by) a cosine signal, its Fourier transform will be $$\mathscr{F}[x(t)\cos(\omega_{0}t)] = \frac{1}{2}(X(\omega - \omega_{0}) + X(\omega+\omega_{0}))$$We can see frequency shifting in the equation. This is seen in practise with *amplitude modulated* (AM) signals, where a high frequency sinusoidal *carrier wave* is modulated by a lower-frequency information signal which is to be transmitted.
![[Fourier Transforms am signals.png]]
## The Fourier Spectrum
Fourier methods decompose a function of time into its constituent frequencies, switching our view from the time domain to the frequency domain, and vice versa. 
- For the Fourier series of a periodic spectrum, the frequencies form a discrete line spectrum, with the separation between the frequencies being $\omega_{0} = \frac{2\pi}{T}$. When the period increases, the spectral lines move closer
- For the Fourier transform of an aperiodic signal, the period has effectively become infinite, and the spectral lines merge into a continuous spectrum.$$X(\omega) = \int^{\infty}_{- \infty} x(t) \exp(-j \omega t) \space dt$$This defines the **complex Fourier spectrum**. Similar to polar coordinates, we can get the same information using the (real) magnitude and phase spectra, defined by
- magnitude spectrum: $|X(\omega)| = \text{abs}(X(\omega))$
- phase spectrum: $\arg(X(\omega))$

The amplitude spectrum gives a direct measure of the relative amounts of different frequencies with a signal, and is often plotted on a logarithmic scale: 

![[Fourier Transforms amplitude spectrum.png]]
![[Fourier Transforms amplitude spectra 2.png]]

We can visualise information that might be unclear in the time-domain signal, but they also provide the basis for signal processing, like filtering, equalisation and noise reduction. 

As with any periodic function, [[Parseval's theorem]] calculates the total energy of the signal in either the time or frequency domain. The expression $|X(\omega)|^{2}$ describes the energy per unit (angular) frequency contained in the signal as a function of $\omega0, known as the *energy spectral density* of the aperiodic signal $x(t)$. $$S_{xx}(\omega) = |X(\omega)|^{2}$$*Power spectral density* is used more often, as it represents the energy spectral density per unit time, and therefore can be used to power signals that exist over all time. 
## Convolution
The [[convolution]] integral in the time domain is given by:$$
y(t) = x*h = (x*h)(t) = \int^{\infty}_{- \infty} x(\tau)h(t- \tau) \space d \tau
$$and the convolution property of the Fourier transform is that the output of a signal $x(t)$ passing through a filter with an impulse response $h(t)$ can be represented by the product of two [[Fourier transform|Fourier transforms]] in the [[frequency domain]]$$\mathscr{F}[x(t)*h(t)] = \mathscr{F}\left[\int^{\infty}_{- \infty} x(\tau)h(t- \tau) \space d \tau\right]= X(\omega)H(\omega)$$We can visualise this in two ways in the [[time domain]]:
![[Fourier Transforms convolution visualisation.png]]