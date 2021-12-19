# 1. ハンズオン概要

## **ハンズオン形式でFlutterアプリを作成しましょう**

![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/3\_codemagic\_2021\_0925\_2335.png)

今回のハンズオンではCodemagicを使い、**FlutterアプリのCI/CD**について学んでいきます。

次のトピックで進行していきます。

* Codemagicとは？
* Codemagicを使ってみる
* Androidアプリをデプロイするまでの流れ
* FlutterからFirebaseへ接続（Android）
* Androidアプリ自動ビルドフローの構築
* ビルド結果を検証する

## **事前準備**

ハンズオンの中で以下のサービスを利用します。\
スムーズに進行するため事前にアカウントの準備をお願いいたします。

#### [GitHub](https://github.com)

[![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/octocat.png)](https://github.com)

おなじみのGitのリモートリポジトリサービスです。基本無料です。\
プロジェクトを自分のリソースへFork/Pushするために必要になります。

※GitHubでは2021年8月13日から[パスワード認証が廃止](https://github.blog/2020-12-15-token-authentication-requirements-for-git-operations/)されています。\
※[トークンを発行](https://docs.github.com/ja/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)し、リポジトリにPushできることを確認しておいてください。

#### [Gitpod](https://www.gitpod.io)

[![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/gitpod.png)](https://www.gitpod.io)

ブラウザ上で仮想環境を立ち上げることのできるサービスです。基本無料です。\
ハンズオンでは開発環境を揃えるため、Gitpodに揃えた環境を立ち上げてコマンドやファイルの編集を行います。\
GitHubアカウントと連携させる形で登録いただければよいかと思います。

#### [Firebase](https://firebase.google.com/?hl=ja)

[![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/firebaselogo.png)](https://firebase.google.com/?hl=ja)

引き続き取り扱うサービスのFirebaseです。基本無料です。\
Googleアカウントと連携することでアカウントが作成されます。

#### [Codemagic](https://codemagic.io/start/)

[![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/codemagiclogo.png)](https://codemagic.io/start/)

今回取り扱うサービスのCodemagicです。基本無料です。\
GitHubアカウントと連携させる形で登録いただければよいかと思います。

#### [NoxPlayer](https://jp.bignox.com)

[![](https://github.com/MarkingCloud/connpass\_image/raw/main/flutter\_sns/noxplayer.png)](https://jp.bignox.com)

デスクトップ用のAndroidエミュレーターでアプリのインストールが必要です。 基本無料です。\
最後のビルド結果の動作確認に利用します。

※利用するためにCPUの仮想化を止める必要があります。\
※VirtualBoxやWSLを利用している方は注意してください。
