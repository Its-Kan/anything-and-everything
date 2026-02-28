 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-07-10]
## So you want to...

> [!uninotes]- Calculating Steady-State Output (DC Gain) for First-Order Systems 
> To calculate the steady-state output or **DC gain** for a stable first-order system $G(s)$ subjected to a unit step input $U(s) = 1/s$:
> 
> - **Recall the Final Value Theorem**: For a function $f(t)$ whose Laplace transform is $F(s)$, if $\lim_{t\to\infty} f(t)$ exists, then $f(\infty) = \lim_{s\to0} sF(s)$.
> - **Apply the theorem to the output**: The output in the Laplace domain is $Y(s) = G(s)U(s)$.
> - **Substitute the unit step input**: For $U(s) = 1/s$, the steady-state output is $y(\infty) = \lim_{s\to0} sY(s) = \lim_{s\to0} sG(s)(1/s)$.
> - **Simplify to find the DC gain**: This simplifies to $y(\infty) = \lim_{s\to0} G(s)$. This limit is known as the **DC gain ($K_{dc}$)** of the system.
> - **Example**: For $G(s) = A/(s+a)$, the DC gain is $A/a$.

> [!uninotes]- Determining First-Order System Step Response Characteristics 
> To characterize the time-domain behavior of a first-order system from its transfer function $G(s) = A/(s+a)$:
> 
> - **DC Gain ($K_{dc}$)**: This is the steady-state value of the output for a unit step input. Calculate it as $K_{dc} = \lim_{s\to0} G(s) = A/a$.
> - **Time Constant ($\tau$)**: The time constant dictates the speed of the exponential response. It is given by $\tau = 1/a$. A larger 'a' (pole further left in the s-plane) means a faster response (smaller $\tau$). The transfer function can be rewritten as $G(s) = K_{dc} / (1 + s\tau)$.
> - **Settling Time ($T_s$)**: The time it takes for the output to settle within 2% of its final value. For a first-order system, $T_s \approx 4\tau = 4/a$.
> - **Rise Time ($T_r$)**: The time it takes for the output to rise from 10% to 90% of its final value. For a first-order system, $T_r \approx 2.2\tau = 2.2/a$.
> - **Time-Domain Response**: The unit step response of a first-order system is $y(t) = K_{dc}(1 - e^{-t/\tau})$.

> [!uninotes]- Identifying Parameters and Pole Locations for a Second-Order System 
> To extract key characteristics from a second-order system's transfer function:
> 
> - **Standard Form**: Ensure the transfer function is in the standard second-order form: $G(s) = K_{dc}\omega_n^2 / (s^2 + 2\zeta\omega_n s + \omega_n^2)$.
> - **Identify Parameters**:
>     - **Undamped Natural Frequency ($\omega_n$)**: This is the natural oscillation frequency if there were no damping. It is the square root of the constant term in the denominator (assuming the $s^2$ coefficient is 1).
>     - **Damping Ratio ($\zeta$)**: This dimensionless parameter controls the decay rate of oscillations. It is found from the coefficient of the 's' term in the denominator: $2\zeta\omega_n = \text{coefficient of } s$, so $\zeta = (\text{coefficient of } s) / (2\omega_n)$.
>     - **Damped Natural Frequency ($\omega_d$)**: This is the actual oscillation frequency in the time domain for underdamped systems. It's calculated as $\omega_d = \omega_n\sqrt{1-\zeta^2}$.
> - **Determine Pole Locations**: The poles of a second-order system are given by the quadratic formula applied to the denominator: $s = -\zeta\omega_n \pm j\omega_n\sqrt{1-\zeta^2}$.
> - **Characterize Damping**:
>     - If $\mathbf{0 < \zeta < 1}$: The system is **underdamped** (complex poles, oscillations with overshoot).
>     - If $\mathbf{\zeta > 1}$: The system is **overdamped** (real and distinct poles, no oscillation).
>     - If $\mathbf{\zeta = 1}$: The system is **critically damped** (real and identical poles, fastest response without overshoot).

> [!uninotes]- Calculating Steady-State Error and Error Constants 
> To determine the steady-state error of a closed-loop system for different types of inputs:
> 
> - **Error Signal Formula**: The error signal in the Laplace domain is $E(s) = V(s) / (1 + G(s)H(s))$, where $V(s)$ is the input and $G(s)H(s)$ is the open-loop transfer function.
> - **Steady-State Error using Final Value Theorem**: The steady-state error $e(\infty)$ is found by $e(\infty) = \lim_{s\to0} sE(s)$.
> - **Error Constants**: These constants characterize the open-loop system's ability to reduce steady-state error:
>     - **Position Error Constant ($K_p$)**: $K_p = \lim_{s\to0} G(s)H(s)$.
>     - **Velocity Error Constant ($K_v$)**: $K_v = \lim_{s\to0} sG(s)H(s)$.
>     - **Acceleration Error Constant ($K_a$)**: $K_a = \lim_{s\to0} s^2G(s)H(s)$.
> - **Steady-State Errors for Specific Inputs**:
>     - For a **step input** ($V(s) = 1/s$): $e(\infty)_{step} = 1 / (1 + K_p)$.
>     - For a **ramp input** ($V(s) = 1/s^2$): $e(\infty)_{ramp} = 1 / K_v$.
>     - For a **parabolic input** ($V(s) = 1/s^3$): $e(\infty)_{parabola} = 1 / K_a$.

> [!uninotes]- Determining System Type and Its Impact on Steady-State Error 
> To understand how "system type" predicts closed-loop steady-state error:
> 
> - **Definition of System Type**: The system type refers to the **number of pure integrators (poles at the origin, $s=0$)** in the open-loop transfer function $G(s)H(s)$. If $G(s)H(s) = K_g \frac{\dots}{s^m\dots}$, then 'm' is the system type.
> - **Relationship to Error Constants and Steady-State Error**:
>     - **Type 0 (m=0)**: Has a finite $K_p = K_g$, resulting in a finite steady-state error for a step input ($e(\infty)_{step} = 1/(1+K_g)$). For ramp and parabolic inputs, $K_v=0$ and $K_a=0$, leading to infinite errors.
>     - **Type 1 (m=1)**: Has infinite $K_p$, resulting in **zero steady-state error for a step input** ($e(\infty)_{step} = 0$). Has a finite $K_v = K_g$, resulting in a finite steady-state error for a ramp input ($e(\infty)_{ramp} = 1/K_g$). For parabolic inputs, $K_a=0$, leading to infinite error.
>     - **Type 2 (m=2)**: Has infinite $K_p$ and $K_v$, resulting in **zero steady-state error for step and ramp inputs**. Has a finite $K_a = K_g$, resulting in a finite steady-state error for a parabolic input ($e(\infty)_{parabola} = 1/K_g$).
> - **General Rule**: For a Type $N$ system, the steady-state error is zero for inputs of order up to $N-1$ (e.g., step for Type 1, ramp for Type 2).

