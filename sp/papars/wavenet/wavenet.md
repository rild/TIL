WaveNet

GitHub implementation

[WaveNet implementations](http://tam5917.hatenablog.com/entry/2016/09/18/131458)


- [ご注文は機械学習ですか？ WaveNet - A Generative Model for Raw Audio [arXiv:1609.03499]](http://musyoku.github.io/2016/09/18/wavenet-a-generative-model-for-raw-audio/)

WaveNet は時間がかかる
サンプリング周波数によるが,
- 44.1 kHz (ナイキスト周波数的な) でサンプリングした音源で学習する場合
  - 1秒あたり90分かかる！？

論文に実装についての記述がない

wav ファイルの形式について
圧縮音源と非圧縮音源

16bit PCM
μ-low algorithm
one-hot vector

> 時系列上の 256 チャンネルに 1*1 px の画像を配置していったらしいけれど, グレースケールということだろうか

サンプリング周波数が学習速度とトレードオフになる

[人工知能の話題でご飯３杯いける 機械学習とか 2016-10-06 WaveNetメモ](http://snowman-88888.hatenablog.com/entry/2016/10/06/052229)
> delated casual convolution で検索したら出てきた
> 受容野が広げられている, とだけ解釈している？

[casual filter](https://en.wikipedia.org/wiki/Causal_filter)
> The word causal indicates that the filter output depends only on past and present inputs.

WaveNet では過去のある時刻までの範囲の全ての信号を入力としてとって, 次の時刻の信号を予測する (RNN 的)
- 次の信号を予測するために過去のデータをどの程度見るか: 受容野

受容野に対して RNN ではなく, CNN で時系列を加味した特徴量を取り出す
- 100 msec の受容野, サンプリング周波数 44.1 kHz の場合, 4410 個の信号が受容野に存在する
  - これが WaveNet の畳み込み層の入力となる？
  - 畳み込みフィルタの幅が 2 のとき, 4410 個の信号をたたみこむには 4409 層必要になる
  - <-> フィルタサイズ (幅？) が 4410 なら 1層ですむ

この問題を解決するために, Dilated Convolution を使う
- 別名: atrous convolution, convolution with holes

<img src="https://gyazo.com/7abc94016bcd5f3bc1b8057adf6b7abf.png" />

これを,

<img src="https://gyazo.com/29bc263a3413b322c5acbece2c4266ba.png"/>

こうする.

- ４層だけで, 受容野が16に広がる
- 4410 の幅を 13 層でカバーできる

ごちきかの人はDilated Convolution は自作したらしい

Residual Network
- 画像認識分野において, 100 ~ 1000 層の CNN の学習を可能にした実績がある

学習について

<img src="https://gyazo.com/d2b9bd19e5cdf2edbae878f557852345.png" />
