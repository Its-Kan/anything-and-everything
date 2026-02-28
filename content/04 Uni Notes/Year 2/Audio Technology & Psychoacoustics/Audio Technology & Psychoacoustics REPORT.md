## Introduction 
> [!uninotes]
> Overview of report contents; Response to the briefing; How your approach combines synthesis and psychoacoustics)

When given the briefing of developing synthesiser software aimed at sixth-form Music Technology A-level students, the project explored into modern electronic genres that would be relevant to students today. Two genres that stood out were lo-fi hip-hop, which has become renowned for the multitude of "beats to study to" playlists, and botanica, which has become popular on YouTube for uniquely "natural" and glitchy sound design. These genres also seem to have a lack implementation in the chosen engine Purr Data (PD), whose community is saturated with patches revolving around hard or ambient generative beats. The synthesiser was designed with this in mind.

A popular synthesis method in botanica is granular synthesis to create background textures, however this wasn't enough for a composition, so vocoder was implemented to add ethereal-sounding voices. In terms of the lo-fi side, more foundational elements of the genre were added, such as a soft Reese bass, a degraded lo-fi piano, as well as a drum machine to bring it all together. With so many synthesis techniques to implement, it would be easy for the user interface (UI) to become crowded and messy, so readability was a priority when designing.  
 
The audio-visual composition using GEM will follow the established visual aesthetics of both lo-fi and botanica, using floaty, dream-like visuals, and pastel colours. All the visual elements in the arrangement correlate to one of the modules, and will update if any of the variables change. 

[insert botanica and lofi visual examples]

Along with the synthesis, there are two psychoacoustic phenomena that have been implemented. The aim was to integrate two psychological phenomena seamlessly with the composition, so more melodic and rhythmic examples of phenomena were explored:
- For the melodic phenomena, the Deutsch's scale illusion [reference] was chosen, where alternating melody and harmony in one ear, and vice versa in the other, seem to merge into one melody line and one harmony line;
- And for the rhythmic phenomena, the galloping rhythm [reference] was chosen, which is an example of auditory streaming. At slow speeds/small intervals, there seems to be one stream, perceived as a repeating 3-note melody. At faster speeds/larger intervals, it seems to break down into two streams, one lower one, and one higher one at half the speed.

