# Foundations for speech processing

## Signal
The first step in digital signal processing is to get the signal into digital form. 

- This involves converting an analogue (continuous) value into a digital (discrete) one. Discretisation in time is called sampling 
- and discretisation in amplitude is called quantisation.

### The Nyquist frequency

The sample frequency is the number of times per second we record the value of the waveform.
```
We can only represent frequencies up to half the sampling frequency. This is called Nyquist frequency.

This means to caputure the frequencies up to 8HZ we must sample at (a mininum of ) 16 HZ
```
In addition to the limitations of sampling, storing each sample of the waveform as a binary number means that there is also limited precision in the way we represent amplitude
```
Most common bit depth is 16 bits

2^16= 65536
```


### Aliasing
If we don't remove all energy above the Nyquist frequency, we would get aliasing which results in artefacts in the resulting digital
signal. 

### short-term analysis, frames and windowing
The rectangular window can create artefacts because of the abrupt of starting and stoping of the signal.

There are various better types of windows which smooth the edges.
```
hamming
```

```
short-term analysis          # short region of speech
frame                        # one at a time
```


## speech processing

```
sound is a pressure wave that travel through medium such as air
```
- We can plot the signal in frequency domain - we call that the **spectrum**
- It is often more useful to investigate the sound in the frequency domain, rather than, the time domain
- Repeating pattern
- A prism splits light into its component colours

```
Fourier principle tells us that any periodic signal can be decomposed into a sum of simple signals
```

- Spectrum of a voiced sound where x represents the frequency and the y axis represent magnitude

Two distinct components

- overall shape (spectral envelope)
- spectral detail

Resonance system
- some periodic sound source generate pressure waves
- Resonance will occur if reflected pressure waves are "in step" with new waves produced by the sound source, "in step" waves add up and 
reinforce one another, amplitude builds up.
- filters: magnitude with full frequencies to detect the resonant frequency.

## Speech signal 
- vocal folds
- speech production need sound source with energy
- speech production apparatus
- filter model

## Speech sythesis - text processing
```
Definition: a text-to-speech system must be
- able to read any text
- intelligible
- natural sounding
```






