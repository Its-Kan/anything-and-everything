**Year**: [[Year 2]]
**Subject**: [[Acoustics and Studio Recording]]

---

Ultimately, we will be writing reports about audio signals. If we have an audio signal, we should listen to it to understand it, but we also need analysis tools to identify parts of the signal. We need to learn methods to focus in on features such as time and frequency of the signal we're focusing on.
# One Sine Wave
The bane of our existence as Music Tech students. This is the most simple, pure audio we can work with. This is a vibration at a single frequency. This graph is familiar to us, we can work out the period, frequency, etc, to get a empirical way to describe what this sounds like.



Looking at this graph, we see Amplitude against Time. This is what we call a **[[time domain]]**. However, this doesn't tell us anything about the frequency without calculation. In order to do this, we can apply the **[[04 Uni Notes/Dictionary/fourier transform]]** this graph, to obtain a **[[04 Uni Notes/Dictionary/frequency domain]]**, which is a Normalised Amplitude against Frequency graph, which shows us what frequencies are present in a signal. To go from a Frequency Domain to Time Domain , we can apply the inverse  **[[04 Uni Notes/Dictionary/fourier transform]]**. 

> [!Note]
> The specifics of how to do a **[[04 Uni Notes/Dictionary/fourier transform]]** will be covered in the [[Mathematics, Signals & Systems]] module. In here, it's purely the method to convert a Time Domain into a Frequency Domain, and vice versa with an inverse Fourier Transform.


And this is what a **[[04 Uni Notes/Dictionary/frequency domain]]** looks like for the 440Hz signal.



Of course, this shows there is one 440Hz frequency, and is (relative to... nothing) the only, loudest signal.

> [!NOTE]
> Near the bottom of the graph, it appears there is a range of frequencies. This is a real world example, which means we aren't going to get a perfectly pure sine wave. If we were to limit our amplitude to just -30dB, then it would look like a perfect 440Hz frequency.
> 
# Two Sine Waves
Ok, let's introduce a second sine wave. We'll add a sine wave three times the frequency (1320Hz), but 1/3 of the amplitude. In the Frequency Domain , we will just see another peak, 1/3 of the height, at 1320Hz. 
## Sum
This is when we play them both at the same time. Their waveforms will interfere with each other, and we get a new waveform in our Time Domain. 

	We chose a sine wave three times the frequency, as it's a harmonic of the fundamental frequency. If we keep adding odd numbered harmonics, with amplitudes that are the inverse of the harmonic number, we will eventually get a square wave.
## Sequence
This is where we play the two waves one after the other. We have to zoom out to see both waves in full.

	The Frequency Domains looks similar on both, but not the exact same. The sequence plot has a wider range of frequencies. This is because there is more variation over time, as the signal changes over time. The longer the 

Ok cool, but we can't really see how it changes over time. Just looking at the Frequency Domains, we know what frequencies are present in both signals, but not what happens over time. Same argument for the Time Domains, we can see the amplitudes and general shapes of the waveforms, but not what frequencies. If only we can combine both of these approaches...

# Spectrograms
## Sine Waves

What we've been doing so far is taking the whole signal, and applying the Fourier Transform to it. With a **[[spectrogram]]**, we split our signal into small chunks called frames (which we can change the size of, or set an overlap), and then apply the Fourier Transform on that frame. We get a Frequency Domain of that frame. We can plot frequency on the y-axis, and then the magnitude in a 3rd dimension, which we will represent with colour. Keep doing that for every frame going down time, and we get this for a 440Hz sine wave:



Now, we can see Frequency and Magnitude over Time. Nice! This also gives us an easier way to relate what we see on the graph, to what we actually hear. Let's see what it looks like for the Sum and Sequence graphs now:



	It's harder to see the difference amplitudes with the two sine waves. However, you can slightly see the 1320Hz band is less bright than the 440Hz band.



## Musical Sounds

We've just been looking at sine waves, which are boring. Let's look at a waveform from an actual instrument (a synth).
### Synth



As you know with synth design, we can analyse the waveform by listening to it:
- There's an amplitude envelope. There's a very short attack, which decays out.
- There's a filter envelope too. It starts very sharp, but a low pass filter filters out all the high end.

Can we see this in the spectrogram?



Yes we can! 
- At the start, there are a lot of frequencies at the start, but they die off over time, leaving the fundamental frequency at the end
- The magnitude also seems to die off over time, as the colour gets darker over time.

### Music

This is Lost at Birth by Public Enemy (1991).



We can hear:
- Low, heavy kick drums
- A punchy snare
- Ride cymbals
- Descending synth line

From the Time Domain, we can see: 
- some snappy percussive spikes, so there's likely a drum 
But we can't really gather much else just from this.



From the Spectrogram, we can see:
- a descending frequency below 4000Hz
- some quick spikes covering multiple frequencies, likely percussive hits
- strong, loud kick pattern below 2000Hz 



### Sample

That descending synth line is actually sampled from a guitar in Living Wreck's Deep Purple (1971). 



We can't see that similarity purely in the waveform:



But we can see that same descending frequency pattern in the spectrogram:



This proves another use for spectrograms, as it makes it easier to compare the similarities between two different signals. 