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

## 3. Codemagicの設定を変更する

取得したKeystoreをCodemagicに登録します。

またGitHubにコードがプッシュされるとBuildが動くようにもしておきます。

次の操作を行ってください。

{% hint style="success" %}
**work**

* Workflow settings へ移動する
* Build for platformsにて以下を選択
  * Androidのチェックを付ける
  * Webのチェックを外す
* Build triggersにて以下を選択
  * Trigger on push
* Buildにて以下を選択
  * Android build gormat でAPKを選択
  * ModeでReleaseを選択
* Distributionにて以下を選択
  * Enable Android code signingにチェックを付ける
  * Keystoreにダウンロードしたファイルをアップする
  * Keystore Password: **P@ssw0rd**
  * Key alias: **upload**
  * Key Password: **P@ssw0rd**
* Save changesを選択
{% endhint %}

{% embed url="https://scribehow.com/shared/Codemagic__kqYUlHqOQImiXusTZ4_ghA" %}



## 4. **build.gradleの設定を変更する**

ここで作成したKeystoreの情報をAndroidの**build.gradle**が読み込めるように設定を追記します。

次の操作を行ってください。

{% hint style="success" %}
**work**

* `android/app/build.gradle` のコメントアウトを解除 (3か所)
  * TODO keystorePropertiesの読み込み
  * TODO relese用Configの設定
  * TODO buildTypeの設定

{% code title="android/app/build.gradle" %}
```dart
// TODO keystorePropertiesの読み込み
def keystoreProperties = new Properties()   
def keystorePropertiesFile = rootProject.file('key.properties')
if (keystorePropertiesFile.exists()) {
    keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
}

android {
    ...

    // TODO relese用Configの設定
    signingConfigs {
        release {
            keyAlias keystoreProperties['keyAlias']
            keyPassword keystoreProperties['keyPassword']
            storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
            storePassword keystoreProperties['storePassword']
        }
    }

    // TODO buildTypeの設定
    buildTypes {
        release {
            signingConfig signingConfigs.release
        }
    }
}
```
{% endcode %}


{% endhint %}

## 5. コードをGitHubにPushする

ではコードをGithubにPushしてみて、Codemagicが正しく動くか見てみましょう

次の操作を行ってください。

{% hint style="success" %}
**work**

* GitHubにコードをPushする

```bash
git add .
git commit -m "Uncomment todo line"
git push origin HEAD
```
{% endhint %}

ビルドが完了し、アイコンが緑色になれば成功です！

![](.gitbook/assets/android\_build\_success.png)

## 6. ビルドしたAPKファイルを実行してみる

NoxPlayerを使ってAPKファイルの動作確認を行ってみましょう。

次の操作を行ってください。

{% hint style="success" %}
**work**

* APKファイルをCodemagicからダウンロードする
* NoxPlayerにAPKファイルをドラック＆ドロップする
* アイコンをクリックする
{% endhint %}

![](<.gitbook/assets/image (9).png>)

無事にアプリが開いたら成功です！
