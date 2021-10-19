# 7. 投稿リスト / アイコンを表示する

## 1. StateProviderで投稿リストを保持する

まずは![](<.gitbook/assets/riverpod (1).png>)**Riverpod** と![](<.gitbook/assets/flutterhooks (1).png>) **Flutter Hooks** を使って投稿リストを作成します。

では実際に使って動きを見てみましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `timeline/timeline_viewmodel.dart`の`postsProvider`のコメントアウトを解除。

{% code title="timeline/timeline_viewmodel.dart" %}
```diff
// Todo
final postsProvider = StateProvider(
  (ref) => [
+   Post(
+     user: 'anonymous',
+     body: 'body1',
+     uid: 'anonymous',
+     photoURL: '',
+     timeStamp: DateTime(2021),
+   ),
+   Post(
+     user: 'anonymous',
+     body: 'body2',
+     uid: 'anonymous',
+     photoURL: '',
+     timeStamp: DateTime(2021),
+   ),
+   Post(
+     user: 'anonymous',
+     body: 'body3',
+     uid: 'anonymous',
+     photoURL: '',
+     timeStamp: DateTime(2021),
+   ),
  ],
);
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

投稿がカードになって表示されるかと思います。

![](<.gitbook/assets/image (4) (1).png>)

### 解説

軽く解説を行います。

まずは`timeline/timeline_viewmodel.dart`の`postProvider`を確認してください。

ここでは**Riverpod**の**StateProvider**を使っています。\
**StateProvider**とは状態を保持できるシンプルなProviderです。

使い方は、**StateProviderクラス**の中で保持したい値をreturnするだけです。

次に`timeline/timeline_view.dart`の`_timeLine`を確認してください。

ここで**Flutter Hooks**の**useProvider**を使ってstatus呼び出しています。中の値を取り出して使うときは`変数.state`で呼び出します。

{% tabs %}
{% tab title="viewmodel" %}
{% code title="timeline/timeline_viewmodel.dart" %}
```dart
// Todo
final postsProvider = StateProvider(
  (ref) => [
    Post(
      user: 'anonymous',
      body: 'body1',
      uid: 'anonymous',
      photoURL: '',
      timeStamp: DateTime(2021),
    ),
    Post(
      user: 'anonymous',
      body: 'body2',
      uid: 'anonymous',
      photoURL: '',
      timeStamp: DateTime(2021),
    ),
    Post(
      user: 'anonymous',
      body: 'body3',
      uid: 'anonymous',
      photoURL: '',
      timeStamp: DateTime(2021),
    ),
  ],
);
```
{% endcode %}
{% endtab %}

{% tab title="view" %}
{% code title="timeline/timeline_view.dart" %}
```dart
  // bodyの要素
  Widget _timeLine(BuildContext context) {
    final posts = useProvider(postsProvider); // ここでposts呼び出し
    return _timeLineCards(context, posts.state); // 変数.state で値にアクセスできる
  }

  Widget _timeLineCards(BuildContext context, List posts) {
    return ListView.builder(
      itemCount: posts.length,
      itemBuilder: (context, index) {
        return _postCard(posts[index]);
      },
      reverse: true,
    );
  }

  Widget _postCard(Post post) {
    return Card(
      child: ListTile(
        leading: _postIcon(post),
        title: Text(post.user),
        subtitle: Text(post.body),
        isThreeLine: true,
      ),
    );
  }
```
{% endcode %}
{% endtab %}
{% endtabs %}

###

## 2. StateProviderのユーザー情報を更新する

次に**StateProvider**の値を更新してみましょう。

**StateProvider**は外からの変更を受け取れるという特徴を持っていて、\
`変数.state = 新しい値`で値を更新することが出来ます。

ではユーザー情報を更新できるようにしましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `timeline/timeline_viewmodel.dart`の`signIn`と`signOut`のコメントアウトを解除。

{% code title="timeline/timeline_viewmodel.dart" %}
```dart
final authProvider = StateProvider((ref) => false);

// Todo
void signIn(StateController user) {
+ user.state = true;
}

void signOut(StateController user) {
+ user.state = false;
}
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

これでログインボタンが機能するようになりました。(ログインするとおやじのイラストが表示されます)

![](<.gitbook/assets/image (5) (1).png>)
