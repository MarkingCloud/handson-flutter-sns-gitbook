# 7. アプリをFirebaseにデプロイする

Hostingの良いこと書く

{% hint style="success" %}
### work

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
