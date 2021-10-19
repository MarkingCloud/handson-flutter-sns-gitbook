# 5. 画面レイアウトを作成する

## 1. main.dartを確認する

では画面レイアウトを作成していきましょう。

まずは`main.dart`を確認してみます。

{% code title="main.dart" %}
```dart
void main() {
  runApp(
    const ProviderScope(
      child: MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);
  
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'MarkingCloud SNS',
      home: const TimeLinePage(),
      routes: {
        '/post': (BuildContext context) => const PostModalPage(),
      },
      debugShowCheckedModeBanner: false,
    );
  }
}
```
{% endcode %}

### 解説

軽く解説を行います。

L21～L30に注目してください。**Widget**という見慣れない言葉が書かれています。

**Widget**とはFlutterが定義しているクラスで、画面を構成するパーツを意味します。\
**ButtonWidget**などオブジェクトを配置するものや、**CenterWidget**など位置を調整するものがあります。

ここでは**MaterialApp**というWidgetが使われており、さらに**TimeLinePage**が呼び出されています。

## 2. AppBarを表示する

では**TimeLinePage**が書かれている`timeline/timeline_view.dart`を確認してみましょう。

{% code title="timeline/timeline_view.dart " %}
```dart
class TimeLinePage extends HookWidget {
  const TimeLinePage({Key? key}) : super(key: key);

  @override

  // Todo
  Widget build(BuildContext context) {
    return Scaffold(
      // appBar: AppBar(
      //   title: const Text('Time Line'),
      //   actions: [_userIcon(), _authButton()],
      // ),
      body: _timeLine(context),
      // floatingActionButton: _postButton(context),
    );
  }
// ...
}
```
{% endcode %}

ここでは**Scaffold**というWidgetが使われています。\
**Scaffold**はアプリの土台となるWidgetで、簡単にアプリらしいレイアウトを作ることができます。

では実際にAppBarを表示してみましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `timeline/timeline_view.dart`の`Scaffold`の`appBar`のコメントアウトを解除。

{% code title="timeline/timeline_view.dart " %}
```diff
  // Todo
  Widget build(BuildContext context) {
    return Scaffold(
+     appBar: AppBar(
+       title: const Text('Time Line'),
+       actions: [_userIcon(), _authButton()],
+     ),
      body: _timeLine(context),
      // floatingActionButton: _postButton(context),
    );
  }
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

画面上部にAppBarが表示されたかと思います。簡単ですね！

![](<.gitbook/assets/image (1) (1).png>)

## 3. floatingActionButtonを表示する

次は右下の追加ボタンを作成しましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `timeline/timeline_view.dart`の`Scaffold`の`floatingActionButton`コメントアウトを解除。

{% code title="timeline/timeline_view.dart " %}
```diff
  // Todo
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Time Line'),
        actions: [_userIcon(), _authButton()],
      ),
      body: _timeLine(context),
+     floatingActionButton: _postButton(context),
    );
  }
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

コレで右下のよく見るボタンが簡単に作成できました！

![](<.gitbook/assets/image (3) (1).png>)
