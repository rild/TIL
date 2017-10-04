[CCRMAでのワークショップ](http://musicinformationretrieval.com/)

このページでは, [Basic Feature Extraction](http://musicinformationretrieval.com/basic_feature_extraction.html) のページの翻訳をしていきます.

## Basic Feature Extraction
なんらかの形で, 音響信号の特徴, characteristics を抽出する必要がある.

特徴が解決しようとするタスクに関連することが多い.

例えば, 音色によって楽器を分類するときに,
ピッチではなく音色ごとに音を識別するための特徴が必要になってくる.
ピッチ推定をする場合には, 音色ではなく, ピッチを識別する特徴が必要になる.

- 楽器分類, classify instruments
  - 音色によって音を識別するための特徴が必要
- ピッチ推定, perform pitch detection
  - ピッチを識別するための特徴が必要

20種類の音響信号で練習をします.
- 10種類のキックドラム (バスドラム？)
- 10種類のスネアドラム

それぞれ, 1回ドラムを叩いた音が入っている

簡単のため, 一度にこのデータをダウンロードするため
`stanford_mir.download_samples`
というライブラリを使う.

データを変数に代入する
```py
kick_signals = [
    librosa.load(p)[0] for p in kick_filepaths
]
snare_signals = [
    librosa.load(p)[0] for p in snare_filepaths
]
```

キックドラムの信号を表示する
```py
for i, x in enumerate(kick_signals):
    plt.subplot(2, 5, i+1)
    librosa.display.waveplot(x[:10000])
    plt.ylim(-1, 1)
```

<img src="https://gyazo.com/5f221583421aab18dc5b57e6036e5ef0.png" />

スネアドラムの信号を表示する
```py

for i, x in enumerate(snare_signals):
    plt.subplot(2, 5, i+1)
    librosa.display.waveplot(x[:10000])
    plt.ylim(-1, 1)
 ```

 <img src="https://gyazo.com/7502b39e24e7960aa164dedf63833dd8.png" />


### 特徴ベクトルを作る
ある特徴ベクトルは, 簡単にいうと一つの特徴の集まりである.

ある信号から２次元の特徴ベクトルを作る単純な関数の例を示す.

```py
def extract_features(signal):
    return [
        librosa.feature.zero_crossing_rate(signal)[0, 0],
        librosa.feature.spectral_centroid(signal)[0, 0],
    ]
```

一つの特徴セットの信号の中から抽出した全ての特徴ベクトルを集計したい場合,

次のリスト表現を使用することができる.

```py
kick_features = numpy.array([extract_features(x) for x in kick_signals])
snare_features = numpy.array([extract_features(x) for x in snare_signals])
```

それぞれのクラスで離散的なヒストグラムをプロットして,
特徴量の中の違いを可視化する.

```py

plt.hist(kick_features[:,0], color='b', range=(0, 0.1))
plt.hist(snare_features[:,0], color='r', range=(0, 0.1))
plt.legend(('kicks', 'snares'))
plt.xlabel('Zero Crossing Rate')
plt.ylabel('Count')
```

<img src="https://gyazo.com/9c9b37ec4884c5cfe130dd1816a2598f.png" />


```py

plt.hist(kick_features[:,1], color='b', range=(0, 4000), bins=40, alpha=0.5)
plt.hist(snare_features[:,1], color='r', range=(0, 4000), bins=40, alpha=0.5)
plt.legend(('kicks', 'snares'))
plt.xlabel('Spectral Centroid (frqeuency bin)')
plt.ylabel('Count')
```

<img src="https://gyazo.com/653748a86bb72d1cc541e8479e854dc0.png" />


### 特徴のスケーリング
前に示した例で使った特徴には, 過ゼロ率, zero crossing rate, とスペクトル重心を含んでいた.

それらの２つの特徴量は異なるユニットを使って表現される.

この不一致が, 後でクラスタリングをする時に問題になってくる.

したがって, それぞれの特徴量ベクトルを一般的な領域に正規化する. そして, 正規化されたパラメータをクラスタリングに使用するために保存しておく.

特徴量をスケーリングするために多くの手法が存在する.
今回は, [sklearn.preprocessing.MinMaxScaler](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.MinMaxScaler.html) を使用する.

**MinMaxScaler** はスケーリングされた値の配列を返す. それぞれの特徴量の次元は, -1 から 1 で表現される.

特徴ベクトルセットを一つの特徴テーブル, *feature table*, へ連結します.

```py
feature_table = numpy.vstack((kick_features, snare_features))
print feature_table.shape # (20, 2)
```

それぞれの特徴量の次元を -1 から 1 の範囲でスケーリングする

```py
scaler = sklearn.preprocessing.MinMaxScaler(feature_range=(-1, 1))
training_features = scaler.fit_transform(feature_table)
print training_features.min(axis=0) # [-1. -1.]
print training_features.max(axis=0) # [ 1.  1.]
```

スケールされた特徴量をプロットする
```py
plt.scatter(training_features[:10,0], training_features[:10,1], c='b')
plt.scatter(training_features[10:,0], training_features[10:,1], c='r')
plt.xlabel('Zero Crossing Rate')
plt.ylabel('Spectral Centroid')
```

<img src="https://gyazo.com/870586bcdbc8fa34bad17db3fd251afc.png" />
