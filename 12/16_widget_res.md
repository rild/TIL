第３回記事書く

Unix system programming のじゅぎょー

---
ウィジェットを作りたい気持ちDrivenな記事、第３回目です。
リソースフォルダ編の後編です。ウィジェットのレイアウトについて翻訳していきます。

# ウィジェットのレイアウトを作る
ウィジェットはレイアウトを定義するための、xmlファイルのレイアウトリソースが必要になります。レイアウトファイルは (ActivityやFragment同様) `res/layout` に保存されている必要があります。

一部のViewオブジェクトは、ウィジェットのレイアウトリソースに使うことができないので注意が必要です。ウィジェットのレイアウトを作る場合は、[App Widget Design Guidelines](https://developer.android.com/guide/practices/ui_guidelines/widget_design.html) に従うことが推奨されています。

[レイアウト](https://developer.android.com/guide/topics/ui/declaring-layout.html)の記事の内容について慣れているならば、ウィジェットのレイアウトを作ることは難しくありません。しかし、ウィジェットのレイアウトは、[RemoteViews](https://developer.android.com/reference/android/widget/RemoteViews.html) の上に作られる点に気をつけなければなりません。`RemoteViews` では、全ての `layout` と `view` がサポートされている訳ではありません。

## RemoteViews でサポートされている `layout` オブジェクト
`RemoteViews` クラスでサポートされている (すなわちウィジェットで利用可能な) レイアウトクラスは以下の４種類です。
- [FrameLayout](https://developer.android.com/reference/android/widget/FrameLayout.html)
- [LinearLayout](https://developer.android.com/reference/android/widget/LinearLayout.html)
- [RelativeLayout](https://developer.android.com/reference/android/widget/RelativeLayout.html)
- [GridLayout](https://developer.android.com/reference/android/widget/GridLayout.html)

## RemoteViews でサポートされている `view` オブジェクト
`RemoteViews` クラスでサポートされている `widget class ` は以下の１２種類です。
> View クラスとは書かれていませんでしたが、以下全て、	`android.view.View` 継承クラスなので、ウィジェットで利用可能な View という理解で良さそうです。

- [AnalogClock](https://developer.android.com/reference/android/widget/AnalogClock.html)
- [Button](https://developer.android.com/reference/android/widget/Button.html)
- [Chronometer](https://developer.android.com/reference/android/widget/Chronometer.html)
- [ImageButton](https://developer.android.com/reference/android/widget/ImageButton.html)
- [ImageView](https://developer.android.com/reference/android/widget/ImageView.html)
- [ProgressBar](https://developer.android.com/reference/android/widget/ProgressBar.html)
- [TextView](https://developer.android.com/reference/android/widget/TextView.html)
- [ViewFlipper](https://developer.android.com/reference/android/widget/ViewFlipper.html)
- [ListView](https://developer.android.com/reference/android/widget/ListView.html)
- [GridView](https://developer.android.com/reference/android/widget/GridView.html)
- [StackView](https://developer.android.com/reference/android/widget/StackView.html)
- [AdapterViewFlipper](https://developer.android.com/reference/android/widget/AdapterViewFlipper.html)

## Custom View について
`RemoteViews` では、CustomView のサポートはしていないので、独自 View はウィジェットでは使えません。

## ViewStub について
`RemoteViews` では、[ViewStub](https://developer.android.com/reference/android/view/ViewStub.html) のサポートをしています。ウィジェットがレイアウトリソースを `inflate` するタイミングでは、読み込ませたくない View があるならば、ViewStub を使用することができます。

> `ViewStub` は、`invisible` かつ `zero-sized` な View であり、`setVisibility(int)`　か `inflate()` メソッドが配置されている ViewStub に対して要求された時に、配置された ViewStub と入れ替わりに `android:layout` に指定されているレイアウトリソースが読み込まれる。

## マージンについて
通常、ウィジェットは画面端からは離れていることが推奨されます。また、他のウィジェットと同一平面上に存在することも避けるべきです。

> *should not visually be flush with other widgets* の訳なのですが、他のウィジェットとの間にマージンがないといけない、という感じでしょうか。

以上の理由により、ウィジェットのレイアウトの周囲にマージンを入れる必要があります。

Android4.0 からは、ウィジェットと、ウィジェットが入っているグリッドの間に自動的に `padding` が設定されます。これにより、他のウィジェットやアプリのアイコンと並べた時にも、より良いレイアウトを提供することができます。この機能は強く推奨されており、ウィジェットの `targetSdkVersion` を 14 以上に設定することが求められています。

### Android4.0 以前のプラットフォームに対応する場合
Android4.0 以降のプラットフォームで、余計なマージンを表示することなく、Android4.0 以前のプラットフォームでマージンをウィジェットの周囲に設定することができます。(もうその[必要](https://developer.android.com/about/dashboards/index.html?hl=ja#Platform)はほとんどなさそうですが。)

作業手順は以下の通りです。
#### 1. `targetSdkVersion` を 14 以上に設定します。
#### 2. ウィジェットのレイアウトファイルに、`android:padding`を設定して、`dimension` リソース (`res/values/dimens/...`)の値を参照させます。

```xml
<FrameLayout
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  android:padding="@dimen/widget_margin">

  <LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal"
    android:background="@drawable/my_widget_background">
    …
  </LinearLayout>

</FrameLayout>
```

#### 3. `res/values` に Android4.0 未満、Android4.0 以降の２種類の `dimens.xml` を作成して、それぞれに `padding` を定義します。

`res/values/dimens.xml:`

```xml
<dimen name="widget_margin">8dp</dimen>
```

`res/values-v14/dimens.xml:`

```xml
<dimen name="widget_margin">0dp</dimen>
```

#### それ以外
[nine-patch](https://developer.android.com/guide/topics/graphics/2d-graphics.html#nine-patch) を変更する方法もあるみたいです。デフォルトで設定されている`nine-patch background asset`に対して、マージンを設定します。同時に、APIレベル 14 以上の端末用のマージンが入っていない `nine-patch` を用意すれば、`res/values` を使うのと同じような結果が得られます。

# さいごに
以上で、ウィジェットに使用するリソースの部分は終わりです。
次は、ソース (AppWidgetProvider継承クラス) の部分について触れていきます。

---
