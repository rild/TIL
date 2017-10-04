Quasi-Recurrent Neural Networks

連続データのモデル化に使用する RNN はそれぞれのタイムステップの独立性から計算時間が長くなっていた.
RNN に対して畳み込みレイヤを使用して高速化を図る.

畳み込みを使って RNN の高速化を図るのは WaveNet の Casual CNN に似てるのかな.

`a minimalist recurrent pooling function`

stacked Recurrent layer

LSTM などの既存の RNN の限界によってできないタスクの例として

- character-level machine translation

が出ていた.
塊ごとに訳すのではなく, 文字ごとに解釈して訳す...みたいな？


---

http://qiita.com/icoxfog417/items/d77912e10a7c60ae680e

> 並列処理に弱い

> 隠れ層の値の意味がわかりにくくなる

*新規* と呼べるかは微妙だが, 伝搬の構成は先行研究とは異なる

> - RNNではなく、CNNを連続的なデータ(文章など)に対して適用する
これにより並列計算が可能になります

>- 重みを使わず伝搬することで、隠れ層の中の各要素を、他要素からの影響から独立した状態でキープする
  - これにより隠れ層の分析(どの場所が活性しているかなど)が行いやすくなる
