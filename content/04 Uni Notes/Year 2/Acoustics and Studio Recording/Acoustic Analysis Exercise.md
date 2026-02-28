# Contents
```table-of-contents
title: 
style: nestedList # TOC style (nestedList|nestedOrderedList|inlineFirstLevel)
minLevel: 2 # Include headings from the specified level
maxLevel: 100 # Include headings up to the specified level
includeLinks: true # Make headings clickable
hideWhenEmpty: false # Hide TOC if no headings are found
debugInConsole: false # Print debug info in Obsidian console
```
--- 
## 1. Introduction
This report aims to present an acoustic analysis of a space, using impulse responses (IRs) and  auralisation. This is achieved by convolving an anechoic recording with an IR, to generate an auralisation. Using MATLAB[^1] for analysis, this report will explore the acoustic characteristics of the anechoic recording, IR space and resulting auralisation. 
## 2. Background
### 2.1 Room Acoustics
In any room, the perceived sound is influenced by how the sound waves interact with the boundaries of said room, whose characteristics, such as room dimensions, location or surface material, ultimately dictate the quality or timbre of the sound itself. We can investigate how sound behaves in a specific environment using room impulse responses (RIRs), by modelling sound as a discrete impulse. By capturing an RIR of a space, were able to apply its results to an anechoic recording, i.e. one without reverb, using a convolution, to simulate what said recording could sound like in a specific environment, called an auralisation.
### 2.2 RIRs
An IR of a space captures the acoustic characteristics of a room by its reaction to being played in said room. It can capture what happens with the sound waves in a room, which can be broken down into three segments:
- The direct sound, which arrives at the listener "uncontaminated" and doesn't interact with any boundaries 
- Early reflections which can be heard as echoes from the first initial reflections
- Reverberation, which accounts for all the other boundary interactions that happen

Instead of using archaic methods such as popping a balloon or clapping which have uncontrollable variables, a modern approach to creating an IR, and the method that has been used in this report, would be using a "time reversal mirror" technique. We can record an exponential sine sweep in the room, and then convolve that with the time reversed version of the input signal, effectively deconvolving the signal. The resulting sound wave is an IR of the space. 
### 2.3 Schroeder Curves
We can quantify the acoustic parameters of an IR using Schroeder curves, by first squaring the IR, convert it to decibels (dB), and then perform a reverse integration to get the measurement of the cumulative energy. Using this to analyse this IR gives us the more specific parameters that control how sound behaves in an environment, such as:
- reverberation time (RT60) which extrapolates a portion of the Schroeder curve to estimate the -60dB point,
- early decay time (EDT) which is the perceptual relevance of the early stages of the IR from 0 and -10dB,
- clarity (C50), which is the ratio of the early to late energy in dB and/or 
- definition (D50), which is the ratio of the early to total sound energy ratio. 
## 3. Details of the IR recording Space
The IR was recorded at Rawcliffe Lake, York. The location chosen was a jagged landing that overlooked the lake, blocked by some concrete blocks (see **Figure 1a**), and behind it was a subtle valley (see **Figure 1b**) with steps to its left and right . The steps, landing and blocks were made of concrete, but most of the valley was natural grass and dirt. An unavoidable consequence to recording outside was the amount of wind present, however this was mitigated by using a wind shield and by taking multiple recordings. 

| Figure 1 - Rawcliffe Lake            |                                         |
| ------------------------------------ | --------------------------------------- |
| ![[Acoustics REPORT Space.png\|230]] | ![[Acoustics REPORT photo 2.png \|230]] |
| **- Figure 1a**                      | **- Figure 1b**                         |
## 4. IR Analysis
### 4.1 Time and Frequency Domain Features
Due to the wind and other external interruptions in the recordings, an average of multiple recordings had to be used to reduce the signal-to-noise ratio, using MATLAB with my own written function called $\text{averageWaveforms.m}$. Using the method described in **Section 2.2**, the averaged waveform is then converted to an IR using the inverse sin sweep, and then convolved with the anechoic recording to get an auralisation in both the time and frequency domains.  
#### 4.1.1 Time Domain 
Looking at the time domain (see **Figure 2**), we can see three distinct peaks in the waveform.

