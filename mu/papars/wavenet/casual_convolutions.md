# 概論
- Casual Convolutions がわからなかったので調べた
  - WaveNet のまとめを読んでいて 「Delated Casual Convolutions」 とあった部分がわからなかった

# What are casual convolutions
[Quora](https://www.quora.com/What-are-causal-convolutions)

- `casual` は信号処理に由来する
- 線形フィルタの特定の形式
- 線形フィルタと畳み込みは同じ意味
  - Linear filters and convolutions are the same
- `casual` が意味するところはフィルタが未来の入力に依存しないということ
  - the filter output does not depend on future inputs

> in WaveNet とかあったことにここで気がつく

- WaveNet では, NNが同じ時刻 t に出力した, 現在の音響強度 (信号強度？) は t 以前のデータにのみ依存する
- ネットワークが新しいデータの生成に使われる場合, その時点でまだ生成していないデータを使うことはない

During training it could, but then the network could not be used to generate new data

- 学習の際には可能だが, 生成の時にはそれはできない

> ここの訳が不安
