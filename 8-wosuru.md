# 8. 投稿機能を実装する

## 1. テキストフォームとProviderをデータバインディングさせる

次は![](<.gitbook/assets/freezed (1).png>)**freezed** と![](<.gitbook/assets/statenotifier (1).png>)**StateNotifier** も使って、投稿機能を実装しましょう。

まず**freezed**ですが、これは**immutableな(変更不可能な)クラス**が必要とするいろいろな機能を、\
イイ感じに生成してくれるパッケージです。

今までに何回か登場している**Postクラス**が**freezed**で作成したクラスになっています。\
`abstract/post.dart`で定義されています。(freezed独特の書き方をします)

{% code title="abstract/post.dart " %}
```dart
@freezed
abstract class Post with _$Post {
  const factory Post({
    @Default('') String user,
    @Default('') String body,
    @Default('') String uid,
    @Default('') String photoURL,
    @Default(null) DateTime? timeStamp,
  }) = _Post;
}
```
{% endcode %}

**StateNotifier**は値に変更があったときに自動で通知を飛ばしてくれるクラスです。\
状態の変化に反応して動的に値を表示するような処理をスッキリ書くことが出来ます。

そしてこれらを組み合わせた**StateNotifierProvider**というProviderを作ることで、\
データバインディングを実現することが出来ます。

では実際に動きを見てみましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `postmodal/postmodal_viewmodel.dart`の`changeBody`のコメントアウトを削除。

{% code title="postmodal/postmodal_viewmodel.dart(一部省略)" %}
```diff
final postStateNotifierProvider = StateNotifierProvider<PostStateNotifier>((ref) {
  return PostStateNotifier();
});

class PostStateNotifier extends StateNotifier<Post> {
  PostStateNotifier() : super(const Post());

  // Todo
  void changeBody(String value) {
+   state = state.copyWith(body: value);
  }
  // ...
}
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

フォームのテキストに連動して文字数がカウントされるようになったかと思います。

### 解説

軽く解説を行います。

**postStateNotifierProvider**は**StateNotifierProvider**をインスタンス化したものです。\
中身は**PostStateNotifier**でこれは**PostクラスをStateNotifier**でラップしたものになります。

分かりにくいですね、、、簡単に言うとこのProviderは、

1. Postの型に従ったデータを持っています
2. 自分の値を変更するメソッドを持っています
3. 値が変更されたら新しい値を通知します

そしてフォームに文字を打ち込むごとに値を更新し、その結果を文字数カウントに反映させることで、\
**テキストフォーム**と**Provider**と**文字数カウント**でデータバインディングするようにしています。

todo: いい感じの図

自分の値を書き換えるときは`state = state.copyWith(body: value)`と記述します。

`state`で自分自身にアクセスし、`copyWith`で現在の値をコピーした上で新しい値で更新します。\
`copyWith`メソッドは**freezedが自動で生成**してくれたメソッドです\*\*。\*\*(自力で書くとかなり大変)

## 2. 投稿機能を実装

では最後に投稿機能を実装しましょう。次の操作を行ってください。

{% hint style="success" %}
#### work

* `postmodal/postmodal_viewmodel.dart`の`addPost`のコメントアウトを削除。

{% code title="postmodal/postmodal_viewmodel.dart(一部省略)" %}
```diff
class PostStateNotifier extends StateNotifier<Post> {
  PostStateNotifier(this.user, this.posts) : super(const Post());
  final StateController<bool> user; // timeline_viewmodelのユーザー情報
  final StateController<List> posts; // timeline_viewmodelの投稿リスト
  
  //Todo
  void addPost() {
+   // ログイン情報で更新する値を切り替え
+   if (user.state == true) {
+     state = state.copyWith(
+       user: "おじ",
+       uid: "oji",
+       photoURL: url,
+       timeStamp: DateTime.now(),
+     );
+   } else {
+     state = state.copyWith(
+       user: 'anonymous',
+       uid: 'anonymous',
+       timeStamp: DateTime.now(),
+     );
+   }
+   
+   // 投稿リストを更新
+   final newPosts = [...posts.state];
+   newPosts.add(state);
+   posts.state = newPosts;
  }
}
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

フォームに打ち込んだ文章を投稿できるようになったかと思います。
