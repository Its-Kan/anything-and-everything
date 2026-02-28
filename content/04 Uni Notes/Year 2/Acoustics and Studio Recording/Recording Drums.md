**Year**: [[Year 2]]
**Subject**: [[Acoustics and Studio Recording]]

---
The drumkit is a collection of sources, however in a mix, we want to treat it as a whole, cohesive instrument. Drums have a wide dynamic and frequency range, which can make it hard to setup.
```table-of-contents
Index
```
---
## Setup

> [!tip] Reminder
> As a reminder, here's the notes about [[Microphones]], [[Recording Basics]] and [[Stereo Recording]]. 

Make sure to set aside ample time to setup the drums itself.
### Before you start
- What genre are you recording? Make sure it fits in the mix you're creating
- Consider the kit itself: 
	- Snares, sticks, beaters and cymbals can be replaced to suit sound
	- You can tune or damp snares
- Consider the room:
	- Hard to change, but placement of the drum can affect sound. Hold the floor tom, and bang it around the room to find a good 
### Tone
#### Drum Tuning
- Tuning drums affects tone/resonance. 
- Takes a while and is very complicated, but can affect the sounds
#### Damping
- Adds an amount of mass added to the drum heads. Near the heads, 
	- Tape 
	- Moon gel
	- O-rings: plastic hoops that evenly dampen sound
- Make sure to listen to the mics. Doesn't matter what it sounds like in the room

---
## Miking the Drumkit
### Overheads
The core of the recording revolves around a stereo mic pair, also known as overheads. Jazz drums sometimes only use a stereo pair.

Any of the stereo techniques we've covered can work (see [[Stereo Recording]]), but there are also some drum-specific techniques. 
#### General
##### XY
- Gives an accurate, neutral stereo image with no phase issues
- Positioned over the drummer's head pointing down, or placed in front of the kit

| ![[Overhead XY Pair Top View.png]] | ![[Overhead XY Pair Front View.png]] |
| ------------------------ | ------------------------------------ |

##### Spaced
- Most common stereo miking technique
- Any matched pair of mics, with any pattern, placed a distance apart, about a metre above the kit
- Often equidistant from the snare, to keep the snare central and prevents any phase mixing

| ![[Overhead Spaced Top View.png]] | ![[Overhead Spaced Front View.png]] |
| --------------------------------- | ----------------------------------- |

> [!question] Symmetry?
>Many engineers assume the snare is central, but it's really up to you. Regardless, the overheads alone should give:
>- A full stereo width
>- Full resonant sound
>- Decent balance of levels

#### Drum-Specific
##### Glyn Johns Overheads
- Named after the British recording engineer
- Two equidistant from the snare mics
	- One directly above the snare (100-150cm)
	- One above the floor tom, facing the hi hat
- Plus a kick and snare mic
- With cardioid or figure-8 mics

| ![[Glyn Johns Overheads Top View.png]] | ![[Glyn Johns Overheads Front View.png]] |
| -------------------------------------- | ---------------------------------------- |
##### Recorderman Overheads
- Recent technique similar to Glyn Johns
- Two mics, equidistant from the kick AND snare
	- One above the snare (100cm)
	- One over the drummers right shoulder (45º) 
- Augmented with kick/snare spot mics
- Originally ribbons but others work
- Good for bedroom and budget studios

| ![[Recorderman Top View.png]] | ![[Recorderman Front View.png]] |
| ----------------------------- | ------------------------------- |
### Kick
Usually under-represented in overheads, and always almost has it's own mic.
#### Inside
- Great isolation, but not the "true" sound of the kick.
- Common mic choices are dynamic, the following are specifically bass drum mics:
	- *AKG D112*
	- *Shure Beta 52A*
	- *Sennheiser MD421*
- In terms of placement:
	- Avoid the centre line between drum heads, as modes interact strangely.
	- Moving the mic can also change the tone
		- Moving front/back gives a click near the beater
		- In the middle gives a full sound
		- Nearer the resonant head gives a tighter/shorter sound
#### Outside (front)
- If there's no hole in the head, this is the next option
- Placed on the audience side, in front of the kick
- More of a natural sound, but more spill
- More mic choices here, but standard mics still work. You can use the ones mentioned before
#### Outside (pedal side)
- A lot of attack, but if paired with a front however keep phase in mind. Invert one of them to ensure no phase cancellation
### Snare
Usually the centre of the kit, for both the drummer and engineer, however very prone to bleed and a wide dynamic range. 

There are two sound sources: the stick impact (body) and the snare wires (buzz). 
- That buzz can be annoying, especially if a tom resonates with it. Fix this with tuning.
- The top and bottom of a snare are usually miked. Beware of phase cancellation though; invert one.
- For isolation, use a cardioid mic, where the null point faces the hi-hat.

- *SM57* is a common mic, but anything goes.
- Standard positions are just above the rim, pointing to the centre. Make sure your rummer doesn't hit it!
- Distance and angle can make a difference:
	- Closer to get more of the stick
	- Angle towards the edge for brighter overtones
- Miking the shell (the side) of the snare can work, which adds body.
### Cymbals
These are mostly captured by the overheads, but you might want to add spot mics to add more definition.
- Use condensers to capture high frequency transients. Ribbons can give a softer, almost vintage sound.
- These sources are complex, but they can behave predictably:
	- The even harmonics (gives a full, round sound) go upwards from the cymbal
	- The off harmonics (gives bright, thin sound) go out from the cymbal
	- We can use this into like tone control, depending on the angle of the mic.
	- However, right along the plane of the cymbal there's almost no sound.

![[Snare Miking Tone Control.png]]
#### Rides
- Mic near-ish the impact point
- Can be placed relatively closed
#### Hi-hats
- Placed opposite/above
- The snare is the main source of bleed, so put the mic in-line with snare, so the hi-hat blocks the snare.
- Beware of air when the pedal is pressed. 
#### Crashes
- Cymbals move! Especially with crashes, the wobble will add an annoying tremolo. 
- Mic slightly above the crash to avoid.
### Toms
They're often spot-miked individually, if you need. We want consistency, so the same mic for every tom:
- Dynamics are popular for this, *SM57*, *MD421*, but condensers also work.

Similar guidelines to a snare:
- Closer gives more attack and body
- Middle for stick impact, edge for more high frequencies
### Room Mics
These add reverb and "meat" to drums. We just want a couple points in the room, with spaced, distance mics. We can get more of the room using cardioids pointing away, or Figure-8s for more "room". 

---
## Samples
We get augment drum recordings with samples. We can hance the drum sounds, or replace any recordings that are substandard.

We can do this with:
- Drum triggers, which send MIDI out of a drum hit
- Dedicated software, such as Slate Trigger
- Extract MIDI from audio

Probably don't do this for the assignment though. It covers up all the hard work.
