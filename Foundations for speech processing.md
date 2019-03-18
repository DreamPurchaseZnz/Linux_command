# Foundations for speech processing

## Signal
The first step in digital signal processing is to get the signal into digital form. 

- This involves converting an analogue (continuous) value into a digital (discrete) one. Discretisation in time is called sampling 
- and discretisation in amplitude is called quantisation.

### The Nyquist frequency

The sample frequency is the number of times per second we record the value of the waveform.
```
We can only represent frequencies up to half the sampling frequency. This is called Nyquist frequency.
```
In addition to the limitations of sampling, storing each sample of the waveform as a binary number means that there is also limited precision in the way we represent amplitude

### Aliasing
If we don't remove all energy above the Nyquist frequency, we would get aliasing which results in artefacts in the resulting digital
signal. 

