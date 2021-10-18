# 3. Firebaseとは

## Firebaseとは

アプリ開発に特化したクラウドサービスです。

* 細かいチューニングが不要
* アプリ開発に必要な機能が色々
* 無料枠が大きい

などの特徴があります。

![](https://markingcloud.github.io/handson-markdowne-editor\_part2-firebase/vuepress/docs/curriculums/firebase.png)

## 細かいチューニングが不要

使える機能が限定されている代わりに、細かいチューニングが不要です。\
[GCP のブログ (opens new window)](https://cloud.google.com/blog/products/compute/choosing-the-right-compute-option-in-gcp-a-decision-tree)中で次のように説明されています。

> GCP では、ユーザーが完全にコントロールできるもの（Compute Engine）から、高度に抽象化されたもの（Firebase や Cloud Functions）まで、さまざまなコンピュートサービスが提供されており、その管理や運用は Google が行っています。...\
> 純粋にコードに集中し、アプリケーションの API エンドポイントを公開するマイクロサービスを構築したい場合は、Firebase と Cloud Functions を使用します。

![](https://markingcloud.github.io/handson-markdowne-editor\_part2-firebase/vuepress/docs/curriculums/tree.png)

## アプリ開発に必要な機能が色々

アプリに開発に必要な機能が幅広く揃っています。

* Build
  * アプリ作成に必要なツール一式
    * **ホスティング：Hosting**
    * **データベース：Cloud Firestore**
    * ストレージ
    * 認証
    * ランタイム
* Release & Monitor
  * 監視と分析
    * アプリ分析
    * パフォーマンス監視
* Engage
  * ユーザーエンゲージメント
    * A/B テスト
    * プッシュ通知
    * メール通知

![](https://markingcloud.github.io/handson-markdowne-editor\_part2-firebase/vuepress/docs/curriculums/app.png)

## 無料枠が大きい

大きな無料枠が設定されており、小規模開発であれば完全無料で完結させることも可能です。\
払いすぎないようにアラート設定なども可能です。

[Firebase Pricing(opens new window)](https://firebase.google.com/pricing)

| プロダクト                                                                                                    | 無料(Spark プラン)                                              | 従量制(Blaze プラン)\*                                                                                                                                                  |
| -------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p><strong>Hosting</strong><br>ストレージ<br>Data transfer<br>Custom domain &#x26; SSL<br>プロジェクトごとに複数のサイト</p> | <p><br>10 GB<br>360 MB/day<br>✔<br>✔</p>                   | <p><br>$0.026/GB<br>$0.15/GB<br>✔<br>✔</p>                                                                                                                        |
| <p><strong>Cloud Firestore</strong><br>保存データ<br>下りネットワーク<br>ドキュメントの書き込み<br>ドキュメントの読み取り<br>ドキュメントの削除</p>  | <p><br>合計 1 GiB<br>10 GiB/月<br>2 万/日<br>5 万/日<br>2 万/日</p> | <p><br>$0.18/GiB<br><a href="https://cloud.google.com/firestore/pricing">Google Cloud pricing(opens new window)</a><br>$0.18/10 万<br>$0.06/10 万<br>$0.02/10 万</p> |

\*Spark プランの無料使用量を含む