Simplified versions of these phenomena are available in the upper-right module, which use the lo-fi module to play the phenomena, with adjustable variables. However, both phenomena are also incorporated into the audio-visual composition, using the vocoder for the scale illusion, granular synthesiser for the galloping rhythm (as it's able to change the playback speed of a sample). 
## Synthesis Report 
> [!uninotes]
> Synthesis Report (4 pages) 
> o 2.1 Introduction to your synthesiser (Synth method; theoretical background; context; how you’ve made your patch ‘self-documenting’) 
> o 2.2 Pd design rationale (Structure of your Pd patch and any sub-patches; how you’ve achieved the main synthesiser build - use annotated screenshots) 
> o 2.3 Audio-visual demonstration (Aesthetic choice of visual objects in relation to the synth audio; how you’ve used GEM to build the composition; linking with the synth) 
> o 2.4 Evidence of testing and evaluation (Your testing plan to show how well each section works; qualitative feedback from user tests)

### An intro to "Mosse"
[image of synth]

The name of the multi-synth is "Mosse," inspired by the soft, natural sounds of botanica. As stated before, there are multiple synthesis techniques used here, so each module contains a "pd" sub-patch, which provides instructions on how to use it, as well as the following descriptions for their respective module:
- A granular synthesiser, which effectively "chops" a sample into many bits (grains), and then plays back these grains. This allows us to play with each grain's duration, playback speed, or even randomise its start position or panning to get unique textures.
- Originally developed in the 1930-40s by Homer Dudley [reference], a vocoder analyses the formants of a sound (the modulator), usually a human voice, and then applies the magnitudes to their according formants in another sound (the carrier), which should have a lot of frequencies available to modulate. This technique was popularised by Daft Punk to achieve a unique robotic sound in vocals, but has been used in modern electronic tracks to add colour to basses.
- A simple, wide Reese bass, popular in a wide variety of electronic genres to fill in the low end. The filter can make keep it in the low sub frequencies, or given distortion or saturation to fill the frequency spectrum.
- A randomised sequencer, based off the detuned piano sound in many lo-fi tracks. It's based around an additive synthesiser, with portamento, dynamic filter and unison implemented. The random notes are based off the notes in the Lydian scale.
- A simple drum sequencer with a kick, snare, clap and hi-hat, with adjustable velocities for each voice.
The top-level for each module's sub-patch also has adequate comments describing the logic behind the signal chain, if the user would want to understand how the technical workings of each module.
### PD Design Rationale
#### Granular Synthesiser
The granular synthesiser is inspired by both QCGInteractiveMusic's [reference] and Really Useful Plugin's [reference] patches. 

The sub-patch uses a sawtooth LFO to play through a sample, which then passes it into an abstraction called, "SingularGrainStereo," which is cloned 16 times to avoid clipping [two images]. The abstraction takes a sample, and then outputs a grain using the current position in the LFO, and a very short volume envelope of adjustable decay. Bringing all these grains together recreates the sample, but now we can manipulate these grains individually. 
- a "random" object can add a random integer to the current position, making it jump around the sample, giving glitchy, natural ambience. 
- another "random" object can give each grain a random panning, which can give a natural stereo widening effect.
- the sawtooth LFO's frequency can be increased or decrease, allowing us to change the playback speed 
- the decay in the volume envelope of each grain can be increased, causing the grains to overlap with each other, almost like "blurring" the sample together.
#### Vocoder
There were two approaches to doing this in PD: either manually with multiple band passes for each formant, or automatically using the fast Fourier transform (FFT) algorithm. When testing the former, the sub-patch got cluttered with how many band passes needed to get a clean result, and even then, there ended up being a lot of spectral noise, so the FFT algorithm was looked into. "Loadbang - Programming Electronic Music in Pure Data" by Johannes Kreidler [reference] proved to be a valuable resource in understanding the "fft~" objects and their uses. So, the module was created with inspiration from Naofumi Aoki's patch [reference], as there was a lack of examples using the FFT in PD on the internet.

The user loads in wav samples for the modulator and carrier, which is stored in their respective arrays. The carrier is run through a "fexpr~" object, which takes each sample, and takes it away the previous sample. This effectively differentiates the signal, cancelling out low frequencies and accentuating transients, which should make the output much clearer when the modulator is applied. The differentiated carrier and the modulator is passed into a "vocoder" sub-patch.

Both samples have the Han window applied to reduce spectral noise, and then run through the reverse FFT (using the "rfft~" object). The magnitude of each formant in the carrier is calculated, and them multiplied with the multiplied by the modulator, which completes the vocoding process. It's converted back to sound with the inverse RFFT (using the "rifft~" object). 
[two images]
#### Reese Bass
To create a wide Reese bass, panned copies of a filtered sawtooth waves across the frequency spectrum, each of which slightly detuned. If they were panned too close to each other, then the waves would cancel each other out, creating beating patterns. To fix this, the copies are panned further from the centre be an integer multiple of the fundamental frequency, and then detuned it. Portamento has also been added whenever the note changes. The old note is stored, and whenever a new note is pressed, a "vline~" object smoothly ramps from the old note to the new note over an adjustable amount of time. Finally, this module is able to be controlled with keyboard, which uses the "key" and "select" objects to detect what key has been pressed.
#### Randomised Sequencer
There are two parts of this module: the randomised note sequence, and the lo-fi piano. 

The randomised sequencer is stored in an abstraction called "RandomNote", and is based off the 7 diatonic chords in the Lydian scale. The midi numbers of the notes in these chords are stored in a message, and is unpacked into 7 individual messages. One of these messages is chosen by random when the abstraction receives a bang. 8 copies of this system are made, each of which have a increasing variable delay to create a sequencer (at small delays, it's akin to a strummed chord; at larger delays, it's like an arpeggiator). A percentage probability is implemented for whether a number is actually outputted, to create unique sequencer.

Each copy sends up to 8 numbers to the cloned "LofiPiano" abstraction. There were 5 distinct aspects to this sound that have been implemented:
- a subtly saturated sin wave, which has been translated to an additive synthesiser, to have more control over the harmonics
- a fast attack and soft release in the volume envelope (using the "adsr~" object)
- a key-tracked filter, to make sure the high end isn't too bright while keeping the spectral shape of every note the same
- a slight portamento, to mimic the warped detuned sound of a cassette or vinyl player
- the felt hammer hitting the keys, by layering filtered white noise over the sound.
#### Drum Machine
Roughly the same approach was used for each drum sound, which played whenever a bang is sent into each sub-patch. Every drum has a transient part which imitates the striking of the drum, and a tonal part that gives the drum it's character, all put through a volume envelope with a sharp attack and varying release. 
- the kick is a filtered and frequency modulated sin wave;
- the clap are 4 copies of filtered noise, each of which delayed very slightly;
- the snare uses FM synthesis to give a unique tonal part;
- and the hi-hat has many square waves with filtering and a very short volume envelope.

The sequencer is controlled through 4 8-element wide arrays, one for the kick, snare, clap and hi-hat. The height of each bar dictates it's amplitude, allowing for variations in velocity. A "counter" sub-patch counts from 0 to 7, and wraps around again, effectively being one bar of eighth notes. The values in this array are read based off the corresponding position in the counter, and sends a bang to the sub-patch containing the appropriate drum sound whenever the value in the array is not 0. The float value of the element in the array controls the loudness of each sound.
### Audio-Visual Demonstration
The musical composition is an original piece, inspired by Porter Robinson's "Worlds" album and awe's work on YouTube. A "qlist" object was used to automatically control all the modules over time, who's timings are stored in the "Composition.txt" file. Both the granular synth and vocoder require samples to work, so they just had to be loaded to be played, while the Reese bass and random sequencer just needed it's root note changing, which is also done in the "qlist".

The visual aspect was inspired by ethereal, dream-like album art with soft, pastel colours, such as Glass Animal's  "Dreamland," and once again, Porter Robinson's "Worlds". Every module has a visual representation, which are also affected by the parameters on each one. The only exception to this is the gradient background, made with the "colourSquare" object, which zooms in and out to make it look like the gradient change over time. 
- The random connected lines in the background (created with the "slideSquares" object) react to the attack of the granular synthesiser (using the "bonk~" object) , stretching vertically whenever it detects a transient in the sample. This allows a visual representation of the galloping rhythm too; as the sample's playback speed gets faster, the stretching gets more frantic.
- The pink and blue rectangles on the left and right react to the pitch on the left and right channels of the vocoder (using the "sigmund~" object) by moving vertically. It also gives a visual representation of Deutsch's scale illusion, as the left and right pitches are always alternating between melody and harmony.
- The Reese bass is represented by an expanding light blue torus in the centre of the screen, who's size and thickness changes based on what note was playing. The time it takes to transition between each size is the same as the portamento length. 
- A particle system that activates whenever the randomised sequencer patch is played.
- The drum sequencer controls two objects: a square in the background which shrinks when a snare is played and rotates when a hi-hat is played, and the 3D model of a statue, which expands when a kick is played and changes it's texture mapping when a clap is played.

A "fade" sub-patch was also created, which takes a colour value and float value from 0 to 1, and can fade the colour between black and the original colour. I used this for the intro with every element, which fades up to make the transition between sections smoother. 
### Evidence of Testing and Evaluation 
Though the target audience is sixth form music tech students, the levels of experience the user will have when using the patch can't be guaranteed. So two participants tested the patch, one with knowledge with synthesis and one without, to play around with the first completed version. Importantly, It was made sure that any assistance wasn't offered or any questions asked weren't answered. This test allowed insights in the design that might be obvious to its creator, but not to a new user. 

From the experienced user, one of the main issues seen was the user taking a while to understand what each button did, as the only descriptor of what buttons did was through text. While not a massive issue, the interface should instantly understandable from first glance. As well as text, icons were added to some of the more important buttons, as visual iconography is a shared language between many interfaces. For example, the "Load .wav" button has an upload icon, and the "Play" button has a black triangle pointing right icon.

From the inexperienced user, there was lot of confusion over what the modules actually are, and what they do. A "pd info" object was added in the top left, that runs down what the synth is, and what the user is looking at, and where to get started into learning more about each module. However, there was no obvious way of knowing it's even clickable. So, it was made so that it appears the first time the synth is opened, and if that didn't work, added a small "<- click me!" comment to incentivise the user to explore the sub-patches more. Short descriptions and tutorials were then added at the top of each module's sub-patch, which gives the necessary context to understand what's happening in each module.  
## Psychoacoustics Report

> [!uninotes]
> 3.1 Explanation of the chosen psychoacoustic phenomenon (Context of relevant fundamentals of psychoacoustics; description of the phenomenon; references to academic literature) 
> o 3.2 Design and implementation of the Pd patch (Overview of patch signal flow; use of automation; user interface design) 
> o 3.3 Evaluation of the effectiveness of the finished patch (Quality of the demonstration produced; ease-of-use; interactivity) 
> o 3.4 Time- or frequency-domain analysis of the patch output audio (Suitable use of waveform plots, spectral plots, spectrograms; appropriate axes; labels/titles etc; accompanying explanation)
### Explanation of the Chosen Psychoacoustic Phenomenon 
As stated, the two psychoacoustic phenomena chosen are Deutsch's scale illusion, and auditory streaming, using the galloping rhythm. There were two ways the synth demonstrates both phenomena: one was integrated into the composition, and the other was through the "PlayArea" module on the top right, which allowed the user more specific control over the variables that could affect the phenomena. 

Deutsch's scale illusion was discovered by Diana Deutsch in 1973 [reference]. This is where a passage of two series of notes are played simultaneously into the left and right channels on stereo headphones. One side alternates between melody and harmony, while the other alternates between harmony and melody. When played, the series of unconnected notes seem to combine into a single melody line. Deutsch found that right-handed listeners tend to perceive the melody in the right ear, and similarly in the left ear for left-handed listeners. The sub-patch aims to further investigate if the harmonic relationships between the upper and lower lines of the passage, or the volume of each channel, changes the effectiveness of the scale illusion.

Auditory streaming, coined by Albert Bregman in 1990 [reference], relates to how the brain organises complex auditory components into their own distinct "streams," based on pitch (simultaneous grouping), timing (sequential grouping), or spatial location. The pitch and timing aspects phenomenon can be investigated in a melodic context using the galloping rhythm [reference], where an ABA pattern of alternating high and low tones can either be perceived as one stream (a 3-note melody) at large pitch intervals and/or slow speeds, but breaks down into two streams (an upper part at half the rate as the lower part) at smaller pitch intervals and/or fast speeds. To add to this, the sub-patch also investigates whether the bass note being constant or changing has any effect on auditory streaming.
### Design and Implementation
Both illusions' sub-patch use the "LofiPiano" abstraction used in the random sequencer module. This means the timbre of the illusions can be varied, from the simplest sound a sin wave, or adding more harmonics for a harmonically richer sound. 

For the scale illusion, I used a "qlist" approach to have three pre-set examples for the user to test. When switching between options in the radio, a different text file is loaded, and is then played whenever the play button is pressed. Each text file sends a set of two midi values to two instances of the "LofiPiano," with each channel getting the alternating harmony and melody. The three text files include: two with the same melody but different harmonies (contrary and parallel motion), and one with a contrary motion chromatic scale. A custom "panner" abstraction also helped in panning the audio left and right, which allowed the fading out of either side, to test if the volume of each channel mattered.  

The galloping rhythm needed to loop for however long the user wanted, so a similar sequencer method as the drum machine, which sends midi messages in an "ABA" pattern to a "LofiPiano" abstraction. Adding an integer value to the "B" part of the pattern allows the interval between the two notes to be varied, and a value in beats per minute can be sent into the "counter" sub-patch, which allows the sequencer to change speeds. One setting is activates a 4-wide sequencer, which has a constant bass note, and another setting activates a 16-wide sequencer, which has been set to have a changing bass note.  
### Evaluation of Effectiveness
Overall, the implementation was adequate. Both sub-patches were able to demonstrate the basic conditions and variables for the phenomena to be demonstrated, as well as implementing a few more variables that could push its perception to the limits. However, due to the lack of space, more parameters for both phenomena that were planned to be added weren't able to. For example, the decay of the "LofiPiano" patch was planned to be varied, to see if note duration had affected the perception of the illusion. Or for the galloping rhythm, the second "A" part of the pattern was planned to also be varied while still being lower than the "B" part, to see if this affected the illusion. Unfortunately, this didn't fit in the given space, however it could've introduced more visual clutter.

In terms of usage, the sub-patch for each phenomena has a short description of the phenomena, as well as instructions on how to use it. More importantly though, there are questions added to challenge the user into analysing their perception of the illusions. This proved extremely useful in user tests, as it gave context behind the phenomena, and allowed the user to understand what was being played, and how to interpret the changes in variables.
### Analysis of the Patch Output Audio
As seen in Figure, the spectrogram of both channels using a pure sin wave clearly show each side alternating between melody and harmony. When looking at the combined version of the two passages, it's clear there is a melody and harmony line. However, it appears the audio for the right channel appears quieter, despite the settings for both channels being the same.

Figure shows the spectrogram and waveform plot of a galloping rhythm that gradually speeds up. Even visually the phenomena holds, as at slow speeds the "ABA" rhythm is clearly it's own "object", but starts to blur together at faster speeds. However from the waveform plot, it seems the sound is overall getting louder. This could be from the midi inputs overlapping with each other when the BPM changes, but this wouldn't explain the linear increase.
## Conclusion
> [!uninotes]
> Refer to briefing and summarise your response; overall evaluation of exercise including future work ideas

Overall, the Mosse multi-synth successfully educates and demonstrates examples of a broad-range synthesiser techniques, as well as demonstrations of two psychoacoustic phenomena with multiple variables to adjust, and push the limits of auditory perception. Upon that, the GEM visuals are unique and well-integrated with the characteristics of each synthesiser. The neat UI and well-documented sub-patches allows easy use for a sixth form student with any amount of experience. The seamless merging of all these aspects demonstrate how effective this product could be in a music technology classroom.

Looking to the future, the modular design of the user interface, it would be easy to implement more instruments such as more sound design of natural sounds, or simulating real instruments using physical modelling. The expanding of the aforementioned psychoacoustic phenomena could allow for more insights in how they work as well.