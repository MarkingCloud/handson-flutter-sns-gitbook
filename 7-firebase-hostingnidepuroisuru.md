# 7. Firebase Hostingにデプロイする

## 1. Firebase Hostingとは

![](https://markingcloud.github.io/handson-markdowne-editor\_part2-firebase/vuepress/docs/curriculums/hosting2.png)

Firebase HostingとはFirebaseの持っているホスティングサービスです。

コマンド一つで簡単にデプロイできる上に、デフォルトで次のようなことを自動で行ってくれます。

* ドメインの付与
* TLS による暗号化（HTTPS 化）

ホスティング対象となるディレクトリは`firebase.json` で指定します。

{% code title="firebase.json" %}
```json
{
  "firestore": {
    "rules": "firestore.rules",
    "indexes": "firestore.indexes.json"
  },
  "hosting": {
    "public": "build/web", // ここで対象ディレクト指定
    "ignore": [
      "firebase.json",
      "**/.*",
      "**/node_modules/**"
    ]
  }
}
```
{% endcode %}

## 2. デプロイしてみる <a href="1-sassokutefuroishitemiru" id="1-sassokutefuroishitemiru"></a>

それでは Hosting にデプロイしてみましょう。

Gitpod のコンソールから次の操作を行ってください。

{% hint style="success" %}
**work**

* FlutterのコードをWeb用にビルドする。

```bash
flutter build web
```

* Firebase Hostinにデプロイする。

```bash
firebase deploy --only hosting
```
{% endhint %}

発行されたURLにアクセスしてみてください。

無事にビルド後のFlutterアプリが開けば成功です。
