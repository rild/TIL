from reference
`WaveNet a Generative Model for Raw Audio`

```md

abstract, conclusion

```

to

titled

`VOCAINE THE VOCODER AND APPLICATIONS IN SPEECH SYNTHESIS`

# Main

at least, should I read abstract and conclusion

## ABSTRACT
- vocoders received renewed attention
  - << basic components in speech synthesis applications

- We report
  - Vocaine improves our statistical TTS synthesizers and oour new statistical parametric synthesizer
  - << matched the wuality of our mature production Unit-Selection system with uncompressed waveforms

- Vocaine
 - that features a novel Amplitude Modulated-Frequency Mudulated (AAM-FM) speech model
 - a new way to synthesize non-stationary sinusoids (sin curve) using quadratic phase splines

*spline*

> スプライン 与えられたいくつかの点をなめらかに結ぶ曲線 [weblio](http://ejje.weblio.jp/content/spline)

*quadratic phase splines*

> 二次位相スプライン

# INTRODUCTION

## Vocoder

- a vocoder is a key component of modern speech synthesis applications
 - because it provides a parametrization of the speech waveform
 - amenable to quantization, modification and statistical modeling  

- the commercial interest for vocoders
 - speech coding

- speech coding
 - STC, the Sinusoidal Transform Codec
 - AMBE, Advanced MultiBand Excitation

but (that) was later reduced for about a decode following the dominance of CELP codecs

- many speech waveform models ware proposed during that period
 - for use in voice Transform and voice conversion
 - HNM, the Harmonicplus-Noise Model

- audio processing community
 - Sinusoids-plus-Noise model
 - IRCAM's Super Vocoder Phase

the quest to realistically modify voice quality characteristics

## Renewed interest

- A renewed interest for vocoders came with application of Statistical Parametric Speech Synthesis, SPSS

- Statistical synthesizer require
 - a parametric representation of speech
 - the speech is amenable to statistical modeling

- the two most notable contributions here
 - STRAIGHT
 - AhoCoder which is an STC/HNM variant
- both vocoders are reported to be of similar quality
 - but, STRAIGHT is more widely used by the community as a baseline

- we will henceforth focus on those related to contemporary speech synthesis

## STRAIGHT and AhoCoder

### STRAIGHT
- STRAIGHT synthesis is too slow
 - to be used in practice
 - because it relies on high-order FFT for high-resolution spectral synthesis

- attempts to make it faster
 - replacing FFTs with an log-spectrum filter
 - so with variable lattice filter and mixed-excitation

- Mixed-excitation is a pulse plus colored noise
 - that sounds buzzy sometimes

- STRAIGHT reduces buzziness using an all-pass filter
 - to fuzzify the pulse in higher frequencies
 - an approach that works well in many cases

but alters voicing quality, reduces *brightness ??* and does not produce realistic voices fricatives

### AhoCoder
- Sinusoidal vocoders
 - like STC, HNM and AhoCoder
 - on the other hand do not have an implicit way
 - to deal with intra-harmonic noise and forcefully split the speech spectrum in two parts
 - deterministic and noise

- HNM and AhoCoder have explicit noise models
 - use modulation to incorporate noise into the signal
 - a trick that has also being used successfully in "Combined estimation/- coding of highband spectral envelopes for speech spectrum expan- sion", "Towards flexible speech coding for speech synthesis: an LF+ modulated noise vocoder."

- Band-splitting has the disadvantage that it is biased towards synthesizing noisy higher formants
 - penalize brightness (=clarity?)
 - it is sensitive to voicing decisions
 - frequently suffering from artifacts in unvoiced-voiced transients and onsets

## Vocaine
 - Vocaine was designed to overcome
  - shortcomings of STRAIGHT and
  - HNM with low computational complexity

a *universal vocoder synthesizer*

- a speech waveform renderer
 - can be used to different analysis mothods

## Overview 
- section 2 presents a novel speech model
 - describes the speech signal in a sinal equation as a sum of non-stationary sinusoids and
 - incorporates a coherent noise-modulation model for frication and breathiness
- section 3 presents a phaselocked pitch-synchronous synthesis mechanism
 - allows explicit phases to be set at glottal closure instants
 - successfully deals with transients
- section 4 presents a novel phase interpolation techniques
 - referred to as quadratic phase splines
 - very fast and automatically introduces dithering noise at non-stationary parts pf speech
- section 5 presents a novel super-fast cosine generation procedure
 - significantly lowers computational complexity
- section 6 presents objective and subjective results in Copy-Synthesis and SPSS
