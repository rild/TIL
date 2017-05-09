### 8th
> 4.2.4 [バッチ対応版]交差エントロピー誤差の実装

ここがよくわからない.

> 実装のポイントは、one-hot 表現で t が 0 の要素は、交差エントロピー誤差 も 0 であるから、その計算は無視してもよいということです。言い換えれば、正 解ラベルに対して、ニューラルネットワークの出力を得ることができれば、交 差エントロピー誤差を計算することができるのです。

```py
def cross_entropy_error(y, t):
         if y.ndim == 1:
             t = t.reshape(1, t.size)
             y = y.reshape(1, y.size)
         batch_size = y.shape[0]
         # return -np.sum(t * np.log(y)) / batch_size
         return -np.sum(np.log(y[np.arange(batch_size), t])) / batch_size
```

`log` の計算回数が減るから計算が早くなるって話？

> ニューラルネットワークの学習の際に、認識精度を“指標”にしてはいけない。 その理由は、認識精度を指標にすると、パラメータの微分がほとんどの場所で 0 になってしまうからである。

大事な部分. (多分)


### 1st
OpenCV のライブラリを使いながら feature detector をpythonで作ろうとしたら

`cv2` 入ってない問題発生して、入れようとしたら、

brew 関連で困った

/user/local の権限を変更して,
brew コマンド通るように変更する必要があった

http://www.yukun.info/blog/2016/01/homebrew-directory-not-writable.html
> 権限変更関連


`brew install opencv3` をオプション無しでやったら python2.7 のライブラリが
入っていた感じが下からオプション付きでやり直した.

追記
brew で入れるの断念

conda にしよう
http://qiita.com/keitaMatsuo/items/900e549769484363fba2　
> anaconda の install with pyenv

in installing with pyenv, /bin/ is located on ~/.pyenv/versinos/...
知らなかったよ
考えたら当たり前だけど...

command not found 祭り
http://qiita.com/noraworld/items/4556f91bc31f641d187d
.bash_profile の PATH を上書きするときに, :$PATH つけ忘れて, 何もできなくなる案件(再)発生
昔やったなぁ...
成長してないなぁ...

次はやらないようにしよう...
http://qiita.com/keisei_1092/items/746dfe6ddac9b4f516b3
`export PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin`

``` >>> fast = cv2.FastFeatureDetector()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: module 'cv2' has no attribute 'FastFeatureDetector'
```

> fixed, should be cv2.FastFeatureDetector_create()

https://github.com/opencv/opencv/issues/6534
