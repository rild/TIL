 Web開発進めなきゃ

 一人でやる勢いで

# Android
Widgetについてまとめてみます。

seil君から質問が飛んできてWidget熱が再燃。頑張るぞ。

[ウィジェット公式ドキュメント](https://developer.android.com/guide/topics/appwidgets/index.html) 最高。

## まず初めに

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
