# April
## 27th 
Python3系で描画できない問題

`~/.bash_profile`
に忘れ物. 

```
eval "$(pyenv init -)"
```

`pip`
は python のバージョンごとに管理してるのね
pyenv global 3.5.1 で pip list したら何も出てこなくて焦った. 
知らなかったよ. 

## 26th
GitHub の方でアカウント認証されなくて困った.
研究室の方の GitLab 用に global の config を書き換えちゃったためであるとはすぐにわかったものの,

直すのに, ちょっと時間かかった.

```shel
git config --local user.name
git config --local user.email
```

`user.mail` という勘違いが原因だった.

thx [qiita](http://qiita.com/zaki-yama/items/bfb0c2bef516af58c3fa)

## 21st
そもそも Text-to-Speech をやるにはどう使えばいいのやら

http://stackoverflow.com/questions/41679110/how-to-use-tensorflow-wavenet

> issues で話し合われていることを見るといい

みたいなことが書かれていた

https://github.com/ibab/tensorflow-wavenet/issues/189

ここの流れをまず追ってみる
Speech-to-Text をやってから, データを作って, Text-to-Speech の学習をすればいいんじゃない？とかやってた
