Google Play Music のウィジェットとかもいいよね

---

ウィジェットを作りたい気持ちDrivenな記事、第４回です。

Androidのウィジェットの開発に関する記事です。公式ドキュメント[App Widgets](https://developer.android.com/guide/topics/appwidgets/index.html)の訳を中心に記事を書いていきます。

間違いを見つけた場合、コメントで指摘していただけると幸いです。

AppWidgetProvider編です。

# AppWidgetProvider クラスを使う
[AppWidgetProvider](https://developer.android.com/reference/android/appwidget/AppWidgetProvider.html) クラスは BroadcastReceiver の子クラスなので、ウィジェットへのブロードキャストを扱うことができます。`AppWidgetProvider` が受け取るのは、 `updated、deleted、enabled、disabled` といった、ウィジェットに関連のあるブロードキャストイベントだけです。これらのブロードキャストイベントが起きた際に、`AppWidgetProvider` の対応するメソッドが実行されます。

## AppWidgetProviderのコールバックメソッド
## onUpdate()
AppWidgetProviderInfoの `updatePeriodMillis` に設定されたインターバルでウィジェットを更新するタイミングで呼ばれるメソッド。([Adding the AppWidgetProviderInfo Metadata](https://developer.android.com/guide/topics/appwidgets/index.html#MetaData)、[【第２回】:updatePeriodMillis](http://qiita.com/rild/items/43881b44a356d9888aa1#updateperiodmillis))

このメソッドは、ユーザがウィジェットを配置した際にも呼ばれるため、ウィジェットに必要な初期化も行われる。ウィジェットの View へのイベントハンドラの設定を行ったり、一時的な [Service](https://developer.android.com/reference/android/app/Service.html) をスタートさせることができる。しかし、必要であるならば、ウィジェットの `configration Acitivity` で、ウィジェット設置時に `onUpdate()` メソッドが呼ばれないように設定することができる。[Creating an App Widget Configuring Activity](https://developer.android.com/guide/topics/appwidgets/index.html#Configuring)
## onAppWidgetOptionsChanged()

## onDeleted(Context, int[])

## onEnabled(Context)

## onDisabled(Context)

## onReceive(Context, Intent)
