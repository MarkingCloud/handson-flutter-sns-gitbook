# 3. Flutterとは

## Flutterとは

**Flutter**とはGoogleが開発している**クロスプラットフォーム**のアプリケーションフレームワークです。\
1つのソースで複数のプラットフォーム(Mobile, Web Desktop)に対応したアプリの開発が可能です。

利用されている言語は**Dart**でこちらもGoogleが開発している言語です。

[Google Ads や Google Assistant ](https://flutter.dev/showcase)などGoogle自身もFlutterを導入していたり、力を入れているようです。\
また日本では[TOYOTAがFlutterを導入](https://techplay.jp/column/1516)して少し話題になっていました。

## Flutterの特徴

Flutterの特徴は次の3つです（公式より）

### 素早く開発できる

Flutterは**ホットリロード**で開発することが可能で、動作確認の時間を大幅に削減することが出来ます。\
(残念ながらWebで実行する場合はホットリロードは適用されません。代わりに自動リスタートします。)

{% embed url="https://flutter.dev/assets/videos/FastDev.mp4" %}

### 美しいUIを簡単に利用できる

Flutterには標準で**Material Design**のライブラリが入っており、簡単に利用することが出来ます。

### ネイティブ言語と同等のパフォーマンス

Flutterは特殊なモジュールにラップせず、AndroidとiOSそれぞれの特性に合わせてビルドされるため、\
ネイティブでのパフォーマンスをフルに活用することが出来ます。
