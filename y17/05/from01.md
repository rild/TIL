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
