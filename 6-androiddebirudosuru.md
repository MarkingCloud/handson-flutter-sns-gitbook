# 6. Androidでビルドする

## 1. FlutterアプリをAndroidでリリースするまで

Androidでアプリをビルドしてリリースするまでに必要な以下のドキュメントで説明されています。

* [**Androidアプリをビルドしてリリースする**](https://docs.flutter.dev/deployment/android)****

今回はそのうち、

* アプリに署名する
* リリース用のアプリの構築

をCodemagicを使って実施します。

## 2. Keystoreを取得する

アプリに署名を行うためのKeystoreを取得します。

次の操作を行ってください。

{% hint style="success" %}
**work**

* Keystoreを作成する

```
keytool -genkey -v -keystore ./upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

* 以下の通り情報を入力する
  * Enter keystore password: **P@ssw0rd**
  * Re-enter new password: **P@ssw0rd**
  * What is your first and last name?: **(何も入力せず) Enter**
  * What is the name of your organizational unit?: **(何も入力せず) Enter**
  * What is the name of your organization?: **(何も入力せず) Enter**
  * What is the name of your City or Locality?: **(何も入力せず) Enter**
  * What is the name of your State or Province?: **(何も入力せず) Enter**
  * What is the two-letter country code for this unit?: **(何も入力せず) Enter**
  * Is \~\~ \[no]: **yes**
* 作成されたファイルを右クリック > Download
{% endhint %}

{% embed url="https://scribehow.com/shared/Keystore__f9aHx906TjOS8AfTB4pXMg" %}





