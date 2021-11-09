# 6. FireStoreでDB連携を行う

## 1. Firestoreを有効にする

Firestoreを有効にします。次の操作を行ってください。

{% hint style="success" %}
### work

* [**Firebase コンソール**](https://console.firebase.google.com)へ移動する
* Firestore Database > データベースの作成 を選択
* テストモードで開始する > 次へ > asia-northeast1 > 有効にする を選択
{% endhint %}

{% embed url="https://scribehow.com/shared/FireStore__HI7dy8FUQxatkxRQwvun_A" %}

## 2. データを書き込む処理を実装する

データを書き込む処理を実装しましょう。次の操作を行ってください。

{% hint style="success" %}
* `model/posts_model.dart`の`addPstDB`のコメントアウトを解除。

{% code title="model/posts_model.dart " %}
```dart
void addPostDB(Post post) async {
+  await FirebaseFirestore.instance.collection('posts').add(post.toJson());
}
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

投稿ボタンを押すことで、Firestoreにデータが追加されることを確認しましょう。

### 解説

Firestoreにデータを書き込む方法はいくつかありますが、今回は**add**を使って**postsコレクション**にデータを追加しています。

また、postクラスのままだとFirestoreに追加できないので、toJsonメソッド\*でjson形式にしています。

\*toJsonメソッドは[freezed](https://app.gitbook.com/s/-MkUYx1nH-LtZrLYKsQ9-103505250/6-flutterdenonitsuite#freezed)の機能です。

## &#x20;3. データを取得する処理を実装する

次にFirestoreからデータを取得します。次の操作を行ってください。

{% hint style="success" %}
* `model/posts_model.dart`の`postsModelProvider`のコメントアウトを解除。

{% code title="model/posts_model.dart " %}
```dart
final postsModelProvider = StreamProvider.autoDispose((ref) {
+  final stream = FirebaseFirestore.instance
+      .collection('posts')
+      .orderBy('timeStamp')
+      .snapshots();
+  final posts = stream.map(
+    (snapshot) => snapshot.docs.map(
+      (doc) => Post.fromJson(doc.data()),
+   ),
+ );
+ return posts;
- //return Stream<Iterable<Post>>.value([]);
});

```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

これでFirestoreのデータが投稿カードとしてアプリに表示されるようになりました。

### 解説

`postsModelProvider`を確認してください。

ここでもAuthと同じStream型とするため`StreamProvider`を利用しています。

メソッドの中では、`.collection`でpostsを指定し、`.orderBy`で時間順に並び替え、`.snapshots`でデータをStream型で受け取っています。受け取ったデータはjson形式のため、fromJsonメソッド\*\*でpost型に変換して受け取るようにしています。

\*\*fromJsonメソッドも[freezed](https://app.gitbook.com/s/-MkUYx1nH-LtZrLYKsQ9-103505250/6-flutterdenonitsuite#freezed)の機能です。