> [!uninotes]- Constructing a Bode Plot (Magnitude) 
> To sketch the magnitude portion of a Bode plot for a system's frequency response:
> 
> - **Purpose**: Bode plots are useful for analyzing system behavior in response to continuous inputs like noise.
> - **Preparation**:
>     1. **Convert Gain Constant to dB**: Express the overall gain constant ($K_g$ or other DC gain) of the transfer function in decibels (dB) using $20 \log_{10}(Gain)$.
>     2. **Identify Pole/Zero Frequencies**: Determine the corner frequencies (in rad/s) for all poles and zeros. For first-order terms $(1+sT)$, the corner frequency is $1/T$. For second-order terms $(s^2 + 2\zeta\omega_n s + \omega_n^2)$, use $\omega_n$.
> - **Starting the Plot (Low Frequency)**:
>     1. **Determine Low-Frequency Gradient**: This is based on the **system type** (number of integrators/poles at the origin). Each integrator contributes a -20 dB/decade slope. (e.g., Type 0: 0 dB/decade; Type 1: -20 dB/decade).
>     2. **Adjust Vertical Position**: The starting line should pass through the calculated gain constant (in dB) at a frequency of 1 rad/s.
> - **Iterate through Corner Frequencies**:
>     1. **For each pole/zero in ascending order of frequency**: Mark the corner frequency on your plot.
>     2. **Calculate Gain at Corner**: If your previous point was $(\omega_{last}, A_{last})$ and the current slope is $m$, the gain at the new corner frequency $\omega_{pz}$ is $A_{pz} = A_{last} + m \times \log_{10}(\omega_{pz}/\omega_{last})$.
>     3. **Update Slope**:
>         - **Poles**: Decrease the slope by **-20 dB/decade** for each real pole. For a second-order pole pair, the slope changes by -40 dB/decade.
>         - **Zeros**: Increase the slope by **+20 dB/decade** for each real zero. For a second-order zero pair, the slope changes by +40 dB/decade.
>     4. **Connect Points**: Draw straight lines between consecutive corner points with the updated slopes.

