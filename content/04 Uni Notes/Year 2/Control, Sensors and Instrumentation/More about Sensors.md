 [Module:: [[Control, Sensors and Instrumentation]]]
[Date Created:: 2025-04-08]

--- 
These are technologies for sending position in space, attitude and some other quantities such as temperature, pressure or light. 
```table-of-contents
```
---
## Position
Identifying position in 3D space is difficult. There are two approaches:
- External references
- Dead reckoning
### Satellite Navigation
There are 4 currently operational systems:
- GPS (USA)
- GLONASS (Russia)
- BeiDou (China)
- Galileo (European Space Agency)

They all have multiple satellites in low-earth orbit (~20000km), and each one broadcasts information about it's current orbit and the current time. The receiver contains a local clock kept accurate by the satellites. Using multiple of these satellites, we can compare the receive times of each, and use **trilateration** to determine position.

However, we're limited by:
- Local clock precision
- Atmospheric phenomena affecting path delays
- Consumer equipment limited to around 30m

Atmospheric effects are localised, so if there's another receiver with a known location, you can use those to compensate. This is called **Differential GPS** (DGPS) using two receivers: one fixed, and one roving. The fixed receiver can be transported or part of a fixed network, and It must be reasonably local.
### Indoor Positioning
Indoor GPS signals are too weak to use. So for robotics for instance, multiple fixed cameras are sometimes used:
- Robots or end effectors carry fiducial markers (often reflective)
- Position can be determined accurately by triangulation
- Orientation can often be determined as well

Sometimes it's the other way round, and the space has the fiducial markers
- Common in industrial robotics
### Dead Reckoning
This is the process of estimating current position based off:
- Your previous position
- Velocity, acceleration or other movement data
- Elapsed time

Obviously, much more error prone. 

However, **inertial navigation** uses dead reckoning given information on acceleration, and angular rate in an **Inertial Measurement Unit** (IMU). Transatlantic flights often use this as there aren't any external references to use.

Measuring position or velocity requires an external references, however acceleration does not. A simple proof of this is on a mass on a spring. If we accelerate the frame the system is in, the mass will move and compress the spring. This is a type of **deflection transducer**. Acceleration of the sensor leads to a phantom force acting on the mass. And since displacement is proportional to acceleration (assuming a linear spring), and we can find acceleration without any outside references. These are used commonly in MEMS (Micro Electro-Mechanical System).

The null transducer variant of this is a **null balance accelerometer**. An actuator attempts to retain zero mass displacement, but the force to balance this out is the sensor output. Micro sensors with piezo-electric balance actuators available.
### Gyroscope
Acceleration is only useful if your attitude (orientation) is known. Gyroscopes can help with this by sensing angular rate. There's two possible applications:
- Creating a "stable table" (null deflection)
	- This can be done completely mechanically
	- Saves a lot of mathematics! 
- Collecting angular rate information for numerical integration. 

A spinning gyroscope exhibits torque-induced [[precession]]. Rotations perpendicular to the spin axis generates a torque perpendicular to both. This torque can be measured, and used to measure angular velocity. 

Other common gyroscope technologies are vibrating and optical gyroscopes.
#### Vibrating Structure 
A vibrating mass will tend to continue vibrating in the same plane. Changing the plane of vibration results in a Coriolis force on its supporting structure, as a force is required to change that plane. They can be made very small as they don't need to rotate, meaning very light and very low cost. 

However accuracy and precision are very limited due to thermal drift and sensitivity to acceleration.
#### Optical
These use the constant speed of light and the Sagnac effect.

Light is sent in two directions around a circle. The rotation of the circle causes a differential change in path length, then interferometry can be used to detect the different transit times. 

Typical implementations are laser-ring gyroscopes (LRGs) and fibre-optic gyroscopes (FOGs). They're large and expensive, but very accurate and precise. 
### Sensor Fusion
Dead reckoning can be combined with reference-based approaches. This is known as sensor fusion, and is not unique to navigation.
### SLAM
Stands for Simultaneous Localisation And Mapping. It's not really a sensor technology, but uses dead-reckoning and external references. SLAM maps the environment as a reference using dead reckoning, and then uses the environmental features to improve the its accuracy using sensor fusion as the map builds up.  LIDAR is commonly used.
## Pressure
As you know, pressure is just force per unit area. Pressure sensors are therefore related to force sensors. It may sense:
- absolute pressure, relative to total vacuum
- relative pressure, with two sensing ports
- gauge pressure, relative to ambient
- vacuum pressure, relative to ambient

Electronic pressure sensors typically use:
- Strain gauges, like a load cell
- Capacitive sensing of a deflecting diaphragm
- Piezoelectric material that generate voltage when deformed
- LVDT (low voltage differential transformer): a diaphragm moves a ferromagnetic core within a transformer 
## Temperature
### Thermocouples
These measure differential temperature using the Seebeck effect. 

Let's say you have a wire, with both ends at different temperatures. This causes a voltage difference. The problem is that if we wanted to measure this voltage, the probes end up in the same place. The temperature differences cancel out. So, we need different materials for the sense wire and connections, making sure they have different Seebeck coefficients. 

This voltage is tiny however. This can be alleviated using a thermopile, which consists of multiple thermocouples in series for better sensitivity. Calibration is unnecessary too, as the characteristics depend only on the materials used.
### Thermistors
These are temperature-dependent resistors.
- PTC (positive temperature coefficient) thermistor resistance increase with temperature
- NTC (negative temperature coefficient) thermistor resistance decrease with temperature.

Accuracy can be very good, but relies on accurate manufacture.
## Light
The photodiode can be used for light sensing, seen in [[Movement and Deflection]].
### Phototransistor
These can be an alternative. A bipolar junction transistor (BJT) allows current to flow from collector to emitter. 