輪講発表用のメモ

TACOTRON: TOWARDS END-TO-END SPEECH SYNTHESIS
のメモ
Submitted to Interspeech 2017

# 雑記

複雑な TTS の生成過程を単純化して合成精度の向上を目指す
HMM-based 音声合成では, 多くのパラメータを扱う必要があり, 専門性が高く, システムの構築が大変.

それぞれの要素がバラバラに調整されるため, 各要素のエラーの修正が容易ではない.

これらが原因で, 新しい合成システムの構築には多くの工学的努力が必要になる.

statistical parametric TTS

> HMM-based synthesis is a synthesis method based on hidden Markov models, also called Statistical Parametric Synthesis. [wiki](https://en.wikipedia.org/wiki/Speech_synthesis)

 - linguistic features
 - a duration model
 - an acoustic feature prediction model
 - a complex signal-processing-based vocoder

substantial engineering efforts

---
many advantages

an integrated end-to-end TTS system that can be trained on <text, audio> pairs

First, such a system alleviates the need for laborious feature engineering, which may involve heuristics and brittle design choices.

試行錯誤が伴う, 不安定な特徴調整を減らすことができる

Second, it more easily allows for rich conditioning on various attributes, such as speaker or language, or high-level features like sentiment. This is because conditioning can occur at the very beginning of the model rather than only on certain components.

感情や話者, 言語特性などの要素を音声合成システムに組み込みやすくなる
- これらは, 特定の要素ではなく, システム全体に影響を与えると考えられるため

Similarly, adaptation to new data might also be easier.

新しいデータへの対応が容易になる

Finally, a single model is likely to be more robust than a multi-stage model where each component’s errors can compound.

要素を簡略化することで, ロバスト性が高くなる

>  Robustness can be defined as "the ability of a system to resist change without adapting its initial stable configuration"

These advantages imply that an end-to-end model could allow us to train on huge amounts of rich, expressive yet often noisy data found in the real world.

現実世界にある, 多様で表現豊かな音声合成モデルを実装できるようになる

---
a large-scale inverse problem

Text は高度に情報圧縮された媒体であり, それを音響信号に解凍する必要がある

同じ文は何通りにも読まれ得るため, end-to-end な学習モデルは特に困難であった
- ある文字入力に対して, 多くの信号レベルで異なる出力がある

- end-to-end speech recognition (Chan et al., 2016)
- machine translation (Wu et al., 2016)

TTS では, 出力が連続値かつ, 入力値よりも非常に大きな連続値となる

これが, 音声合成において prediction errors の原因となる

---

本論文では "Tacotron" を提案している

end-to-end な TTS 生成モデル
seq2seq (Sutskever et al., 2014)
attention paradigm (Bahdanau et al., 2014)

に基づいている

入力: 文字列 characters
出力: 音声波形のスペクトログラム raw spectrogram

seq2seq モデルに, 幾らかの改善を施している

random initialization により, ゼロから from scratch 完璧に訓練することができる

phonome-level alignment を必要としない
音素レベルの関連付け

このため, (既存のモデルより？)多くの音響情報を組み込むモデルにスケールしやすい
記述言語を使う with transcripts

MOS スコアで 平均 3.82 を記録する
parametric system より naturalness という観点で, 大幅に性能が上回った状態で, である

---

関連研究

WaveNet (van den Oord et al., 2016)
DeepVoice (Arik et al., 2017)

Wang et al. (2016)
これにはアクセスできなかった
今調べたらなんか DL できた...あれ？

事前に訓練された HMM ベースの aligner
vocoder parameters を予測するため, vocoder を必要とする
このため, 訓練には phoneme を用いる必要があり, 生成結果にはいくらかの制限があるようであった

Char2Wav (Sotelo et al., 2017)
は Tacotron とは異なる, end-to-end な音声生成モデルである
これも, vocoder parameters を予測している
- SampleRNN neural vocoder (Mehri et al., 2016) を使用しているため
この seq2seq + SampleRNN モデルでは, 事前訓練が必要になるが, Tacotron ではそれが必要ない

元の seq2seq パラダイムに対して, いくらかの重要な変更を加えた
- 元のモデルでは, 文字レベルの入力ではうまく動作しなかった

demos
https://google.github.io/tacotron/
