# 5. Firebaseで認証連携を行う

## 1. Firebase Authを有効にする

## 2. サインイン・サインアウト機能を実装する

まずはFirebaseのAuth使った認証連携を実装しましょう。

次の操作を行ってください

{% hint style="success" %}
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
{% endhint %}



## 3. ユーザー情報を取得する処理を実装する

次の操作を行ってください

{% hint style="success" %}
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
