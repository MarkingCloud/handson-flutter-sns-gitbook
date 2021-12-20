# 5. Codemagicを使ってみる

## 1. リポジトリを選択する

まずは簡単にCodemagicを使ってみましょう。

以下の操作を行ってください。

{% hint style="success" %}
**work**

* [**Codemagic**](https://codemagic.io/apps) へ移動する
* Add your first app を選択
* Connect repositoryにて「GitHub」を選択 > Next
* Set up applicationにて
  * GitHub integration > アカウント > all repositories > Save の順で選択
  * リロードボタン > 作成したレポジトリ > 「Flutter App」 > Finish の順で選択
{% endhint %}

{% embed url="https://scribehow.com/shared/__5E1X6kNxRy6MHpSt3RV0Mg" %}

## 2. Webでビルドしてみる

一番簡単なWebでビルドを行ってみます。

次の操作を行ってください。

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

