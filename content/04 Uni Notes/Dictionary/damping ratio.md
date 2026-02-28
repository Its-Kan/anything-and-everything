[Location:: #dictionary/uni]
[Subject:: #uni/maths]
[Tags:: #uni/control]

---
## Definition
$\zeta$ is the damping ratio, and is a measure of **energy dissipation in the system**.
- Higher $\zeta$ means a slower system, but less oscillation
- Lower $\zeta$ speeds up response time, but adds "ringing"

$\omega_{d} = \omega_{n}\sqrt{1-\zeta^{2}}$ is real only when $\zeta < 1$. 
- When $0 < \zeta < 1$, the system is **underdamped**. The poles are complex, and there will be overshoot.
- When $\zeta > 1$, the system is **overdamped**. The poles are real and distinct. Practically two [[System Properties - First Order|single order systems]].  
- When $\zeta = 1$, the system is **critically damped**. $\omega_{d}= 0$, and the poles are real and identical. 
