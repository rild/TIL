# 開発メモ
詰まったところを残しておく

## Day1

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
