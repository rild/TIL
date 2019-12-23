Generation Sequences With Recurrent Neural Networks

LSTM
RNN

- LSTM の能力を測った論文


complex sequences with long-range structure

predicting one data point at a time

- text
  - where the data are discrete
- online handwriting
  - where the data are real-valued

extended to handwriting synthesis
- highly realistic cursive handwriting

- RNN について一般的に
> RNN can be trained for sequence generation
by processing real data sequence
and predicting what comes next

予測が確率的であると予測すると...
novel sequences は
1. ネットワークの出力結果から繰り返しサンプリングを行う
2. 得られたサンプルを次のステップで使用する
ような訓練されたネットワークを使って、生成される

ネットワークが決定的であっても、出力に確率的要素を与えられる？

- RNN はファジー
  - 予測をする上で, 学習データをそのまま抽出する訳ではない
  - 中間表現を使って, より高次の補完を行う

通常の RNN では長期に渡る情報の保持が難しい

common to all conditional generative models
problem
ネットワークによる予測が過去の少数の出力にのみ依存した場合、（そしてその出力はネットワークそのものによる予測によって得られたものの場合）過去の失敗を修正することがほとんどできない

ネットワークの更新が起こりやすくした場合、
学習データの誤りをすぐに反映してしまうようになる

acute with real-valued data

robustness to surprising inputs

LSTM すごいよ、という話
