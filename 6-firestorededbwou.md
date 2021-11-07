# 6. FireStoreでDB連携を行う

## 1. FireStoreを有効にする

## 2. データを書き込む処理を実装する

次の操作を行ってください

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

## &#x20;3. データを取得する処理を実装する



次の操作を行ってください

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
