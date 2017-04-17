Trajectory training considering global variance
for speech synthesis
based on neural networks

Abstract
this paper proposes a new training method of DNNs
for statistical parametric speech synthesis

acoustic models that represent mapping functions from linguistic features to acoustic features in statistical parametric speech synthesis

TTS

There are problems to be solved
in conventional DNN-based speech synthesis
- the inconsistency between the training and sysnthesis criteria
- the over-smoothing of the generated parameter trajectories

> Experimental results show that
the proposed method outperforms
the conventional method in the naturalness of synthesized speech

# Introduction
acoustic models
- in statistical parametric speech synthesis
  - relation between acoustic features and linguistic features

Hidden Markov models HMMs
have been widely used as acoustic models


- acoustic features
- duration of speech

synthesized speech sounds muffled

compare with natural speech

motivated by the success of DNNs in speech recognition


A single DNN

trained to represent the mapping function
from linguistic features
to acoustic features

HMMs

DNN-based speech synthesis shows the potential to produce more naturally-sounding synthesized speech

this paper focuses on two problems in DNN-based speech synthesis
- inconsistency between the training and synthesis criteria
- over-smoothing of the generated parameter trajectories
  - muffled ?
