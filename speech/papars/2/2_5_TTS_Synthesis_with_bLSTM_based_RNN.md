TTS Synthesis with Bidirectional LSTM based Recurrent Neural Networks

BLSTM-RNN
Bidirectional Long Short Term Memory

Feed-forward
DNN
(better than context-dependent HMM)
in TTS

the long time span contextual effect
still not easy

the dynamic features

RNN-BLSTM セルに、任意の二つの瞬間の相関と共起を捉える仕組みを実装した？

学習済み HMM を使った合成では, 発音ユニット同士の結合部で不自然さが残る
overlay smoothed parameter trajectories も不十分である

sound not as lively as desired

DNN の音声認識分野における成功に影響されて,
vocoder-based speech synthesis のパフォーマンスを改善する試みが見られる

DNN based approach, which models the relationship between
- input texts
- their corresponding acoustic features

DNN-based approach > HMM-based approach

the training aspects
- activation functions
- weights initialization in "pre-training"

Vector Space Model, VSM
based binary or continuous features
as input features

Deep Belief Network, DBN
with stacked,
restricted Boltzmann machines, RBMs

can

model the structure in the input data as generative "pre-training"

find a region of the weight-space

that can reduce over-fitting
for the discriminative "fine-tuning" phase in speech recognition

RBM を使った合成音声も成果をあげている
