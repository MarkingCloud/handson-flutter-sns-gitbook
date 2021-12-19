# 4. 事前準備

## 1. リポジトリを用意する <a href="#1-rihoshitoriwosuru" id="1-rihoshitoriwosuru"></a>

利用するリポジトリを用意します。

次の操作を行ってください。

{% hint style="success" %}
**work**

* [**GitHub**](https://github.com) **** に移動する。
* Repositories > New を選択
* Repository name へ適当な名前を入力する。
* Public を選択する。
* Create Repository を選択する。
{% endhint %}

{% embed url="https://scribehow.com/shared/__BeBleVXqStC54KCXMVSMQg" %}

## 2. Gitpod でコードを開く <a href="#2-gitpod-tektowoku" id="2-gitpod-tektowoku"></a>

Gitpod を開いてコードをクローンしましょう。

次の操作を行ってください。

{% hint style="success" %}
**work**

* [**Gitpod に登録**](https://gitpod.io/#https://github.com/MarkingCloud/handson-flutter-sns/tree/part3-codemagic) して、管理画面に移動する。
* 必要な権限を許可する。
  * setting > Integrations > \[...] > Edit Permissions を選択。
  * 次の項目にチェックを入れ、Update Permissions を選択。
    * public\_repo
  * Authorize gitpod-io を選択し、パスワードを入力。
* Gitpod の管理画面はこれ以上操作しないため、タブを閉じる。
{% endhint %}

{% embed url="https://scribehow.com/shared/Gitpod___OcHEPD7vRr2xXYIW3d5Jjg" %}

{% hint style="info" %}
テーマをダークモードに変更したい場合は次の手順を実行してください。

* 歯車マーク > Color Theme > 好きなテーマを選択 (Dark+ default dark がオススメ)
{% endhint %}

## 3. リモートリポジトリを変更する

Gitpod 上から新しく作ったリポジトリへリモートリポジトリの設定を変更します。

次の操作を行ってください。

{% hint style="success" %}
**work**

* 先ほど作成したリポジトリの URL をコピーする。
  * **HTTPS**の方をコピー
* 次のコマンドを実行してリモートリポジトリを変更する。

```
git remote set-url origin コピーしたURL
git push -f origin HEAD
```
{% endhint %}

{% embed url="https://scribehow.com/shared/__hy7YWhz3T-i8ywoS3QZQcw" %}

ここまでで準備は完了です。
