**Subject**: 
**Tags**:

---
## Definition

Used on aperiodic signals $x(t)$, where:

- $x(t)$ must be a single valued function
- $x(t)$ must have only a finite number of maxima and minima in any finite interval
- $x(t)$ must be absolutely integrable over the entire timeline (which means the integral is less than infinity)
Which can be represented as a continuous sum (integral) of sine and cosine waves.
### Inverse Fourier Transform

$$
x(t) = \frac{1}{2\pi} \int_{-\infty}^{\infty} X(\omega) e^{j\omega t} \, d\omega
$$
### Fourier Transform

$$
X(\omega) = \int_{-\infty}^{\infty} x(t) e^{-j\omega t} \, dt
$$
