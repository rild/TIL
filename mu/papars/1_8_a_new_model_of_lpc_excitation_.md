A new model of LPC excitation for producing natural-sounding speech at low bit rates

the excitation for LPC

Linear Predictive Coding

> Linear predictive coding (LPC) is a tool used mostly in audio signal processing and speech processing for representing the spectral envelope of a digital signal of speech in compressed form, using the information of a linear predictive model.[1] It is one of the most powerful speech analysis techniques, and one of the most useful methods for encoding good quality speech at a low bit rate and provides extremely accurate estimates of speech parameters. [wiki](https://en.wikipedia.org/wiki/Linear_predictive_coding)

# Abstract
the excitation for LPC speech synthesis usually consists of two separate signals
- a delta-function plus once every pitch period for voiced speech and white noise for unvoiced speech

the speech segment classification
voiced and unvoiced categories

a rigid idealization of the vocal excitation
is often **responsible for
the unnatural quality associated with synthesized speech**

this paper describes
a new approach to
the excitation problem

doesn't require a priori knowledge of
either the voiced-unvoiced decision
or the pitch period

LPC filter

a non-iterative analysis-by-synthesis procedure

minimizes a perceptual-distance metric
this represents
(subjectively-important) differences between
the waveforms of the original and
the synthetic speech signals

distance metric

differential sensitivity of the human ear to errors
- the formant
- inter-formant regions
of the speech spectrum

# Conclusions
developing a new model of LPC excitation

multi-plus excitation signal

- locations
- amplitudes
of the pulses in the multi-pulse excitation

analysis-by-synthesis procedure

the difficult problems are eliminated
- voiced-unvoiced decision
- pitch analysis

# Introduction

synthesis of natural-sounding speech  
at low bit rate

speech coding methods
- waveform coders
  - mimic the speech waveform
  - high quality
  - only at bit rate above about 16 kbits/sec
- vocoders
  - synthesize speech using a parametric model of speech production
  - efficient at reducing the bit rate
  - lower speech quality
  - lower speech intelligibility


pulse code modulation systems
generalizations

low bit rates speech production

<img src="https://gyazo.com/14c9ba2c6c1dbd64ad7bd40945ab2283.png" />

two basic functions

first,
linear filter
- vocal tract
- spectral shaping of the vocal source

second,
excitation to the linear filter

the model assumes
- speech signal can be classified
  - classified into　one of two classes, voice and unvoiced
- the pitch period of the voiced speech segment is known

quasi-periodic pulse train

- voiced speech
  - quasi-periodic pulse train
  - delta functions
  - pitch period intervals
- unvoiced speech
  - excitation
  - white noise

idealized model of speech production

difficult to produce high-quality speech
even at high bit rates

only way at present
at bit rates below about 4 kbits/sec

What is the problem of this model
central problem
- highly inflexible way
  - excitation

an alternate way of representing the spectral information
