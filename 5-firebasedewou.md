# 5. Firebaseで認証連携を行う

## 1. Firebase Authを有効にする

最初にFirebaseの管理画面からGoogleアカウントの認証機能を有効にしましょう。

次の操作を行ってください。

{% hint style="success" %}
### work

* [**Firebase コンソール**](https://console.firebase.google.com)へ移動する
* Authentication > 始める > Sign-in method > 追加プロバイダ > Google を選択
* 「有効にする」を選択 > 「プロジェクトサポートメール」を選択 > 保存を選択
* 承認済みドメイン > ドメインを追加 を選択
* アプリを開いているページのURLを張り付け > 追加を選択
{% endhint %}

{% embed url="https://scribehow.com/shared/Firebase_Auth__P2kC24BFQfOxN0ZKPgHbvQ" %}

## 2. サインイン・サインアウト機能を実装する

まずはFirebaseのAuth使った認証連携を実装しましょう。

次の操作を行ってください

{% hint style="success" %}
### work

* `model/auth_model.dart`の`signInAuth`と`signOutAuth`のコメントアウトを解除。

{% code title="model/auth_model.dart " %}
```dart
void signInAuth() {
+  GoogleAuthProvider googleProvider = GoogleAuthProvider();
+  FirebaseAuth.instance.signInWithPopup(googleProvider);
}

void signOutAuth() async {
+  FirebaseAuth.instance.signOut();
}
```
{% endcode %}



* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

右上のサインインボタンからサインインを行ってみましょう。

Firebase コンソール の Authentication > Users に自分の情報が登録されていれば成功です。

## 3. ユーザー情報を取得する処理を実装する

次にログイン情報を取得する処理を実装しましょう。

次の操作を行ってください

{% hint style="success" %}
### work

* `model/auth_model.dart`の`authModelProvider`と`getCurrentUser`のコメントアウトを解除。

{% code title="model/auth_model.dart " %}
```dart
final authModelProvider = StreamProvider.autoDispose((ref) {
+ return FirebaseAuth.instance.authStateChanges();
- // return Stream<User?>.value(null);
});

User? getCurrentUser() {
+  final user = FirebaseAuth.instance.currentUser;
+  if (user != null) {
+    return user;
+  } else {
+    return null;
+  }
-  // return null;
}
```
{% endcode %}

* webサーバーをリロードする（実行を止めてしまった場合は再実行）。

```bash
flutter run -d web-server --web-port=8080 --web-renderer html
```
{% endhint %}

### 解説

まずは `authModelProvider` を確認してください。

ここでは **FirebaseAuth.instance.authStateChanges** というメソッドでFirebaseAuthの**認証情報の変化**を**Stream型**で取得しています。Stream型とは監視対象からの通知によってデータ取得する(Pub/Subと言われるモデル)場合に利用される型です。

`authModelProvider`は以下のように利用します。

* `useProvider`を使ってView側で呼び出す。
* `.when`メソッドでデータ取得後(data)、データ取得中(loading)、エラー時(error)の処理を記述。

例として`timeline/timeline_view.dart`の`_authButton`を確認してみましょう。

{% code title="timeline/timeline_view.dart" %}
```dart
  Widget _authButton() {
    final user = useProvider(authProvider);
    return user.when(
      data: (user) {
        if (user == null) {
          return _signInButton();
        } else {
          return _signOutButton();
        }
      },
      loading: () => const CircularProgressIndicator(),
      error: (err, stackTrace) => Text(err.toString()),
    );
  }
```
{% endcode %}

次に`getCurrentUser`を確認してください。

ここで利用されている**FirebaseAuth.instance.currentUser**はキャッシュから現在ログイン中のユーザー情報を取得するメソッドです。

非同期的な処理のStream型と違い同期的な処理 (外部通信の待ち時間が発生しない処理) なので使い勝手が良く、別途用意しています。

使い方は普通のメソッドと同様です。`postmodal/postmodal_viewmodel.dart`の`addPost`を確認してみてください。

{% code title="postmodal/postmodal_viewmodel.dart" %}
```dart
  void addPost() {
    final user = getCurrentUser();
    if (user != null) {
      state = state.copyWith(
        user: user.displayName.toString(),
        uid: user.uid,
        photoURL: user.photoURL.toString(),
        timeStamp: DateTime.now(),
      );
    } else {
      state = state.copyWith(
        user: 'anonymous',
        uid: 'anonymous',
        timeStamp: DateTime.now(),
      );
    }
    addPostDB(state);
  }
```
{% endcode %}
