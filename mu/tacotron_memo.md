輪講発表用のメモ

TACOTRON: TOWARDS END-TO-END SPEECH SYNTHESIS
のメモ

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
