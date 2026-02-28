**Subject**: #task/uni 
**Tags**: #uni/fourier 

---
## Definition
Used on periodic signals $x(t)$, where:
- $x(t)$ must be a single valued function
- $x(t)$ must have only a finite number of maxima and minima
- $x(t)$ must be absolutely integratable over one period (which means the integral is less than infinity)
Which can be represented as an infinite sum of sin and cosine waves.

**Fourier Series**
$$
\begin{align}
x(t) &= a_{0} + \sum^{n=\infty}_{n=1} (a_{n} \cos(2\pi nt) + b_{n}\sin (2\pi nt)) \\
&= a_{0} + \sum^{n=\infty}_{n=1} A_{n} \sin(n \omega_{0}t + \phi_{n}) \\
&= \sum^{n=\infty}_{n=- \infty} c_{n} e^{jn \omega_{0}t}
\end{align}
$$
**Fourier Coefficients:**
$$
\begin{align}
a_{0} &= \frac{1}{T} \int_{\langle T \rangle} x(t) \space dt \\
a_{n} &= \frac{2}{T} \int_{\langle T \rangle} x(t) \cos(n \omega_{0}t) \space dt \\
b_{n} &= \frac{2}{T} \int_{\langle T \rangle} x(t) \sin(n \omega_{0}t) \space dt
\end{align}
$$
## Examples