> [!uninotes]- Calculating Root Locus Asymptote Parameters 
> When sketching a Root Locus diagram, especially if there are more open-loop poles than zeros, determine the behavior of the loci as gain approaches infinity:
> 
> - **Asymptotes (Rule 3)**: If the number of open-loop poles ($n$) is greater than the number of open-loop zeros ($m$), the remaining $n-m$ loci branches will tend towards asymptotes.
> - **Angles of Asymptotes (Rule 4)**: The angles $\theta_A$ of these asymptotes are given by: $\theta_A = (2n'+1) \cdot 180^\circ / (\text{excess of poles})$, where $n' \in \mathbb{Z}$. The "excess of poles" is simply $n-m$. _Example_: If there are 2 more poles than zeros, the angles are $(2n'+1) \cdot 180^\circ / 2 = \pm 90^\circ$ (for $n'=0, 1$).
> - **Centre of Gravity (Rule 5)**: All asymptotes meet at a single point on the real axis called the centre of gravity ($s_{cg}$), calculated as: $s_{cg} = (\sum \text{poles} - \sum \text{zeros}) / (\text{excess of poles})$. This is the sum of the real parts of all open-loop poles minus the sum of the real parts of all open-loop zeros, divided by the excess of poles.

> [!uninotes]- Calculating Angles of Departure/Arrival for Complex Poles/Zeros 
> To accurately sketch the root locus when complex open-loop poles or zeros are present:
> 
> - **Angles of Departure (Rule 9)**: If there are complex open-loop poles, the locus branches start from these points. The angle $\theta_{p1}$ at which a locus leaves a complex starting point $p_1$ is given by: $\theta_{p1} = \sum \theta_{zi} - \sum_{i=2} \theta_{pi} \pm 180^\circ$.
>     - $\sum \theta_{zi}$ is the sum of angles from all open-loop zeros to the pole $p_1$.
>     - $\sum_{i=2} \theta_{pi}$ is the sum of angles from all _other_ open-loop poles to the pole $p_1$.
>     - All angles are measured counter-clockwise from the positive real axis to the vector pointing from the pole/zero to $p_1$.
> - **Angles of Arrival (Rule 10)**: If there are complex open-loop zeros, the locus branches end at these points. The angle $\theta_{z1}$ at which a locus arrives at a complex ending point $z_1$ is given by: $\theta_{z1} = \sum \theta_{pi} - \sum_{i=2} \theta_{zi} \pm 180^\circ$.
>     - $\sum \theta_{pi}$ is the sum of angles from all open-loop poles to the zero $z_1$.
>     - $\sum_{i=2} \theta_{zi}$ is the sum of angles from all _other_ open-loop zeros to the zero $z_1$.
>     - Again, all angles are measured counter-clockwise from the positive real axis to the vector pointing from the pole/zero to $z_1$.

> [!uninotes]- Determining Controller Gain for Desired Closed-Loop Pole Location 
> Once a desired closed-loop pole location is identified on the root locus:
> 
> - **Gain Criterion (Rule 12)**: The magnitude of the open-loop transfer function at any point on the root locus must be equal to 1, i.e., $|K G(s)H(s)| = 1$. This allows calculating the required gain $K$.
> - **Monic Form Gain ($K_m$)**: The rule for calculating gain at a point 's' on the root locus is: $K_m = (\prod \text{finite pole lengths}) / (\prod \text{finite zero lengths})$.
>     - Measure the distance (length) from the desired closed-loop pole location to each finite open-loop pole and each finite open-loop zero.
>     - Multiply all the pole lengths together.
>     - Multiply all the zero lengths together.
>     - Divide the product of pole lengths by the product of zero lengths.
> - **Adjust for Existing Monic Gain**: If the plant $G(s)$ already has a monic form gain (a constant multiplier in front of the normalized transfer function), divide the calculated $K_m$ by this existing gain to find the actual controller gain $K$.
> - **Iterative Design**: This process is often part of an iterative design, where the desired pole location might be adjusted based on the resulting controller gain and performance.

> [!uninotes]- Implementing Digital PID Controller Algorithm 
> To implement a continuous PID control law $c(t) = K_p e(t) + K_i \int e(\tau)d\tau + K_d \frac{de(t)}{dt}$ digitally:
> 
> - **Sampling**: The error signal $e(t)$ is sampled at discrete time intervals $T$ (sample period), denoted as $e_n = e(nT)$.
> - **Approximate Derivative Term**: The derivative $de(t)/dt$ at time $nT$ can be approximated using the **backwards difference method**: $d_n = \frac{1}{T}(e_n - e_{n-1})$.
> - **Approximate Integral Term**: The integral $\int e(\tau)d\tau$ at time $nT$ can be approximated iteratively:
>     - **Rectangular (Euler)**: $i_n = i_{n-1} + e_n T$ (simple, 0th-order).
>     - **Trapezoidal**: $i_n = i_{n-1} + \frac{T}{2}(e_n + e_{n-1})$ (more accurate, 1st-order).
> - **Digital PID Algorithm (Iterative Steps)**:
>     1. **Initialization**: Set previous error ($e_{n-1}$) and previous integral ($i_{n-1}$) to zero before the first sample.
>     2. **Every Sample Period**:
>         - **Read Current Error**: Obtain $e_n$ (the current sampled error).
>         - **Compute Derivative Term**: Calculate $d_n$ using the chosen approximation.
>         - **Update Integral Term**: Calculate $i_n$ using the chosen approximation.
>         - **Calculate Controller Output**: Compute the current control output $c_n = K_p e_n + K_i i_n + K_d d_n$.
>         - **Store Previous Values**: Set $e_{n-1} = e_n$ and $i_{n-1} = i_n$ for the next iteration.
> - **Sample Rate Considerations**:
>     - **High Rate Advantages**: More accurate approximations and reduced control loop delays (improves phase margin).
>     - **High Rate Drawbacks**: Increased computational effort, greater numerical precision problems, and amplified noise susceptibility in derivative calculations due to $1/T$ term.
## Study Guide
### Topics
#### I. Introduction to Control, Sensors, and Instrumentation

1.  **Defining Control and Instrumentation:**
    * **Control**: The process of regulating or directing a system's behaviour. In this context, "feedback control" or "closed-loop control" is emphasized, involving sensing, comparing, and reacting to reduce error.
    * **Instrumentation**: The tools and techniques used for measurement, observation, and control of physical quantities. It is the foundation for obtaining the data needed for control systems.
2.  **Flipped Classroom Model:**
    * **Concept**: Reverses traditional teaching; delivery of concepts via pre-recorded videos (watched independently), while contact hours are dedicated to workshops for practice, consolidation, and Q&A.
    * **Benefits**: Overall better results (fewer failures, higher mean marks, positive feedback).
    * **Challenges**: Requires students to be proactive in watching videos, attending workshops, attempting question sheets, and communicating early if falling behind.
3.  **The Laplace Transform - Core Concepts and Applications:**
    * **Purpose**: A mathematical tool used in control engineering to convert linear differential equations into algebraic polynomials, simplifying analysis. It also replaces convolution integrals with multiplication.
    * **Time Domain vs. Laplace Domain**: Understanding the correspondence between time-domain functions (input $u(t)$, output $y(t)$, impulse response $g(t)$) and their Laplace domain counterparts ($U(s)$, $Y(s)$, $G(s)$).
    * **Transfer Functions**: Represent the input-output relationship of a system ($Y(s) = G(s)U(s)$).
    * **Practical Application**: Calculating step responses and steady-state values (DC gain) using partial fraction expansion and the Final Value Theorem.
        * **Final Value Theorem**: $f(\infty) = \lim_{s\to0} sF(s)$. For a unit step input $U(s) = 1/s$, the steady-state output is $y(\infty) = \lim_{s\to0} G(s)$.
4.  **Unity Negative Feedback:**
    * **Structure**: A fundamental control loop where the output is fed back and subtracted from the desired input (set point) to generate an error signal.
    * **Components**: Plant $G(s)$ (the system to be controlled), Controller $H(s)$, Input $V(s)$ (set point), Output $Y(s)$, Error Signal $E(s)$.
    * **Closed-Loop Transfer Function $T(s)$**: $T(s) = Y(s)/V(s) = G(s)H(s) / (1 + G(s)H(s))$. This is the primary equation for analysing the system's behaviour.

#### II. Modelling Control Systems

1.  **Origin of Transfer Functions:**
    * Transfer functions are derived from the mathematical models of dynamic systems (e.g., electrical networks, mechanical systems).
    * Focus on **linear systems** due to the applicability of the Laplace transform (superposition and homogeneity).
2.  **Modelling Mechanical Systems (Translational and Rotational):**
    * **Impedance Concept**: The ratio of force $F(s)$ to displacement $X(s)$ in the Laplace domain, analogous to electrical impedance.
    * **Components and their Impedances**:
        * **Mass (M)**: $Ms^2$ (from Newton's Second Law: $f(t) = M\ddot{x}(t)$)
        * **Spring (K)**: $K$ (from Hooke's Law: $f(t) = Kx(t)$)
        * **Damper (B)**: $Bs$ (from viscous friction: $f(t) = B\dot{x}(t)$)
    * **Modelling Procedure**: Use free-body diagrams to sum forces to zero on each mass, resulting in simultaneous differential equations, which are then Laplace transformed.
    * **Rotational Systems**: Analogous to translational systems.
        * Force becomes Torque ($T$).
        * Displacement becomes Angle ($\theta$).
        * Velocity becomes Angular Velocity ($\omega$).
        * Mass becomes Inertia ($J$).
        * Impedances: $Js^2$ (Inertia), $K$ (Torsion Spring), $Bs$ (Viscous Damper).
3.  **Gearboxes in Rotational Systems:**
    * **Assumptions**: Linear effects only, no inertial mass, friction, or elasticity within the gearbox itself.
    * **Gear Ratio**: Number of rotations of input per rotation of output (e.g., 6:1).
    * **Transformation Rules**:
        * Angle (and speed, acceleration) is divided by the gear ratio.
        * Torque is multiplied by the gear ratio.
        * Impedance is divided by the **square** of the gear ratio when moving components to one side of the gearbox.

#### III. Sensing and Measuring

1.  **Purpose of Sensing/Measuring**: Monitoring, alerting, quality management, and crucial for feedback control systems.
2.  **Energy Transfer and Observer Effect**: Sensors always transfer energy from the system under observation, which inherently affects the system ("observer effect").
3.  **Sensor Classifications:**
    * **Passive vs. Active**:
        * **Passive**: Takes energy from the system (e.g., microphones, optical sensors, deflection transducers).
        * **Active**: Adds energy to the system and measures the response (e.g., radar, ultrasound, null transducers like load cells with actuators).
    * **Absolute vs. Relative**: All measurements are fundamentally relative to a datum. Some sensors explicitly measure relative quantities (e.g., thermocouples).
4.  **Reading Sensor Outputs**: Most sensors convert physical quantities into electrical signals (voltage or frequency) for processing (amplification, A/D conversion).
5.  **Measurement Limitations and Errors:**
    * **Sources of Error**: Transducer properties, physical principles, temperature stability, linearity limits, signal processing, conversion inaccuracies.
    * **Accuracy vs. Precision**:
        * **Accuracy**: Closeness of the mean measurement to the true value.
        * **Precision (Repeatability)**: Spread or variability of measurements.
    * **Sensitivity**: Smallest change in input that causes a response.
    * **Dynamic Range**: Ratio of largest to smallest measurable response.
    * **Resolution/Quantisation**: Error introduced by discrete numerical representation; affects accuracy and relates to dynamic range.
    * **Noise**: Random fluctuations affecting precision, but not accuracy. Often modelled as additive Gaussian noise. Lower bandwidth sensors can be less noisy due to filtering.
    * **Nonlinearity**:
        * **Hard Nonlinearities**: Sudden changes (e.g., limits).
        * **Soft Nonlinearities**: Non-straight line input-output relationships (e.g., hysteresis – dependence on history, causing lag).
        * **Delays**: Time between event and sensor response; can affect control stability.

#### IV. Movement and Deflection Sensors

1.  **Position Sensing Categories**: Binary/continuous, absolute/incremental, mechanical/contactless.
2.  **Proximity Switches**: Binary sensors; mechanical microswitches (snap action, hysteresis, repeatable) or contactless (inductive, capacitive, Hall effect).
    * **Inductive**: Senses metallic objects via magnetic field changes; reliable in harsh conditions.
    * **Capacitive**: Senses conductive objects via capacitance changes; smaller range, susceptible to parasitic coupling.
    * **Hall Effect**: Senses magnetic fields or ferromagnetic material; deflects charge carriers, generating voltage. Used for contactless switching, speed sensing.
3.  **Time-of-Flight (ToF) Sensors**: Active, contactless, measures distance by round-trip time of sound (ultrasonic) or light.
    * **Ultrasonic**: Cheap, limited range (~5m), poor accuracy/precision.
    * **Optical**: Uses indirect measurement (e.g., two pixels detecting light pulse arrival) due to light speed. Affected by target reflectivity.
4.  **Encoders (Linear and Rotary)**: Scale and read head, provides position or angle.
    * **Incremental**: Resets on power cycle; uses quadrature encoding (digital or analogue sinusoidal patterns) for direction and higher accuracy.
        * Optical ("glass scales") vs. Magnetic.
    * **Absolute**: Every part of scale unique; maintains position on power loss. Gray code often used for multi-bit outputs to avoid large errors at boundaries.
        * Single-track Gray codes for compactness.
    * **Magnetic Angle Sensors**: Increasingly popular for absolute angle; use Hall effect with diametrically polarized magnets. Low cost, high resolution, but can be nonlinear and sensitive to magnet placement/external fields.
5.  **Potentiometers**: Simple, cheap, absolute angular position sensors; limited rotation, can be noisy, not always linear.
6.  **Measuring Weight and Force (Strain Gauges and Load Cells)**:
    * Mass cannot be directly measured, but weight (force) can be by measuring deflection.
    * **Strain Gauge**: Measures elongation (strain) of a material; resistance changes with length and cross-sectional area. Very small resistance changes require Wheatstone bridge.
    * **Wheatstone Bridge**: Circuit for measuring small resistance changes. Can be quarter-bridge (one strain gauge) or full-bridge (four strain gauges). Full bridge offers linear output and common-mode rejection (e.g., temperature changes).
    * **Load Cell**: Combines strain gauges with a "spring element" to measure applied force.

#### V. More About Sensors

1.  **3D Position**: External references (satellite navigation, fixed cameras) or dead reckoning.
    * **Satellite Navigation (GPS, GLONASS, BeiDou, Galileo)**: Uses satellite broadcast times for trilateration. Precision limited by local clock and atmospheric effects.
    * **Local Corrections (DGPS, RTK)**: Uses nearby fixed receivers to compensate for atmospheric effects, enabling centimeter accuracy.
    * **Indoor Positioning Systems**: For robotics, multiple fixed cameras with fiducial markers (or vice versa) for triangulation.
    * **Dead Reckoning**: Estimates position based on previous position, movement data (velocity, acceleration), and elapsed time.
        * **Inertial Navigation**: Uses IMUs (Inertial Measurement Units) for acceleration and angular rate.
2.  **Acceleration Sensors (Accelerometers)**:
    * Measures acceleration directly (no external reference needed).
    * **Moving Mass Accelerometer**: Deflection transducer; mass on a spring, displacement proportional to acceleration. MEMS versions common.
    * **Null Balance Accelerometer**: Null transducer; actuator maintains zero mass displacement, required force is output.
3.  **Gyroscopes**: Senses angular rate for attitude determination.
    * **Spinning Gyroscope**: Exhibits torque-induced precession.
    * **Vibrating Structure Gyroscopes (MEMS)**: Small, cheap, but limited accuracy/precision, susceptible to thermal drift and acceleration.
    * **Optical Gyroscopes (LRGs, FOGs)**: Uses Sagnac effect (differential path length of light in a rotating circle). Large, expensive, but very accurate and precise.
4.  **Sensor Fusion**: Combining data from multiple sensors (e.g., GPS + IMU) to improve accuracy and precision, leveraging their complementary strengths.
5.  **SLAM (Simultaneous Localisation And Mapping)**: Uses environmental features (mapped via dead reckoning) to improve localization accuracy and simultaneously refine the map. LIDAR is a common sensor for SLAM.
6.  **Pressure Sensors**: Measures force per unit area.
    * **Types**: Absolute, relative, gauge, vacuum.
    * **Technologies**: Strain gauges, capacitive sensing of diaphragms, piezoelectric materials, LVDT.
7.  **Temperature Sensors**:
    * **Thermocouples**: Measures differential temperature using the Seebeck effect (voltage across junction of dissimilar metals). Small voltage requires amplification. Thermopiles use multiple thermocouples in series.
    * **Thermistors**: Temperature-dependent resistors (PTC: resistance increases; NTC: resistance decreases). Good accuracy relies on manufacturing; low-cost devices have high variability.
8.  **Light Sensors**:
    * **Photodiode**: Semiconductor diode optimized for light sensitivity.
    * **Phototransistor**: More sensitive than photodiode, but less linear and slower.
    * **Light-Dependent Resistors (LDRs)**: Low cost, low accuracy, very slow.

#### VI. System Properties: First Order

1.  **First-Order Pole Transfer Function**: $G(s) = A/(s+a)$.
    * **DC Gain ($K_{dc}$)**: $\lim_{s\to0} G(s) = A/a$.
    * **Unit Step Response**: $y(t) = (A/a)(1 - e^{-at})$.
    * **Pole Location ($a$)**:
        * Large $a$: Pole far left in s-plane, fast exponential decay.
        * Small $a$: Pole near imaginary axis, slow exponential decay.
        * Negative $a$: Pole in right-half s-plane, increasing (unstable) exponential.
2.  **Time Constant ($\tau$)**: $\tau = 1/a$. Defines the speed of response.
    * Transfer function rewritten as $G(s) = K_{dc} / (1 + s\tau)$.
    * Step response: $y(t) = K_{dc}(1 - e^{-t/\tau})$.
3.  **Settling Time ($T_s$)**: Time for output to settle to within 2% of final value. For first-order systems, $T_s \approx 4\tau = 4/a$.
4.  **Rise Time ($T_r$)**: Time for output to rise from 10% to 90% of final value. For first-order systems, $T_r \approx 2.2\tau = 2.2/a$.
5.  **Modes and Residues**:
    * **Poles**: Define the exponential "modes" (time constants) in the system's time-domain response.
    * **Zeros**: Affect the "residues" (weights or amplitudes) of these modes. Zeros can significantly impact time responses, even though they don't affect stability directly.

#### VII. System Properties: Second Order (I & II)

1.  **Complex Poles and Oscillation**: Complex poles in the Laplace domain lead to oscillatory behavior in the time domain.
    * Example: Impulse response $\cos(\omega t)$ has poles at $s = \pm j\omega$.
2.  **Standard Form of a Second-Order System**: $G(s) = K_{dc}\omega_n^2 / (s^2 + 2\zeta\omega_n s + \omega_n^2)$.
    * **Damping Ratio ($\zeta$)**: Controls the decay rate of oscillations.
    * **Undamped Natural Frequency ($\omega_n$)**: Natural oscillation frequency if no damping.
    * **Poles**: $s = -\zeta\omega_n \pm j\omega_n\sqrt{1-\zeta^2}$.
    * **Damped Natural Frequency ($\omega_d$)**: $\omega_d = \omega_n\sqrt{1-\zeta^2}$.
3.  **Damping Ratio and System Behaviour**:
    * $0 < \zeta < 1$: Underdamped. Complex poles, oscillations with overshoot.
    * $\zeta > 1$: Overdamped. Real and distinct poles, no oscillation, slower response.
    * $\zeta = 1$: Critically Damped. Real and identical poles, fastest response without overshoot.
4.  **Second-Order System Step Response**: $y(t) = 1 - e^{-\zeta\omega_n t} / \sqrt{1-\zeta^2} \sin(\omega_d t + \phi)$.
5.  **Time-Domain Specifications for Second-Order Systems**:
    * **Rise Time ($T_r$)**: Time from 0% to 100% of final value (approx. $T_r = (\pi - \phi)/\omega_d$ for underdamped). Tables are often used.
    * **Settling Time ($T_s$)**: Time for output to reach and stay within $\pm 2$ of final value. $T_s \approx 4/(\zeta\omega_n) = 4/\alpha$ (depends only on the real part of the pole).
    * **Percentage Overshoot (%OS)**: Maximum percentage the output exceeds the final value.
        * Time to Peak Overshoot ($T_p$): $T_p = \pi/\omega_d$.
        * $\%OS = 100e^{-\zeta\pi/\sqrt{1-\zeta^2}}$.
        * %OS depends **only** on the damping ratio $\zeta$.
6.  **Building Blocks of High-Order Systems**: Any polynomial with real coefficients can be factored into first- and second-order components.
7.  **Temporal Dominance**: Poles closer to the origin (slower poles) dominate the time response of cascaded systems. Zeros also exhibit dominance; a zero near a slow pole can reduce its residue, making it less dominant.
#### VIII. Control Loops and Steady-State Error
1.  **Analytic Control (Simple Gain)**:
    * For simple plants $G(s)$ and controller $H(s) = K$, the closed-loop transfer function is $T(s) = KG(s) / (1 + KG(s))$.
    * Increasing gain $K$ can change system behaviour (e.g., from overdamped to underdamped), but finding precise roots for arbitrary $K$ is complex.
2.  **Steady-State Error ($e(\infty)$)**: The difference between the desired output and the actual output as time approaches infinity.
    * **Error Signal**: $E(s) = V(s) / (1 + G(s)H(s))$.
    * **Final Value Theorem Application**: $e(\infty) = \lim_{s\to0} sE(s) = \lim_{s\to0} sV(s) / (1 + G(s)H(s))$.
3.  **Error Constants (for Open-Loop System $G(s)H(s)$)**:
    * **Position Error Constant ($K_p$)**: $K_p = \lim_{s\to0} G(s)H(s)$.
        * Steady-state error for **step input**: $e(\infty)_{step} = 1 / (1 + K_p)$.
    * **Velocity Error Constant ($K_v$)**: $K_v = \lim_{s\to0} sG(s)H(s)$.
        * Steady-state error for **ramp input**: $e(\infty)_{ramp} = 1 / K_v$.
    * **Acceleration Error Constant ($K_a$)**: $K_a = \lim_{s\to0} s^2G(s)H(s)$.
        * Steady-state error for **parabolic input**: $e(\infty)_{parabola} = 1 / K_a$.

#### IX. Steady-State Error and System Type

1.  **System Type**: The number of pure integrators (poles at the origin, $s=0$) in the open-loop transfer function $G(s)H(s)$. Represented by $m$ in the general form: $G(s)H(s) = K_g \frac{(1+T_as)(1+T_bs)\cdots}{s^m(1+T_1s)(1+T_2s)\cdots}$.
    * $K_g$ is the gain constant.
2.  **Relationship between System Type and Steady-State Error**:
    * **Type 0 (m=0)**:
        * $K_p = K_g$, $e(\infty)_{step} = 1/(1+K_g)$.
        * $K_v = 0$, $e(\infty)_{ramp} = \infty$.
        * $K_a = 0$, $e(\infty)_{parabola} = \infty$.
    * **Type 1 (m=1)**:
        * $K_p = \infty$, $e(\infty)_{step} = 0$.
        * $K_v = K_g$, $e(\infty)_{ramp} = 1/K_g$.
        * $K_a = 0$, $e(\infty)_{parabola} = \infty$.
    * **Type 2 (m=2)**:
        * $K_p = \infty$, $e(\infty)_{step} = 0$.
        * $K_v = \infty$, $e(\infty)_{ramp} = 0$.
        * $K_a = K_g$, $e(\infty)_{parabola} = 1/K_g$.
    * **Higher Types**: For Type $N$ systems, the steady-state error is zero for inputs of order up to $N-1$ (e.g., step for Type 1, ramp for Type 2).

#### X. Disturbance Rejection

1.  **Disturbance**: Uncommanded changes to a system's state (physical disturbance) or noise/imprecision (e.g., sensor noise). It is a primary reason for closed-loop control.
2.  **Output Disturbance**: Modelled as an additive signal $D(s)$ at the plant output.
    * Transfer function: $Y(s)/D(s) = 1 / (1 + G(s)H(s))$.
    * Poles of $Y(s)/D(s)$ are identical to the closed-loop system $T(s) = Y(s)/V(s)$. Thus, design criteria for settling time and overshoot also apply to disturbance rejection.
3.  **Sensor Noise**: Modelled as an additive signal $N(s)$ in the feedback loop.
    * Transfer function: $Y(s)/N(s) = -G(s)H(s) / (1 + G(s)H(s))$.
    * The noise transfer function is effectively the same as the closed-loop transfer function $T(s)$ (ignoring the negative sign).
4.  **Frequency Response and Bode Plots**:
    * **Purpose**: Useful for analyzing system behavior in response to continuous inputs like noise.
    * **Poles and Zeros Effects**:
        * **Poles**: Introduce a -20 dB/decade slope decrease above their corner frequency.
        * **Zeros**: Introduce a +20 dB/decade slope increase above their corner frequency.
        * **Integrators (pole at origin)**: -20 dB/decade slope.
        * **Differentiators (zero at origin)**: +20 dB/decade slope.
    * **Construction**: Convert gain constant to dB, identify pole/zero frequencies, plot low-frequency line based on system type and gain, then adjust slope at each corner frequency.
    * **Noise Shaping**: The amplitude spectrum of noise is shaped by the system's amplitude response. Gaussian noise has theoretically infinite bandwidth and constant power spectral density; its output spectrum matches the system's Bode amplitude plot.

#### XI. Design by Root Locus (I, II, III, IV)

1.  **Root Locus Concept**: A graphical method that plots the locations of the closed-loop poles of a system as a single gain parameter ($K$) is varied from 0 to infinity.
    * Closed-loop poles are the roots of $1 + K G(s)H(s) = 0$, or $K G(s)H(s) = -1$.
    * **Gain Criterion**: $|K G(s)H(s)| = 1$.
    * **Angle Criterion**: $\angle (K G(s)H(s)) = (2n+1)180^\circ$, where $n \in \mathbb{Z}$. This criterion determines the **shape** of the locus.
2.  **Rules for Sketching Root Locus (12 rules discussed across lectures)**:
    * **Symmetry (Rule 1)**: Symmetrical about the real axis.
    * **Start/End Points (Rule 2)**: Loci start at open-loop poles and end at open-loop zeros.
    * **Asymptotes (Rules 3, 4, 5)**: If number of poles > number of zeros, remaining loci tend towards asymptotes.
        * **Angles**: $\theta_A = (2n+1)180^\circ / (\text{excess of poles})$.
        * **Centre of Gravity (intersection point)**: $s_{cg} = (\sum \text{poles} - \sum \text{zeros}) / (\text{excess of poles})$.
    * **Real Axis Segments (Rule 6)**: A point $p$ on the real axis is part of the locus if the total number of open-loop poles and zeros to its right is odd.
    * **Break-away/Break-in Points (Rules 7, 8)**: Points where loci leave or arrive at the real axis at $90^\circ$. Found by solving $\sum_{i=1}^m \frac{1}{s-z_i} = \sum_{i=1}^n \frac{1}{s-p_i}$ or $dG(s)/ds = 0$.
    * **Angles of Departure (Rule 9)**: Angle at which a locus leaves a complex open-loop pole. $\theta_{p1} = \sum \theta_{zi} - \sum_{i=2} \theta_{pi} \pm 180^\circ$.
    * **Angles of Arrival (Rule 10)**: Angle at which a locus arrives at a complex open-loop zero. $\theta_{z1} = \sum \theta_{pi} - \sum_{i=2} \theta_{zi} \pm 180^\circ$.
    * **Imaginary Axis Crossings (Rule 11)**: Found by setting $s = j\omega$ in the characteristic equation $1+K G(s)H(s) = 0$ and using the Routh Array (Routh-Hurwitz Stability Criterion).
        * **Routh Array**: Determines absolute stability (no sign changes in first column means stable).
        * **Zero Row**: Indicates poles symmetrical about the origin (often on the imaginary axis). An auxiliary polynomial can be extracted and differentiated to find these points and the gain $K$ at which they occur.
    * **Gain Values (Rule 12)**: The overall monic form gain $K_m$ at any point on the root locus is $K_m = (\prod \text{finite pole lengths}) / (\prod \text{finite zero lengths})$. The actual controller gain $K$ must account for any existing monic form gain in $G(s)H(s)$.
3.  **Design Application**:
    * Allows selection of gain $K$ to place closed-loop poles at desired locations to meet performance specifications (e.g., damping ratio, settling time).
    * **Unmodelled Dynamics**: Simplified models are useful, but high gains can push poles far from open-loop positions, making unmodelled dynamics more significant. Dominance also applies to root locus shape.

#### XII. Reshaping the Root Locus: PD, PI, and PID Control

1.  **Need for Reshaping**: If desired closed-loop pole locations do not lie on the existing root locus, the locus must be reshaped by adding controller poles or zeros.
2.  **PD (Proportional-plus-Derivative) Control**: $H(s) = K_p + K_d s = K(s+z_{pd})$.
    * **Effect**: Adds a zero to the open-loop system, pulling the root locus to the left, which generally improves transient response (faster, more damping).
    * **Design Procedure (Iterative)**: 1. Plot open-loop poles and zeros. 2. Establish desired closed-loop pole positions (e.g., based on $T_s$, %OS). 3. Use angle criterion at desired pole to find the required angle contribution from the PD zero. 4. Determine PD zero position. 5. Use gain rule (Rule 12) to find controller gain. 6. Test closed-loop system behavior (step response) and refine.
    * **Problems**:
        * **Noise Amplification**: Differentiator term amplifies high-frequency noise.
        * **Set-point Kick**: Step changes in the set point lead to large, impulsive controller outputs.
3.  **PI (Proportional-plus-Integral) Control**: $H(s) = K_p + K_i/s = K(s+z_{pi})/s$.
    * **Effect**: Adds an integrator (pole at origin) to increase system type, reducing steady-state error to zero for step inputs (and finite for ramp for Type 1). Adds a zero very close to the origin to counteract the destabilizing effect of the integrator on the root locus and minimize impact on transient response.
    * **Design Procedure (Iterative)**: 1. Find simple gain for desired transient response (often from a previous PD design). 2. Add a pole at the origin (integrator). 3. Add a zero very close to the origin. 4. Test closed-loop system behavior. 5. If slow pole dominates, move the zero further left (away from origin) to reduce its residue. 6. Repeat until performance achieved.
    * **Trade-off**: Improves steady-state error but typically slows down the transient response (increases settling time, often reduces overshoot) due to the new slow pole near the origin.
4.  **PID (Proportional-Integral-Derivative) Control**: Combines benefits of PD and PI: $H(s) = K_p + K_i/s + K_d s$.
    * **Effect**: Adds an integrator and two zeros. One zero for transient shaping (like PD), and another near the origin for steady-state error reduction (like PI).
    * **Design Strategy**: Generally, design PD first for transient, then add PI for steady-state. 1. Design PD controller for desired transient performance (making it slightly more aggressive to account for PI effects). 2. Design PI controller (adding pole at origin and zero close by) to improve steady-state error while minimizing impact on transient. This step is iterative.
    * **Common Use**: Very widely used, even without detailed system analysis.

#### XIII. Phase-Advance Networks (PANs)

1.  **Implementation Problems with PD/PID**:
    * **Differentiators**: Non-existent in ideal form, amplify noise, require active components, cause impulses.
    * **Integrators**: Can lead to "integrator wind-up" if error persists (beyond scope).
2.  **Filtering the Differentiator**: To mitigate noise and set-point kick, a low-pass filter can be added, effectively placing a pole $p_f$ to the left of the PD zero $z_{pd}$ ($p_f > z_{pd}$).
3.  **Phase-Advance Network (PAN) / Phase-Lead Network**: $H(s) = K \frac{s+z_{pd}}{s+p_f}$.
    * **Advantages**: Reduced noise, more realistic implementation, can be passive (if $K < 1$).
    * **Disadvantages**: Does not reduce excess of poles, more complex design (two parameters to place), less "power" (angle contribution) than ideal PD, can worsen overshoot in some cases.
4.  **PAN Design Procedure**:
    1.  Arbitrarily choose compensator zero position (often under the desired pole).
    2.  Calculate compensator pole position to satisfy angle criterion at desired closed-loop pole.
    3.  Find gain using Rule 12.
    4.  Test closed-loop step response and refine pole/zero positions iteratively.
    5.  **Passive Implementation**: Shows an RC circuit realizing a PAN transfer function. Requires careful selection of component values and might need additional gain adjustment.

#### XIV. Digital Controller Implementation

1.  **Digital PID Control Law**: $c(t) = K_p e(t) + K_i \int e(\tau)d\tau + K_d \frac{de(t)}{dt}$.
    * **Sampling**: Error signal $e(t)$ is sampled at discrete intervals $T$. Notation $e_n$ for $e(nT)$.
2.  **Approximating Derivatives and Integrals**:
    * **Derivative (Backwards Difference)**: $d_n = \frac{1}{T}(e_n - e_{n-1})$. Simple, 1st-order approximation.
    * **Integral (Rectangular/Euler)**: $i_n = i_{n-1} + e_n T$. Simple, 0th-order.
    * **Integral (Trapezoidal)**: $i_n = i_{n-1} + \frac{T}{2}(e_n + e_{n-1})$. More accurate, 1st-order.
3.  **Digital PID Algorithm**: Iterative process involving reading error, computing derivative, updating integral, calculating output, and storing previous values.
4.  **Sample Rate ($T$)**:
    * **Advantages of High Rate**: More accurate approximations, reduced delays (improves phase margin).
    * **Disadvantages of High Rate**: Increased computational effort, greater numerical precision problems, increased noise susceptibility in derivative.
    * **Effect on Phase Margin**: Even with negligible processing delay, the system responds on average $T/2$ later, which can erode phase margin and reduce damping.
5.  **Converting Other Controllers to Digital Form**:
    * General procedure: Express controller as $C(s)/E(s)$, rearrange algebraically, substitute sampled signals and derivative approximations (e.g., $s \approx (z-1)/T_z$ for z-transform, or direct time-domain approximation), and derive recurrence relations.
    * Result is a recursive digital filter.

---

### Part 2: Quiz

Instructions: Answer each question in 2-3 sentences.

1.  Explain the primary advantage of using the Laplace transform in control engineering.
2.  What is the "observer effect" in sensing, and why is it always present?
3.  Distinguish between accuracy and precision in the context of sensor measurements.
4.  Describe how a strain gauge measures force, and what additional component is often used for precise measurement.
5.  In the context of system properties, what do "poles" and "zeros" primarily affect in the time-domain response?
6.  For a second-order underdamped system, what does the damping ratio ($\zeta$) specifically control regarding the time response?
7.  Define "system type" for an open-loop transfer function and explain its significance for steady-state error to a step input.
8.  How does a PD (Proportional-Derivative) controller reshape the root locus, and what is a common drawback of its ideal implementation?
9.  What is the main purpose of adding an integrator (pure pole at the origin) to a control system, and what is a key challenge this introduces?
10. Briefly explain how increasing the sample rate in a digital control system can improve performance, and one significant drawback.

---

### Part 3: Quiz Answer Key

1.  The primary advantage of using the **Laplace transform** in control engineering is its ability to convert linear differential equations into algebraic polynomials. This transformation greatly simplifies the analysis and design of control systems, as complex operations like convolution become simple multiplication.
2.  The "**observer effect**" in sensing refers to the phenomenon where the act of measuring a system inherently influences its state. This occurs because sensors must transfer some energy from the system under observation to generate a measurement, causing a perturbation.
3.  **Accuracy** in sensor measurements relates to how close the average of multiple measurements is to the true, "ground truth" value. **Precision**, on the other hand, refers to the spread or variability of those measurements around their mean, indicating the repeatability of the sensor.
4.  A **strain gauge** measures force indirectly by detecting the elongation (strain) of a material to which it is affixed; this elongation causes a change in the gauge's electrical resistance. For precise measurement of these small resistance changes, a **Wheatstone bridge** circuit is typically used.
5.  In the context of system properties, **poles** primarily define the exponential "modes" (or time constants) present in a system's time-domain response. **Zeros**, conversely, affect the "residues" or weights of these modes, thereby influencing the relative amplitude and shape of the response.
6.  For a second-order underdamped system, the **damping ratio ($\zeta$)** specifically controls the rate at which oscillations decay and the amount of overshoot. A higher damping ratio leads to faster decay and less overshoot, while a lower ratio results in slower decay and more pronounced oscillations.
7.  "**System type**" for an open-loop transfer function is defined by the number of pure integrators (poles at the origin, $s=0$) present in the function. Its significance for steady-state error to a step input is that a system type of 1 or higher results in zero steady-state error, whereas a type 0 system will have a finite, non-zero error.
8.  A **PD controller** reshapes the root locus by adding a zero to the open-loop system, which tends to pull the branches to the left, improving damping and speed. A common drawback of its ideal implementation is that the differentiator amplifies high-frequency noise, degrading the signal-to-noise ratio.
9.  The main purpose of adding an **integrator** to a control system is to increase its system type, thereby reducing or eliminating the steady-state error for certain types of inputs. A key challenge this introduces is that integrators tend to shift the root locus to the right, potentially making the system slower or even unstable.
10. Increasing the **sample rate** in a digital control system can improve performance by making the derivative and integral approximations more accurate and by reducing control loop delays, which helps maintain phase margin. However, a significant drawback is increased susceptibility to numerical precision and rounding errors, and amplified noise in derivative calculations due to the larger gain factor $1/T$.

---



## Control Systems Engineering: Essential Cheatsheet

**I. Core Concepts**

- **Control (Feedback/Closed-Loop):** Regulating system behavior by sensing, comparing error, and reacting to reduce it.
- **Instrumentation:** Tools for measurement, observation, and control.
- **Laplace Transform:** Converts linear differential equations to algebraic polynomials; simplifies convolution to multiplication.
    - **Time Domain vs. Laplace Domain:** Input $u(t) \leftrightarrow U(s)$, Output $y(t) \leftrightarrow Y(s)$, Transfer Function (TF) $g(t) \leftrightarrow G(s)$.
    - **TF:** $Y(s) = G(s)U(s)$.
    - **Final Value Theorem (FVT):** $f(\infty) = \lim_{s\to0} sF(s)$. For unit step input, $y(\infty) = \lim_{s\to0} G(s)$ (DC gain).
- **Unity Negative Feedback:** Output subtracted from desired input ($V(s)$) to generate error signal $E(s)$.
    - **Closed-Loop TF ($T(s)$):** $T(s) = Y(s)/V(s) = G(s)H(s) / (1 + G(s)H(s))$.

**II. Modelling Control Systems**

- **Origin of TFs:** From mathematical models of linear dynamic systems.
- **Mechanical Systems (Translational/Rotational):** Use free-body diagrams to sum forces/torques.
    - **Impedance Concept:** Ratio of force/torque to displacement/angle in Laplace domain.
    - **Component Impedances:**
        - Translational: **Mass** ($M s^2$), **Spring** ($K$), **Damper** ($B s$).
        - Rotational: **Inertia** ($J s^2$), **Torsion Spring** ($K$), **Viscous Damper** ($B s$).
- **Gearboxes:** Divide angle/speed, multiply torque by gear ratio. Impedance divided by (gear ratio)$^2$ when moved to one side.

**III. Sensing & Measuring**

- **Purpose:** Monitoring, alerting, quality management, **feedback control**.
- **Observer Effect:** Act of measuring inherently affects the system by transferring energy.
- **Error Types:**
    - **Accuracy:** Closeness of mean measurement to true value.
    - **Precision (Repeatability):** Spread/variability of measurements.
    - **Noise:** Random fluctuations affecting precision (not accuracy), often Gaussian.
    - **Nonlinearity:** Hard (limits), Soft (hysteresis – dependence on history, causing lag).
- **Key Sensor Examples:**
    - **Proximity Switches:** Binary sensors (inductive, capacitive, Hall effect).
    - **Time-of-Flight (ToF):** Measures distance by round-trip time (ultrasonic, optical).
    - **Encoders:** Linear/Rotary, Incremental (quadrature encoding), Absolute (Gray code).
    - **Strain Gauge:** Measures elongation, resistance changes. Used with **Wheatstone Bridge** for precise measurement (full bridge for linearity/temp compensation).
    - **Load Cell:** Combines strain gauges and a spring element to measure force.
    - **Accelerometers:** Measure acceleration directly (moving mass, null balance).
    - **Gyroscopes:** Sense angular rate (spinning, vibrating structure MEMS, optical).
    - **Sensor Fusion:** Combining multiple sensors for improved data (e.g., GPS + IMU).

**IV. System Properties: Time Domain**

- **Poles:** Define exponential "modes" (time constants). For **stability**, all poles must be in the Left-Half Plane (LHP).
- **Zeros:** Affect "residues" (weights/amplitudes) of modes. Do not affect stability directly.
- **First-Order Systems** ($G(s) = K_{dc} / (1 + s\tau)$):
    - **Time Constant ($\tau$):** $\tau = 1/a$ (for $G(s) = A/(s+a)$).
    - **Settling Time ($T_s$):** Time to settle within 2% of final value. $T_s \approx 4\tau = 4/a$.
    - **Rise Time ($T_r$):** Time from 10% to 90%. $T_r \approx 2.2\tau = 2.2/a$.
- **Second-Order Systems** ($G(s) = K_{dc}\omega_n^2 / (s^2 + 2\zeta\omega_n s + \omega_n^2)$):
    - **Complex Poles:** Lead to oscillatory behavior.
    - **Damping Ratio ($\zeta$):** Controls oscillation decay rate and overshoot.
        - $0 < \zeta < 1$: **Underdamped** (oscillations, overshoot).
        - $\zeta > 1$: **Overdamped** (no oscillation, slower).
        - $\zeta = 1$: **Critically Damped** (fastest without overshoot).
    - **Undamped Natural Frequency ($\omega_n$):** Natural oscillation freq. without damping.
    - **Damped Natural Frequency ($\omega_d$):** $\omega_d = \omega_n\sqrt{1-\zeta^2}$.
    - **Settling Time ($T_s$):** $T_s \approx 4/(\zeta\omega_n) = 4/\alpha$.
    - **Percentage Overshoot (%OS):** $\%OS = 100e^{-\zeta\pi/\sqrt{1-\zeta^2}}$. Depends _only_ on $\zeta$.
        - $\zeta = -\ln(\%OS/100) / \sqrt{\pi^2 + \ln^2(\%OS/100)}$.
    - **Temporal Dominance:** Poles/zeros closer to origin (slower dynamics) dominate response.

**V. Control Loops & Steady-State Error**

- **Steady-State Error ($e(\infty)$):** Difference between desired and actual output as time approaches infinity.
    - $e(\infty) = \lim_{s\to0} sV(s) / (1 + G(s)H(s))$.
- **Error Constants (for Open-Loop $G(s)H(s)$):**
    - **Position ($K_p$):** $K_p = \lim_{s\to0} G(s)H(s)$; for step input: $e(\infty)_{step} = 1 / (1 + K_p)$.
    - **Velocity ($K_v$):** $K_v = \lim_{s\to0} sG(s)H(s)$; for ramp input: $e(\infty)_{ramp} = 1 / K_v$.
    - **Acceleration ($K_a$):** $K_a = \lim_{s\to0} s^2G(s)H(s)$; for parabolic input: $e(\infty)_{parabola} = 1 / K_a$.
- **System Type:** Number of pure integrators (poles at origin, $s=0$) in $G(s)H(s)$.
    - **Type 0:** Finite error for step, infinite for ramp/parabola.
    - **Type 1:** Zero error for step, finite for ramp, infinite for parabola.
    - **Type 2:** Zero error for step/ramp, finite for parabola.

**VI. Root Locus (RL) Design**

- **Concept:** Graphical plot of closed-loop pole locations as gain ($K$) varies $0 \to \infty$.
    - **Closed-Loop Poles:** Roots of $1 + K G(s)H(s) = 0$.
    - **Gain Criterion:** $|K G(s)H(s)| = 1$.
    - **Angle Criterion:** $\angle (K G(s)H(s)) = (2n+1)180^\circ$, determines RL shape.
- **Key RL Rules:**
    1. **Symmetry:** About real axis.
    2. **Start/End:** Start at open-loop (OL) poles, end at OL zeros.
    3. **Asymptotes:** For excess poles, angles $\theta_A = (2n+1)180^\circ / (\text{excess})$.
    4. **Asymptote CoG:** $s_{cg} = (\sum p_i - \sum z_i) / (\text{excess})$.
    5. **Real Axis Segments:** A point is on RL if odd number of OL poles/zeros to its right.
    6. **Break-away/Break-in Points:** Where loci leave/arrive real axis (at $90^\circ$). Solve $\sum \frac{1}{s-z_i} = \sum \frac{1}{s-p_i}$ or $dG(s)/ds = 0$.
    7. **Angles of Departure ($\theta_{p1}$):** From complex OL poles. $\theta_{p1} = \sum \theta_{zi} - \sum_{i \neq 1} \theta_{pi} \pm 180^\circ$.
    8. **Angles of Arrival ($\theta_{z1}$):** To complex OL zeros. $\theta_{z1} = \sum \theta_{pi} - \sum_{i \neq 1} \theta_{zi} \pm 180^\circ$.
    9. **Imaginary Axis Crossings:** Use **Routh Array** (Routh-Hurwitz Stability Criterion). A **zero row** in Routh array indicates poles symmetrical about origin (e.g., on imaginary axis).
    10. **Gain Values (at desired pole $s_d$):** **Monic Form Gain** $K_m = (\prod |\text{pole lengths to } s_d|) / (\prod |\text{zero lengths to } s_d|)$. (Actual controller gain $K$ adjusts for $G(s)H(s)$ monic form gain).

**VII. Controller Types & Digital Implementation**

- **Reshaping RL:** Add controller poles/zeros if desired poles not on existing locus.
- **PD (Proportional-Derivative) Control:** $H(s) = K_p + K_d s = K(s+z_{pd})$.
    - **Effect:** Adds a zero, pulls RL left, improves transient response (faster, more damping).
    - **Drawbacks:** Amplifies high-frequency **noise**, **set-point kick** (impulsive output on step input).
- **PI (Proportional-Integral) Control:** $H(s) = K_p + K_i/s = K(s+z_{pi})/s$.
    - **Effect:** Adds an **integrator** (pole at origin) to increase system type, reducing **steady-state error to zero for step inputs**. Adds a zero very close to origin to minimize transient impact.
    - **Trade-off:** Improves SS error but typically **slows transient response**.
- **PID (Proportional-Integral-Derivative) Control:** $H(s) = K_p + K_i/s + K_d s$.
    - Combines benefits of PD (transient) and PI (SS error).
    - **Design Strategy:** Design PD for transient, then add PI for SS error.
- **Phase-Advance Networks (PANs) / Phase-Lead:** $H(s) = K \frac{s+z_{pd}}{s+p_f}$ (where $p_f > z_{pd}$).
    - **Purpose:** Practical alternative to ideal PD; filters differentiator to mitigate noise/set-point kick.
    - **Advantages:** Reduced noise, realistic implementation, can be passive (if K<1).
    - **Disadvantages:** Does not reduce excess of poles, more complex design (two parameters), less "power" than ideal PD, can worsen overshoot.
- **Digital Controller Implementation:**
    - **Sampling:** Error signal $e(t)$ sampled at discrete intervals $T$.
    - **Approximations:**
        - **Derivative (Backwards Difference):** $d_n = \frac{1}{T}(e_n - e_{n-1})$.
        - **Integral (Rectangular/Euler):** $i_n = i_{n-1} + e_n T$.
        - **Integral (Trapezoidal):** $i_n = i_{n-1} + \frac{T}{2}(e_n + e_{n-1})$.
    - **Sample Rate ($T$):** High rate improves approximation accuracy, reduces delays (improves phase margin). Drawbacks: computational effort, numerical precision issues, noise susceptibility.

---