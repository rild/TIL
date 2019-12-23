Which I Remark

2017.4.13 Thu

1 - 1

WAVENET: A GENERATIVE MODEL FOR RAW AUDIO

# ABSTRUCT
wavenet, a deep neural network(DNN) for generating raw audio waveforms.

<font size=1>DNN について読んだ方がいい論文はなんだろう</font>

*probabilistic*

<img width=350 src="https://gyazo.com/d2662889f59acdbc7eeb66a131e57d52.png" />

*確率的*

*autoregressive*

<img width=350 src="https://gyazo.com/c6a84bc0b41b5daeaeb12dea16cac9aa.png" />

*自己回帰的*

predictive distribution for each audio sample

the sample is conditioned on all previous one

*predictive*

nonetheless

１秒あたりのサンプル数: ten thousands, 1万

<font size=1>なぜこのサンプル数なのか</font>



> it yields state-of-the-art performance

*state-of-the-art*

最先端

Human listeners rate that as significantly more natural sounding than the best parametric and concatenative systems
(English and Mandarin)

> a single WaveNet can capture the characteristics of many different speakers with equal fidelity, and can switch between them by conditioning on the speaker identity.

音楽にも応用できる

その場合は音楽用に学習したモデルが必要となる

*discriminative model*

phoneme 音素


識別モデル


fidelity 本物そっくり

# CONCLUSION

a deep generative model of audio data

that operates directly at the waveform level.

*[causal filter](https://en.wikipedia.org/wiki/Causal_filter)*

> In signal processing, a causal filter is a linear and time-invariant causal system. [by wiki](https://en.wikipedia.org/wiki/Causal_filter)

因果性フィルタ（デジタル信号処理）

[デジタル信号処理(wiki)](https://ja.wikipedia.org/wiki/%E3%83%87%E3%82%B8%E3%82%BF%E3%83%AB%E4%BF%A1%E5%8F%B7%E5%87%A6%E7%90%86)

> デジタル信号処理（デジタルしんごうしょり、Digital Signal Processing、DSPと略されることもある）とは、デジタル化された信号すなわちデジタル信号の信号処理のことである。分野としては、これとアナログ信号処理は信号処理の一部である。この分野の大きな研究・応用領域に音響信号処理、デジタル画像処理、音声処理の三つがある。

> 目的は実世界の連続的なアナログ信号を計測し、選別することである。その第一段階は一般にアナログ-デジタル変換回路を使って信号をアナログからデジタルに変換することである。また、最終的な出力は別のアナログ信号であることが多く、そこではデジタル-アナログ変換回路が使用される。

> 処理可能な信号のサンプリングレートを稼ぐ目的に特化したプロセッサを使うことが多い。デジタルシグナルプロセッサという特化型のマイクロプロセッサが使われ、よくDSPと略される。このプロセッサは、典型的な汎用プロセッサに見られる多種多様な機能の内の幾つかを除外し、新たに高速乗算器,積和演算器を搭載している。従って、同程度のトランジスタ個数の汎用プロセッサと比較した場合、条件分岐等の処理では効率が悪化するが、信号を構成するサンプルデータは高効率で処理する事が可能になる。

*dilated*

dilated convolutions 拡張畳み込み

*receptive*

important things to model the long-range temporal dependencies in audio signals

> WaveNet are autoregressive and combine causal filters with dilated convolutions to allow their receptive fields to grow exponentially with depth

音響信号の中で、長い期間の時間依存性に関するモデルについて大切なこと

自己回帰的処理と、拡張畳み込みを使った因果性フィルタの組み合わせ

`認知分野?` が深度にしたがって、指数関数的に増大する

*receptive fields*


> We have shown how WaveNet can be conditioned on other inputs in a global or local way.

|   expressions   |  examples    |
| :------------- | :------------- |
| global way      | speaker identity       |
| local way      | linguistic feature       |


> When applied to TTS, WaveNets produced samples that outperform the current best TTS systems in subjective naturalness.

very promising results when applied to
- music audio modeling
- speech recognition
