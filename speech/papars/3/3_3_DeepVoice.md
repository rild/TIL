Deep Voice: Real-time Neural Text-to-Speech

[Deep Voice: Real-Time Neural Text-to-Speech for Production](http://research.baidu.com/deep-voice-production-quality-text-speech-system-constructed-entirely-deep-neural-networks/)


## Abstract
Deep Voice lays the groundwork

- Test current Deep Learning approaches
  - for truly end-to-end neural speech synthesis

five major building blocks
- a segmentation model for locating phoneme boundaries
  - `a novel way` of performing phoneme boundary detection
- a grapheme-to-phoneme conversion model
- a phoneme duration prediction model
- a fundamental frequency prediction model
- an audio synthesis model
  - a variant of `WaveNet` that requires fewer parameters (and trains faster than the original)
  - 400x speedups over existing implementations

DNN
`a novel way` of performing phoneme boundary detection
with deep neural networks using connectionist temporal classification (CTC) loss


## Introduction
Modern TTS systems features
- complex
- multi-stage processing pipelines
  - each of which may rely on hand-engineered features and heuristics

> まさにこれ

an entirely new dataset that contains `solely audio` and `unaligned textual transcriptions` and generating relatively high quality speech.


However, WaveNet inference poses a daunting computational problem

> daunting 笑

## Conclusion
Result of Demonstration

- building a fully neural system

Unnecessary

trainable without any human involvement

therefore

- dramatically simplifying the process of creating TTS systems

Inference performance can be further improved
