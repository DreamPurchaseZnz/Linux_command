# Foundations for speech processing
[Speech.zone.cources](http://www.speech.zone/courses/)
[Speech.zone.speech-processing](http://www.speech.zone/courses/speech-processing/)

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

## Speech sythesis -text processing
```
Definition: a text-to-speech system must be
- able to read any text
- intelligible
- natural sounding
```

Most common method in state-of-the-art commercial and research systems

```
CHATR Japan
Festival           UK
```

Text processing breaks the original input text into units suitable for 
further processing

- Tokenisation

the system must recognise abbreviations and then expand them
```
Dr. Livingston vs Livingston Dr
```
The interpretation of numbers is comtext sensitive.

- Finite state methods

## Speech synthesis-pronunciation and prosody

Pronunciation, including letter-to-sound models, 
and predicting prosody. 
All these tasks can be done with Classification And Regression Trees (CARTs).

- from letters to sounds

### part-of-speech (POS)
some words have multiple possible POS categories

### lexicon
The entries have three parts:
- head word
- POS
- Pronunciation


### letter to sound
if lexical lookup fails, we fall back on the letter-to-sound rules

### Post-lexical rules

```
Text -> token -> POS -> lex  -> poslex
```

### Prosody prediction
automatic phrase boundary predition

= break strength (BB, big break)


## speech synthesis- waveform generation

Frond end
```
tokenize                      # individually learned from labelled data
pos tag                       # high accuracy
LTS
Phase break 
Intonation
```

TD-PSOLA (time domain-pitch synchronous overlap and add)

The fundamental frequency (also called the fundamental) of a periodic signal is 
the inverse (reciprocal) of the pitch period length. 
We represent the fundamental frequency as F0 ("F-zero", or "F-sub-zero"). 

### join smoothing
using the LP(linear prediction) to disguise the joins

Since the filter is time-varying, we need to decide how frequently to update its coefficients.

LPC: linear prediction coding

## speech recognition - pattern matching
- frame based analysis of speech
- feature vector
- The ear does more than a simple frequency analysis. It's not just doing something like an FTT


# [Speech synthesis](http://www.speech.zone/courses/speech-synthesis/)


