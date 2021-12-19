# 7. Firebaseと連携する(オプション)

Firebaseと連携させるために必要な設定を行います。

## 1. Firebase プロジェクトを作成する

Firebase のプロジェクトを作成しましょう。次の操作を行ってください。

{% hint style="success" %}
**work**

* [**Firebase コンソール**](https://console.firebase.google.com)を開く
* 「プロジェクトを追加」を選択。
* 好きなプロジェクト名を入力して「続行」を選択。
* **Google アナリティクスは無効**にして「プロジェクトを作成」を選択。
{% endhint %}

{% embed url="https://scribehow.com/shared/Firebase__k-dMJVzpS7q3sQlRiO8k-g" %}

## 2. プロジェクトとターミナルを紐づける

作成したプロジェクトを Gitpod に紐づけます。コンソールから次の操作を行ってください。

{% hint style="success" %}
**work**

* 次のコマンドを実行する。

```
firebase login --no-localhost --reauth
```

* 出力された URL をクリックする。
* Firebase にログインしているアカウントと同じアカウントを選択。
* 権限を確認して許可をクリックする。
* 出力された認証コードをコンソールに貼り付けてエンターを押下する。
* 次のコマンドを実行する。

```
firebase use --add
```

* 先ほど作成したプロジェクトのプロジェクトIDを選択する。
* 「what alias do you want to use for this project?」で適当なエイリアス名を入力する。
* 次のコマンドを実行し、正しいプロジェクトに (current) とついていることを確認する。

```
firebase projects:list
```
{% endhint %}

{% embed url="https://scribehow.com/shared/__2JrWAC0cTVCMsOBKLr2TTg" %}

## 3. フィンガープリントを取得する

Firebaseに登録するフィンガープリントを取得します。

次の操作を行ってください。

{% hint style="success" %}
**work**

* 次のコマンドを実行してパスワードを入力する。

```
keytool -list -v -alias upload -keystore ./upload-keystore.jks
```

* 出力されたSHI1の文字列をコピーする
{% endhint %}

![](<.gitbook/assets/image (7).png>)

## 4. アプリを登録する

FirebaseでAndroidアプリの登録を行います。

次の操作を行ってください。

{% hint style="success" %}
**work**

* コンソールトップ画面の Android マーク を選択
* 任意のアプリのニックネームを設定
* 「デバッグ用の署名証明書 SHI-1」に先ほどコピーした文字列を入力
* 「アプリを登録」を選択
* 2, 3, 4は何もせず「次へ」を選択
  * FlutterFireというライブラリで吸収しているため操作不要
{% endhint %}

{% embed url="https://scribehow.com/shared/__6dkiGLXdSJmC_UCKZqJNDQ" %}

## 5. Firebase Authenticationを有効にする

最初にFirebaseの管理画面からGoogleアカウントの認証機能を有効にしましょう。

次の操作を行ってください。

{% hint style="success" %}
**work**

* [**Firebase コンソール**](https://console.firebase.google.com)へ移動する
* Authentication > 始める > Sign-in method > 追加プロバイダ > Google を選択
* 「有効にする」を選択 > 「プロジェクトサポートメール」を選択 > 保存を選択
* 承認済みドメイン > ドメインを追加 を選択
* アプリを開いているページのURLを張り付け > 追加を選択
{% endhint %}

{% embed url="https://scribehow.com/shared/Firebase_Auth__P2kC24BFQfOxN0ZKPgHbvQ" %}

## 6. Firestoreを有効にする

Firestoreを有効にします。次の操作を行ってください。

{% hint style="success" %}
**work**

* [**Firebase コンソール**](https://console.firebase.google.com)へ移動する
* Firestore Database > データベースの作成 を選択
* テストモードで開始する > 次へ > asia-northeast1 > 有効にする を選択
{% endhint %}

{% embed url="https://scribehow.com/shared/FireStore__HI7dy8FUQxatkxRQwvun_A" %}

これでFirebaseとの連携も完了となります！
