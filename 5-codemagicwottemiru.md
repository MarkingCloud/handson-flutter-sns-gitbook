# 5. Codemagicを使ってみる

## 1. リポジトリを選択する

まずは簡単にCodemagicを使ってみましょう。

以下の操作を行ってください。

{% hint style="success" %}
**work**

* [**Codemagic**](https://codemagic.io/apps) へ移動する
* Add application を選択
* Select teamにて「Personal account」を選択 > Next
* Connect repositoryにて「GitHub」を選択 > Next
* Set up applicationにて作成したレポジトリを選択 > 「Flutter App」を選択 > Finish
{% endhint %}

{% embed url="https://scribehow.com/shared/__lMkPUn2nTGKyp_aO0Szckw" %}

## 2. Webでビルドしてみる

一番簡単なWebでビルドを行ってみます。

{% hint style="success" %}
**work**

* Workflow settings へ移動する（上の手順後に自動遷移するはず）
* Build for platformsにて以下を選択する
  * Androidのチェックを外す
  * iOSのチェックを外す
  * Webのチェックを付ける
* BuildにてFlutterのバージョンを選択
  * Flutter version は **2.6.0-11.0.pre**
* Save changes > Start build を選択
{% endhint %}

{% embed url="https://scribehow.com/shared/Web__zUudi1qiRkmO9cByj4Q63g" %}

たったこれだけの操作でBuild設定が可能です。

Build結果は**Artifacts**から取得できます。

![](.gitbook/assets/web\_build\_success.png)

