**Year**: [[Year 2]]
**Subject**: [[Acoustics and Studio Recording]]

---
In a room, sound is influenced by how the sound interacts at the boundaries of the room. The characteristics of the room can affect m:
- The quality of sound
- The timbre of music
- The intelligibility of speech

```table-of-contents
```
## Room Impulse Responses (RIR)

A [[room impulse response]] helps us understand how sound behaves in a specific environment. To do this, we simplify it to the simplest form of sound, an impulse, which can be a clap, gun shot, balloon popping, etc. 

For sound waves at any surface, some energy is reflected and some is absorbed. This absorbed energy is determined by an absorption coefficient, $\alpha$, which is a number between 0 and 1. An idealised open window has an absorption coefficient of 1, i.e. none of the sound energy is reflected.

What happens with the sound in a room can be broken down:

- Direct sound arrives at the listener first, and is "uncontaminated", as it doesn't interact with any boundaries.  
	![[Direct Sound.png]]
- Early reflections are after the direct sound, where discrete reflections are heard. Delays >30ms after the direct sound are heard as "echoes" or reflections.  
![[Early Reflections.png]]
- Reverberation, which accounts for all the other boundary interactions that happen. 
	 ![[Reverberation.png]]

Reverberation can be broken down even more. When there's a sound:
-  A growth in level time, which depends on time between the reflections
	- A larger room will have a longer growth time
	- More absorption will give a shorter growth time
- Then it reaches the steady state level, where the input energy is equal to the energy that is lost, causing a net zero energy loss
	- The steady state level is higher when surfaces aren't very absorbent 
- Decay where the sound dies down
	- The decay is longer when there's little absorption at each reflection

The [[reverberation time]] is the time taken for the sound level to decay by 60 dB, or $RT_{60}$.

![[Reverberation Time.png]]

## Historical Context

So, a lot of these theories were pioneered by one guy called Wallace Sabine, who used an organ pipe and a stopwatch to investigate [[reverberation time]]. He was able to establish acoustic properties.

### Sabine Equation

The Sabine Equation gives us a way to calculate reverberation time:
- $T_{r}= 0.161 \frac{V}{A}$
- where V is room volume, and A is effective surface area
	- the effective surface area is given by the products of each surface area, multiplied by each surface's absorption coefficient.
	- $A = \sum_{i+1}^{n}$ 