The first peak seems anomalous, since it happens before the direct sound. This could be due to the underlying noise from the wind, or some recording anomalies. The second peak is indeed the direct sound, confirmed by using $\text{distance}=343 \text{ms}^{-1} \times 0.00698413s$, which roughly equals $2.5 \text{m}$, which was consistent with the actual distance from the speaker and microphone. It's not completely clean though, again most likely due to the wind. The third peak seems to be the early reflections, likely from the concrete steps to the side of the speakers which explains the multiple drawn out peaks. The reverberation time seems extremely short too, likely due to both the lack of vertical walls, and the grass and dirt in the valley absorbing most of the later reflections. However, there seems to underlying noise after the early reflections uncharacteristic of reverberation. This again, is likely due to the wind. 

| figure 2 - Time domain waveform           |
| ----------------------------------------- |
| ![[Pasted image 20250203055339.png\|500]] |

#### 4.1.2 Frequency Domain 
Looking at the frequency domain (see Figure 3), we can see also three distinct regions in the spectrum, however the entire spectrum seems to exhibit comb filtering, from the slight differences in arrival times from the concrete steps and landing. In the low frequencies, room modes can explain the resonant peaks and 

Below 100 Hz seems to be attenuated, likely from the constant wind noise. The wind was made to cover a consistent range of frequencies when the multiple recordings were averaged into one file, reducing the different frequencies it could cover due to wind speed or direction. The mid range frequencies between 200Hz and 2kHz seems to be fairly consistent. There are noticeable attenuations around 3kHz and 8kHz. As these are mid to high frequencies, it's unlikely these are due to room modes, so it's likely either the concrete or dirt specifically absorb these frequencies more than others.

| figure 3 - Frequency domain Spectrum |
| ------------------------------------ |
| ![[Acoustics REPORT freq.png\|500]]  |
### 4.2 Calculation of Room Acoustic Parameters
The process described in **Section 2.3** allows us to generate a Schroeder curve for each frequency band (see Appendix B), using the Acoustics Parameter Toolbox (APT). We're able to generate values for ISO 3382[^3] standard parameters: $D50$, $D80$, $C50$, $C80$, $CT$, $EDT$, $T20$, $T30$ and $T40$ using the Schroeder curve. The results (see Appendix C) have been summarised in **Table 1**.

| Table 1 -          | iso          | 3382         |              |              |                   |                    |                    |                    |                    |
| ------------------ | ------------ | ------------ | ------------ | ------------ | ----------------- | ------------------ | ------------------ | ------------------ | ------------------ |
| **Frequency Band** | **D50 (\%)** | **D80 (\%)** | **C50 (dB)** | **C80 (dB)** | **CT (Time (s))** | **EDT (Time (s))** | **T20 (Time (s))** | **T30 (Time (s))** | **T40 (Time (s))** |
| 62.5               | 95.67        | 99.65        | 13.44        | 24.53        | 0.02              | 0.23               | 0.15               | 0.15               | 0.15               |
| 125                | 97.36        | 97.63        | 15.67        | 16.15        | 0.04              | 0.07               | 16.96              | 9.38               | 8.58               |
| 250                | 99.85        | 99.97        | 28.12        | 35.55        | 0.01              | 0.05               | 0.04               | 0.25               | 9.37               |
| 500                | 99.94        | 99.97        | 32.13        | 35.52        | 0.00              | 0.03               | 0.06               | 0.16               | 4.24               |
| 1k                 | 99.95        | 99.96        | 33.18        | 34.09        | 0.00              | 0.02               | 0.03               | 0.35               | 10.15              |
| 2k                 | 99.98        | 99.99        | 36.71        | 39.32        | 0.00              | 0.01               | 0.05               | 0.07               | 0.29               |
| 4k                 | 99.98        | 99.99        | 36.79        | 41.00        | 0.00              | 0.00               | 0.05               | 0.06               | 0.26               |
| 8k                 | 99.99        | *100.00*     | 42.53        | 47.65        | 0.00              | 0.00               | 0.03               | 0.05               | 0.12               |
| L                  | 99.97        | 99.99        | 35.86        | 38.57        | 0.00              | 0.00               | 0.05               | 0.11               | 11.77              |
#### 4.2.1 Definition and Clarity
$D50$ and $D80$ measures the ratio of the early sound energy to total sound energy in the first 50 and 80 milliseconds respectively. A higher percentage for this parameter means most of the sound is captured in the first stages of the IR. The definition is consistently above 99%, except slight attenuations at 62.5Hz and 125Hz, which means there is a very quiet reverberation tail. This is 

