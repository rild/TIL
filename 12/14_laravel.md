 Web開発進めなきゃ

 一人でやる勢いで

# Android
Android の Widget についてまとめてみます。

Widgetは個人的に、iPhoneと make a difference できるポイントだと思っています。
iPhoneにもウィジェットは[あります](https://support.apple.com/ja-jp/HT207122)が、アプリのアイコンと混在することはなさそう。

インターフェースの設計的な都合なのだろうと思っています。ホーム画面には、タイル状にアイコンが並ぶべし、みたいな。

seil君から質問が飛んできてWidget熱が再燃。頑張るぞ。

[ウィジェット公式ドキュメント](https://developer.android.com/guide/topics/appwidgets/index.html) 最高。

個人で新しく勉強しながら公式ドキュメントを訳しつつまとめていくので、間違いがきっとあると思います。

間違いを見つけた際はコメントでのご指摘をいただけると嬉しいです。

## まず初めに
一部のAndroid に関する記事は[日本語バージョン](https://developer.android.com/guide/index.html?hl=ja)が用意されていますが、

**Widgetの記事日本語じゃないのです！？**

エモい。

## App Widgets
公式ドキュメントのどの辺にあるか

Develop > API Guides > App Components

## Widgetとは

冒頭の部分の引用

> App Widgets are miniature application views that can be embedded in other applications (such as the Home screen) and receive periodic updates. These views are referred to as Widgets in the user interface, and you can publish one with an App Widget provider. An application component that is able to hold other App Widgets is called an App Widget host.

ウィジェットとは、「ホームスクリーンとかに埋め込まれちゃうような、ちっちゃなアプリ」

## Widget 関連記事
[App Widgets](https://developer.android.com/guide/topics/appwidgets/index.html) の記事からリンクが貼られていた記事
### デザイン
- Googleの[ウィジェットデザインガイドライン](https://developer.android.com/design/patterns/widgets.html)

に従うと良さそう

### ウィジェットのホストアプリ
- [App Widget Host](https://developer.android.com/guide/topics/appwidgets/host.html)

ウィジェットの親玉？

## Widget を作るために必要なこと
1. AppWidgetProviderInfo オブジェクトを使うこと
 - ウィジェットに関するメタデータ。
 - メタデータには、レイアウト、ウィジェットの更新頻度、AppWidgetProviderクラスに関する情報が含まれる。
 - XMLで記述される。
2. AppWidgetProvider クラスを実装すること
 - AppWidgetProviderはウィジェットを動作させる基本的なメソッドが定義されているクラス。
 - ブロードキャストイベントに基づく。
 - ウィジェットが更新、設置、停止、削除されたときAppWidgetProviderを通じて、ブロードキャストを受け取る。
 > **AppWidgetProvider class implementation**
 > : Defines the basic methods that allow you to programmatically interface with the App Widget, based on broadcast events. Through it, you will receive broadcasts when the App Widget is updated, enabled, disabled and deleted. (訳が自信ないので、原文を載せます。)

3. View layout
 - 見た目の部分。
 - レイアウトの初期値を与える。
 - XMLで記述される。

以上の３つが、ウィジェットを作るために必要になるもの。

これらに加えて、ウィジェット設定を変えるためのアプリを作ることも可能。

その場合は、専用の設定が必要 [> Creating an App Widget Configuration Activity](https://developer.android.com/guide/topics/appwidgets/index.html#Configuring)

### Broadcastについて
- [アプリケーションの基礎 > ブロードキャスト レシーバー](https://developer.android.com/guide/components/fundamentals.html?hl=ja)
- [BroadcastReceiver](https://developer.android.com/reference/android/content/BroadcastReceiver.html)


---
第２回
# Manifestでウィジェットを宣言する
ウィジェットを提供する [AppWidgetProvider](https://developer.android.com/reference/android/appwidget/AppWidgetProvider.html) 継承クラスを AndroidManifest.xml で宣言する必要があります。

`<application>` 配下に、`<receiver> ... </receiver>` を記述する。

## 書き方の例
```xml
<receiver android:name="ExampleAppWidgetProvider" >
    <intent-filter>
        <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
    </intent-filter>
    <meta-data android:name="android.appwidget.provider"
               android:resource="@xml/example_appwidget_info" />
</receiver>
```

- receiver
- intent-filter
- meta-data

の、３つの要素から構成されています。

## receiver
この要素には、 `android:name`の属性が必要になります。`android:name`には、ウィジェットに使われているAppWidgetProvider継承クラスが記述されているフォルダを指定します。

## intent-filter
この要素には、`<action>` に関する記述が必要になります。`<action>`では、AppWidgetProvider がブロードキャスト [ACTION_APPWIDGET_UPDATE](https://developer.android.com/reference/android/appwidget/AppWidgetManager.html#ACTION_APPWIDGET_UPDATE) を受け取ることを `android:name` に対して指定します。

`ACTION_APPWIDGET_UPDATE`以外のブロードキャストを指定することはできなさそうです。
> 原文: This is the only broadcast that you must explicitly declare.

[AppWidgetManager](https://developer.android.com/reference/android/appwidget/AppWidgetManager.html) が必要に応じて、自動的にウィジェットの AppWidgetProvider に対してブロードキャストを送ります。

## meta-data
AppWidgetProviderInfoオブジェクトとなる。ここには以下の２つの属性を設定する。

- android:name
 - メタデータに関する記述。 `android.appwidget.provider` を値として設定する。AppWidgetProviderInfo の記述子(descriptor)として、データを使用することを意味している。
- android:resource
 - AppWidgetProviderInfo の リソースフォルダの場所を指定している。
 - リソースフォルダとしては `res/xml/` を使うことになっているので、`@xml/ファイル名`という値を設定することになるはず。

# AppWidgetProviderInfo メタデータを追加する
[AppWidgetProviderInfo](https://developer.android.com/reference/android/appwidget/AppWidgetProviderInfo.html) には、ウィジェットに関する性質が定義されている。例としては、
- ウィジェットの最小サイズ
- ウィジェットが使用するレイアウト
- ウィジェットの更新頻度
- (あるなら)ウィジェットの configuration Activity
## 場所
`res/xml/`にAppWidgetProviderInfoに関するフォルダを作る。

<img width=220 src="https://gyazo.com/1d491443a0003f784f74ecc933b6e2a9.png"/>

## 書き方の例
```xml
<appwidget-provider xmlns:android="http://schemas.android.com/apk/res/android"
    android:minWidth="40dp"
    android:minHeight="40dp"
    android:updatePeriodMillis="86400000"
    android:previewImage="@drawable/preview"
    android:initialLayout="@layout/example_appwidget"
    android:configure="com.example.android.ExampleAppWidgetConfigure"
    android:resizeMode="horizontal|vertical"
    android:widgetCategory="home_screen">
</appwidget-provider>
```

`<appwidget-provider>`配下の属性について、まとめていきます。

## minWidth / minHeight
`minWidth / minHeight`の値は、ウィジェットのデフォルトサイズとなる、ウィジェットの最小サイズに関する属性。

デフォルトホームスクリーンでは、width / height  属性をもつグリッド型のウィンドウに基づいて、ウィジェットがレイアウトされる。

もし、作成したウィジェットの width / height の値が、グリッドのセルサイズにぴったり合わなかった場合、もっとも近いセルサイズに調整されてレイアウトされる。

[ウィジェットのサイズに関するガイドライン](https://developer.android.com/guide/practices/ui_guidelines/widget_design.html#anatomy_determining_size)を参照されたし。

> NOTE: 4 x 4 以下のセルでウィジェットを作成した場合、全てのデバイスで利用可能なウィジェットとはならない点に注意する。

### minResizeWidth / minResizeHeight
ウィジェットの絶対最小サイズを定義する値として、 `minResizeWidth / minResizeHeight`も存在する。これらは
ウィジェットが小さすぎて利用できなくなるサイズに関する値であり、`minResizeWidth / minResizeHeight` の値を設定することで、ユーザが`minWidth / minHeight` に設定したサイズよりも小さくリサイズすることができるようになる。

## updatePeriodMillis
ウィジェットが、[AppWidgetProvider](https://developer.android.com/reference/android/appwidget/AppWidgetProvider.html) から update リクエストを送る頻度に関する属性。コールバックメソッド onUpdate() がリクエストを送ります。

`updatePeriodMillis` に設置した時間ごとに、実際に update リクエストがあることが保証されている訳ではありません。

### 推奨される更新頻度
また、 update リクエストを送る頻度は、バッテリー消費を抑える意味でも、**一時間に一回程度** に抑えることが望ましいみたいです。

インストールしているウィジェットを、１５分毎に更新したいユーザがいれば、１日に一回更新すればいいと感じるユーザもいるかもしれないため、更新頻度については、ユーザが設定できるようにしておくのも推奨されています。

### AlarmManager を使った更新
ウィジェット更新のタイミングでデバイスがスリープ状態であった場合、デバイスは更新を行うために、起動して更新を行います。　

この機能は一時間に一度程度なら、バッテリ消費に与える影響はほとんどありませんが、それ以上の頻度で更新が起きる場合、バッテリ消費を早める原因となりえます。

更新頻度が多くなる場合、また、一定の間隔で更新が起こる必要がない場合には、`updatePeriodMillis` の代わりに、 `AlarmManager` を使うことでデバイスが起動している時のみ更新するようにできます。

[AlarmManager](https://developer.android.com/reference/android/app/AlarmManager.html) を使って、AppWidgetProvider継承クラスへの Intent と共に、アラームを設定することで、通常のウィジェットの更新の代わりとすることができるみたいです。

この場合、alarm type には、[ELAPSED_REALTIME](https://developer.android.com/reference/android/app/AlarmManager.html#ELAPSED_REALTIME) または [RTC](https://developer.android.com/reference/android/app/AlarmManager.html#RTC) を設定します。`updatePeriodMillis` にゼロ`"0"`を設定することも忘れないようにしましょう。

## initialLayout
ウィジェットに使用するレイアウトリソースを設定します。
`"@layout/widget_layout"`のような値になると思われます。

## configure
ユーザがウィジェットを追加した時, 起動する Activity を定義します。

ウィジェット追加時に Activity を起動することで, ユーザがウィジェットの初期設定を行うことができます。

より詳細な情報は [Creating an App Widget Configuration Activity](https://developer.android.com/guide/topics/appwidgets/index.html#Configuring) を参照されたし。

## previewImage
ウィジェットが配置された際のプレビューを提供するための属性。ユーザがウィジェットを選択するリストに並ぶことになる。もし、`previewImage` が設定されていなかった場合、代わりにアプリのアイコンが表示される。

AppWidgetProviderInfo の `previewImage` は、 `AndroidManifest.xml` の `<receiver>` にある ` android:previewImage` と一致する。

より詳細な情報は [Setting a Preview Image](https://developer.android.com/guide/topics/appwidgets/index.html#preview) を参照されたし。

Android3.0 から実装。

## resizeMode
ウィジェットがリサイズされる時のルールを定義します。開発者はウィジェットがホームスクリーン上で縦横にリサイズできる様にするために、 `resizeMode` を利用することができます。

ユーザはウィジェットをリサイズするために、長押しを行います。リサイズハンドラが出現したら、縦横の変更する向きにハンドラをドラッグしてウィジェットのリサイズを行います。このリサイズは、ホームスクリーンのグリッドに合わせて行われます。

`resizeMode` に対して設定可能な値は、
- "horizontal"
- "vertical"
- "none"
の３種類です。

縦横どちらにもリサイズ可能にするためには、
- "horizontal|vertical"
を設定します。

Android3.1より実装。

## minResizeHeight / minResizeWidth
> `minWidth / minHeight` に移動。

## widgetCategory
`widgetCategory` にはウィジェットがホームスクリーン`home_screen`や、ロック画面`keyguard`に表示可能かどうかを設定することができます。

ロック画面でのウィジェット設置は、Android5.0以下で実装可能であり、それ以上のバージョンでは、ウィジェットはホームスクリーンにのみ設置可能となっている様です。

次は、ウィジェットのレイアウトリソースの作成の記事です。

以上で、ウィジェットに使用するリソースの部分は終わりです。
次はいよいよ、ソースコード (AppWidgetProvider継承クラス) の部分について触れていきます。
