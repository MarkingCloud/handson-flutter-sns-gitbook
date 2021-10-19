# 6. Flutterでの状態管理について

次に投稿を表示する機能と、投稿を送信する機能を実装しますが、その前にFlutterの状態管理事情について説明しておきます。

## 1. 状態管理ツールのトレンド

純粋なFlutterで状態管理を行いたい場合、**StatefullWidget**というWidgetを使って実装を行います。

ただし**StatefullWidget**は**ステータスをバケツリレーのように運ぶ必要がある**という欠点があり、プロジェクトが大きくなるほどコードが煩雑になる傾向がありました。

そこで有志の状態管理用のライブラリが開発されており、次のようにトレンドが移り変わっています。

* StatefulWidget
* InheritedWidget
* Provider + BLoC&#x20;
* Provider + ChangeNotifier
* Provider + StateNotifier + freezed
* **Riverpod + StateNotifier + freezed + Flutter Hooks** <mark style="color:red;">★イマココ</mark>

今回は現在最も使い勝手が良いとされている★の構成で状態管理を実装していきます。

## 2. 各ライブラリの説明

これらのライブラリですが、各ツールの役割を理解する必要がある上に、色々な情報が混在しているため、学習が結構大変でした。(Flutterを勉強するうえで一つの障壁になってるのと思います。)

まずは情報を整理するためにここで各ライブラリの役割を軽く説明して、次の項で実際にコードを書いて使い方を確かめる流れで、なるべく分かりやすく説明しようと思います。

### ![](<.gitbook/assets/riverpod (1).png>)Riverpod

状態管理のデファクトスタンダードになってるライブラリで、コレの登場でバケツリレー問題が解消しました。

Riverpodは**○○Provider**という名前でステータスを定義でき、この**Providerがデータの実態を保持**します。Storeと言った方がしっくりくる人もいますでしょうか。

### ![](<.gitbook/assets/flutterhooks (1).png>)Flutter Hooks

React Hooks と同じような使い方ができるライブラリで、複雑な型の取り扱いが簡単になります。

ここでは**Riverpodへのアクセスを簡単に行う**ために利用します。

### ![](<.gitbook/assets/freezed (1).png>)freezed

immutable(変更不可能)なクラスを作成したいときに利用するライブラリです。

クラスを作成する時に、おまけで**便利な関数を自動で生成**してくれます。そのうちの一つを今回使います。

### &#x20;![](<.gitbook/assets/statenotifier (1).png>)StateNotifier

ステータスが変更されたときに自動で通知を送ってくれるライブラリです。Flutterでステータスを動的に扱いたいときは、変更ポイントの再ビルドが必要なためこちらのライブラリが必要になります。

**ステータスが変更されるメソッドはここで記述**します。
