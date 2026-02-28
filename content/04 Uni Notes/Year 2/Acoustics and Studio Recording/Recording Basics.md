**Year**: [[Year 2]]
**Subject**: [[Acoustics and Studio Recording]]
**Topic**: Recording Basics
**Date Created**: 2024-12-02, at 00:07

--- 
```table-of-contents
```
---
## Levels
There are multiple levels to... well, levels!
### Signal Chains
- **[[Mic Level]]:** Mic levels are very quiet, around -60 to -40 dBV (0.001V to 0.01V), and comes from the electrical signal out of the microphones. Due to these small voltages, they are very prone to noise, so ensure they quickly route to a preamp.

> [!info] More info
> See [[Frequency, Phase, Amplitudes and Decibels]] for more about decibels.

- **[[Line Level]]**: This is a more convenient and robust signal level, we can safely transport around the studio at around +4dBu (1.23V). This is the normal I/O level for most equipment. 
### Managing Signals
Dynamic range is the smallest and largest signals the system can handle. Low signals are lost in the noise floor, while high signals will distort.

We can adjust this with [[gain staging]], which ensures the signal level is optimal at each point. This is it going right:
![[Gain Staging.png]]

And this is what it looks like going wrong:
![[Gain Staging Mistake.png]]

So how do we know if we're gain staging right? Then, we have to rely on [[metering]], which is a visual indicator of our signal levels. Whenever you adjust the gain stage, you want to meter the signal to ensure no clipping.

When looking at a meter, make sure to look at the scale and limits of the meter. Look up what the meter is telling you; 0 might be the top limit, or the optimal value.

To set a gain change, make your performer play comfortably, and then aim for the peak to hit **-6dB**, or **-12dB** if you want to be safe.