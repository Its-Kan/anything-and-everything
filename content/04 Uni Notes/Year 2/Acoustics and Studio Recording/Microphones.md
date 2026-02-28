**Year**: [[Year 2]]
**Subject**: [[Acoustics and Studio Recording]]
**Topic**: Microphones
**Date Created**: 2024-12-02, at 00:34

--- 
Microphones are merely transducers, which convert pressure change to voltage. It's like a ball on the water, if you push it down, it comes back up and created ripples.
```table-of-contents
```
---
## Mic Specs
### Frequency Response
This is how well the mic responds across its frequency range, usually between 20Hz to 20kHz. It might be more quiet for certain frequencies
### Dynamic Range
As said in [[Recording Basics]], this is the highest and lowest signals the microphone can deal with. 

At the low end is self noise, where lower is better. This is the noise produced by the mic's circuitry itself.
- If it's <10dBA, then it's a pretty good mic
- If it's >20dBA, then not so good
However not all mics have

The high end is sensitivity, where higher is *usually* higher.
- Passive mics are around -60dBV
- Active mics are around -30dBV
### Maximum Acceptable Level
This is the largest sound pressure level (SPL) the mic can handle. Reach above this, then the mic will distort and even damage the mic. Ever get to these levels, and your ears will definitely hurt, especially right up next to drums. 

--- 
## Types of Microphone

We differentiate mics based on their transducer.
### Dynamic
These mics use a coil of wire attached to a diaphragm, moving over a fixed magnet. The moving magnet in a coil results in a voltage change analogous to the changing acoustic pressure.
![[Dynamic Microphone.png]]

> [!example] Examples of Dynamic Mics
> - **SM57** - a good, everything mic used on guitar cabs and drums
> - **RE20** - another universal mic, but principally made for vocals.
> - **D112** - designed for kick drums 
#### Characteristics

| Advantage                                      | Disadvantage                                      |
| ---------------------------------------------- | ------------------------------------------------- |
| Extremely robust and reliable                  | "Rougher" frequency response (not flat)           |
| Can handle high SPLs (as components are heavy) | Poor transient response (as components are heavy) |
| Low handling noise (noise when holding it)     | Low output level (passive mic)                    |
### Ribbon Mic
An extremely thin, corrugated metal ribbon which is suspended between the poles of a magnet.

![[Ribbon Microphone.png]]

> [!example] Examples of Dynamic Mics
> - **R1**

#### Characteristics

| Advantages                               | Disadvantages    |
| ---------------------------------------- | ---------------- |
| Extremely sensitive                      | Fragile          |
| Excellent transient response             | Low output level |
| Ribbon "sound" (high frequency roll off) |                  |
### Condenser Mic
Probably the most common mic we'll run into. It's a capacitor, of which one side is the diaphragm. If the diaphragm moves, it causes a change in capacitance.

![[Condenser Microphone.png]]

> [!example] Examples of Dynamic Mics
> - **NT5**
> - **C414 XLS** 

#### Characteristics

| Advantages                        | Disadvantages     |
| --------------------------------- | ----------------- |
| Excellent sensitivity             | *Can* be delicate |
| Extended, flat frequency response | Require power     |
| Low noise                         |                   |

--- 
## Mic Characteristics
### Diaphragm Size
The size/weight of a diaphragm has an impact on sound:
- smaller, lighter elements will result in better transient/frequency response
- at the cost of a lower signal level, so more gain and noise
### The "Sound"
Mic types have subtly different sounds.
- **Condensers**: "hyped", "detailed"
	- for vocals, small noises like lip smacking are more audible
- **Dynamic**: "punchy"
	- sounds that have more body to them are accentuated
- **Ribbons**: "gentle", "warm", "rounded", "buttery"
### Directivity/Polar Pattern
Mics can be direction-sensitive, which is termed their polar pattern. Omni and Figure-8 are the opposite ends of a spectrum for polar patterns. A C414 can switch between these.
#### Types
##### Omnidirectional
This is where the mic is equally sensitive to sound in all directions.
![[Omnidirectional Microphone.png]]
##### Figure-8
This is a Figure-8 mic, but rejects sound from the sides.
![[Figure 8 Microphone.png]]
##### Cardioid
Between an omnidirectional and figure-8, which is most sensitive at the front, and becomes less so as you move towards the back.
![[Cardioid Microphone.png]]
#### Proximity Effect
Directional/non-omnidirectional microphones exhibit the **proximity effect**. This is where lower frequencies are boosted, which increases when the mic gets closer to the source.

--- 
## Using a Mic

There are two components to placing a microphone in a room:
- **Direct sound**: close to the source 
- **Reverberation**: far away from the source
The critical distance is where reverb and direct sound are equal. This is normally no larger than a meter.

---
## Choosing a Mic

1. Consider the source:
	- Bright, high frequency transients? *Cymbals, 12-string guitar*
		- Small diaphragm condenser
	- Powerful, mid-range punch? *Toms*
		- Mid/large diaphragm dynamic
	- Low end? *Bass guitar, Kick drum*
		- Large diaphragm dynamic/condenser
2. Consider the placement:
	- Balance between direct sound and reverb
	- Separation

