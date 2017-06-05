## 分割, Segmentation

音響信号処理では, ある時間に対して一つのフレームを操作することは一般的である. 一定のサイズのフレームか, increment などのホップサイズのフレームが用いられる.

フレームは大抵, 10 ~ 100 ms の遅延が起きるように選択される.

[チャープ信号](https://ja.wikipedia.org/wiki/%E3%83%81%E3%83%A3%E3%83%BC%E3%83%97%E4%BF%A1%E5%8F%B7), audio sweep signal, を作成してみます. ここでは, 周波数は 110 Hz ~ 880 Hz に変調されます.

そこで, 信号を分割して, それぞれのフレームに対して, 過ゼロ率を計算を計算します.

まず, パラメータをセットします.

```py
T = 3.0      # duration in seconds
fs = 44100.0 # sampling rate in Hertz
f0 = 440*numpy.logspace(-2, 1, T*fs, endpoint=False, base=2.0) # time-varying frequency
print f0.min(), f0.max() # starts at 110 Hz, ends at 880 Hz

# 110.0 879.9861686
```

チャープ信号を生成します.

```py
t = numpy.linspace(0, T, T*fs, endpoint=False)
x = 0.01*numpy.sin(2*numpy.pi*f0*t)
```

生成した信号を聞いてみます.

```
from IPython.display import Audio
Audio(x, rate=fs)
```

### Python のリスト表現を使って分割する

Python では, 標準の[リスト表現](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions) を使って信号を分割することができる. また, 同時に zero-crossing rate も計算することができる.

- 周波数の計算ができる？

```py

import essentia
from essentia.standard import ZeroCrossingRate
zcr = ZeroCrossingRate()
frame_sz = 1024
hop_sz = 512
plt.semilogy([zcr(essentia.array(x[i:i+frame_sz])) for i in range(0, len(x), hop_sz)])
```

<img src="https://gyazo.com/5dc91355e7b511e2038ae64138c736f1.png" />


#### librosa.util.frame

信号が与えられた時, **librosa.util.frame** は一様にサイズが調整されたフレームのリストを返す.

```py
F = librosa.util.frame(x, frame_sz, hop_sz)
print F.shape # (1024, 257)
```

つまり, **librosa** を使うことで, 信号を自分で分割する必要がなくなる.

特徴量抽出メソッド自体が, 使用する人に分割化を行うからである.

### essentia.standard.FrameGenerator

[essentia.standard.FrameGenerator](http://essentia.upf.edu/documentation/reference/std_FrameGenerator.html) も音響信号の分割に使用することができる.

それぞれのフレームに対して, zero-crossing rate を計算して, 表示することができる.

```py
import essentia
from essentia.standard import FrameGenerator
plt.semilogy([zcr(frame) for frame in FrameGenerator(essentia.array(x), frameSize=frame_sz, hopSize=hop_sz)])
```

<img src="https://gyazo.com/9cdc639eddf70074f14da92149ba4baa.png" />

### Example: Spectrogram

スペクトログラムを生成してみる.

信号のそれぞれのフレームに対して, [Hamming window](https://en.wikipedia.org/wiki/Window_function#Hamming_window) を適用して, ウィンドウ処理を行なった後に, そのスペクトラムを計算する.

```py
from essentia.standard import Spectrum, Windowing, FrameGenerator
hamming_window = Windowing(type='hamming')
spectrum = Spectrum()  # we just want the magnitude spectrum

spectrogram = numpy.array([spectrum(hamming_window(frame))
                     for frame in FrameGenerator(essentia.array(x), frameSize=frame_sz, hopSize=hop_sz)])
```

このスペクトログラムは 260 フレームあり, それぞれ 513 種類の周波数, frequency bins, がある

```py
print spectrogram.shape # (260, 513)
```

最終的に, そのスペクトログラムをプロットする.

時間が横軸で, 周波数が縦軸に表示されるように, スペクトログラムの配列を置き換える必要がある.

```py
plt.imshow(spectrogram.T, origin='lower', aspect='auto', interpolation='nearest')
plt.ylabel('Spectral Bin Index')
plt.xlabel('Frame Index')
```

<img src="https://gyazo.com/d026910c58d4f67761503dc72168a59b.png" />

スペクトログラムを表示するだけなら, Matplotlib や librosa を使った簡単な方法もある.

Essentia による分割を説明した時に使った例がそれである.