$C50$ and $C80$ is similar to definition, but measures the ratio of early sound energy to later reverberant energy, using 50ms and 80ms respectively as its midpoint. These two measures use decibels instead, and tend to be used for speech and music respectively. For $C50$, frequencies above 500Hz exceed 30dB, which shows a very dry signal. For $C80$, all the values are consistently higher than those in $C50$, which again signifies a very dry signal. For both, the frequencies below 125Hz have lower clarity, and thus have slightly more reverb. 
#### 4.2.2 CT and EDT
$CT$ (Centre Time) measures the "centre of gravity" of the IR. With 500Hz and up, most of the impulse is instant, signified by 0s in the table, so. However lower frequencies, more notably at 125Hz, there's more energy spread 0.04s into the IR. The overall low values for CT show us that the early reflections are more dominant over the reverberation tails.

$EDT$ (early decay time) measures how long it takes for the early energy to decay by 10dB. Frequencies above 4k practically decay instantly, and therefore no reverberations. The longest EDT follows the pattern of lower frequencies having more reverb with 62.5Hz having an EDT of 0.23s. 
#### 4.2.3 T20, T30 and T40
$T20$, $T30$ and $T40$ describe how long it takes for the reverberation time to decay, from 0db to 20db, 30db, and 40db respectively. This section of parameters show the longest reverb tail start at 125Hz. However there seems to be an anomalous result for $T40$ at 1kHz, which could be due to the absorption coefficient of concrete favouring this frequency band. For all parameters, the higher frequencies upwards of 2k seem to have extremely short reverb tails. 
## 5. Anechoic Recording
The anechoic recording was done in the University of York's anechoic chamber to capture an instrument without reverb, using a C414 (see Appendix 2). I recorded a ukulele playing the chords of Stromae's "ave cesaria[^1]". The chords were played with a mix of long sustained strums, short staccato strums as well as more transient muted strums, which gave a range of signals for the auralisation.

Looking at the frequency spectrum, there is a large dynamic range in terms of amplitude. The frequency spectrum also has some insights. The 200Hz to 1kHz range is the most prominent, which is likely the melodic component of the ukulele's sound. There are some subtle noise across the entire spectrum, likely the subtle mechanical noise from the heater and laptop that were in the anechoic chamber.

| figure 3 - Anechoic: top TD, middle FD, bottom spectrogram |
| ---------------------------------------------------------- |
| ![[Pasted image 20250203054451.png]]                       |

## 6. Auralisation Critical Evaluation
Looking at the room acoustic parameters in **Section 4.2**, it appears most of the reverberant effects of the IR are found in the lower frequencies of the IR, which is somewhat evident in the auralisation, however not to the extent we could see if I chose a lower instrument such as a bass guitar. 

Listening to the auralisation, there seems to be very subtle reverberation or echo under the ukulele, however it largely sounds similar to the anechoic recording, which is consistent with the parameters of definition and clarity. At the end of the auralisation, there seems to be a continuous reverberation for frequencies under 1kHz, which is consistent with the seemingly anomalous $T40$ results. The lack of reverberation in the higher frequencies (seen in the high definition and clarity values) is also demonstrated, with little to no difference to the anechoic recording (see **Figure 4**). 

| Figure 4 - Auralisation spectrogram: top td, bottom fd |
| ------------------------------------------------------ |
| ![[Pasted image 20250203084812.png\|500]]              |

## 7. Conclusion
This report has introduced room acoustics, IRs, and methods to analyse these IRs and resulting auralisations. These overviews are applied to a space - Rawcliffe Lake - to generate an IR, and then further analysed by calculating its acoustic parameters. These findings are then applied by convolving the IR with an anechoic recordings to further investigate its reverberation effects. 
## 8. Appendix

| APPENDIX A - C414 in an Anechoic Chamber       |
| ---------------------------------------------- |
| ![[Acoustics REPORT anechoic recording.png\|]] |

| Appendix B - 62.5Hz Schroeder curve        |
| ------------------------------------------ |
| ![[Acoustic Analysis Exercise schora.png]] |

| APPENDIX C - APT Results                    |
| ------------------------------------------- |
| ![[Acoustic Analysis Exercise toolbox.png]] |



## 9. References
[^1]: MathWorks, "MATLAB", Mathworks.com [Online]. Available: https://uk.mathworks.com/products/matlab.html [accessed Jan. 21,2025]
[^2]: Stromae, “Stromae - ave cesaria (Official Audio),” YouTube.com [Online], Sep. 13, 2013. Available: https://www.youtube.com/watch?v=8kmzvE6su5I [accessed Jan. 21, 2025]. 
[^3]: ISO, "ISO 3382", Iso.org [Online]. Available: https://www.iso.org/standard/77437.html [accessed Jan. 21, 2025]
