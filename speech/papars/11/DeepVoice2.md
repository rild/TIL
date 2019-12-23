- DeepVoice1 に改良を加えた
- DeepVoice1 と Tacotron より性能が改善された
  - higher performance building block によって, `Deep Voice 1` より音質改善された
  - post-processing neural vocoder によって, `Tacotron` より音質改善された

single-speaker neural TTS の話

- multi-speaker speech synthesis について DeepVoice2 と, DeepVoice1 や Tacotoron を比べた

- single neural TTS system: １話者あたり 30 分以下の時間で 数百人ぶんのユニークな声を学習することに成功した
- 話者特徴と音質はほとんど完全な状態

- Tacotoron を複数話者に対応させた
- Tacotoron のモデルは, ハイパーパラメータの値に強く依存していることを確認
- 一部の話者について, attention mechanisms を学習できないことを確認
- 同じタイムステップで学習データを始める必要がある
  - 意味のある attention 曲線や識別可能な音声に収束しにくくなってしまう
- モデルに最大限の品質の合成をさせるためには, チューニングが必須

- DeepVoice2 とは, 音質というより複数話者への対応可能性の観点で比較を行なった
