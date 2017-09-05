# 開発メモ
詰まったところを残しておく

## Day1

surfaceChanged が２回呼ばれて, デバッグログが２重に出てくる.

<img src="https://gyazo.com/7a103e8973f5da91949bb6fd010160c0.gif"/>

<img src="https://gyazo.com/16a750fb22701b681084036d296ad5f2.gif"/>

<img width=350 src="https://gyazo.com/f4bbc9bf656f713ecf47c675cf93244b.png"/>


これは！

```java
      Rect src = new Rect(
              (pos.x + j) * TILE_SIZE,
              (pos.y + i) * TILE_SIZE,
              (pos.x + j) * TILE_SIZE + TILE_SIZE,
              (pos.y + i) * TILE_SIZE + TILE_SIZE);

      Rect dst = new Rect(
              imageNo * IMAGE_TILE_SIZE,
              0,
              imageNo * IMAGE_TILE_SIZE + IMAGE_TILE_SIZE,
              IMAGE_TILE_SIZE);

//                    c.drawBitmap(icon, src, dst, p);
      c.drawBitmap(icon, dst, src, p);
```

<img src="https://gyazo.com/2c840d6212c318f93e6969668e520ff8.gif" />

### 表示されない？
#### 起きたこと
```java
  @Override
   public void surfaceCreated(SurfaceHolder surfaceHolder) {
       mField = new Field();
       mHolder = surfaceHolder;

       Log.d(TAG, "created");

       /***
        * ゲームの描画開始
        */

       start();
   }

   private void start() {
    Canvas canvas = mHolder.lockCanvas();
    mField.draw(canvas);

    canvas.drawColor(Color.BLUE);

    mHolder.unlockCanvasAndPost(canvas);
  }

```

これで描画されると思ったんだけれど、真っ白なまま...

#### コールバックを設定し忘れた
`getHolder().addCallback(this);` をやり忘れてた.

### Window のサイズが取れない
#### surfaceChanged だと
`public void surfaceChanged(SurfaceHolder holder, int format, int width, int height)` で渡ってくる width, height の情報がなんかおかしい.

#### surfaceCreated で
getWidth / getHeight を呼んで対応してみた.

### うまく枠が作られない？
#### 起きたこと, やったこと
```java
g.fillRect(x * TILE_SIZE, y * TILE_SIZE, TILE_SIZE,
                            TILE_SIZE);
```
この部分の置き換えを

```java
c.drawRect(x * TILE_SIZE, y * TILE_SIZE, TILE_SIZE,
                                TILE_SIZE, p);
```

こうしてたら,

<img widt=350 src="https://gyazo.com/8966146e8c7c788d838cbee1039fc7e2.png" />

こうなった.

#### 解決
<img src="https://gyazo.com/d5bf0d54e93b373528b94ec9113b6d1f.png" />

<img src="https://gyazo.com/17b5fe5a855453e706906dab61cbf3cc.png" />

```java
c.drawRect(x * TILE_SIZE, y * TILE_SIZE, x * TILE_SIZE + TILE_SIZE,
                                y * TILE_SIZE + TILE_SIZE, p);
```

field にはちゃんと入っていたので描画処理が悪いと判断.
長方形の左上, 右下がうまく入っていなかった.

### 正方形のブロックの描画
#### 形がおかしい
<img src="https://gyazo.com/29ba1a8f2f6417feda04c2be9ffccfcd.png" />

#### 右下 Y 座標の設定ミス
<img src="https://gyazo.com/69bcb867f31766f0e0a6f395afbbd22c.png" />

`topLeftY + TILE_SIZE` とすべきところを `topLeftX + TILE_SIZE` と書いていた.

### UIスレッド
外部スレッドから view 触ろうとして怒られた.

```
android.view.ViewRootImpl$CalledFromWrongThreadException: Only the original thread that created a view hierarchy can touch its views.
```

http://cuuma.publog.jp/archives/30332977.html


```java
runOnUiThread(new Runnable() {

    public void run() {
         //UI操作するコードをここに書く
    }
});
```
