---
title: '𝕏のいいね欄が見えなくなったので、VSCodeからBlueskyにポストできる拡張機能を作った'
emoji: '🦋'
type: 'tech'
topics: ['vscode', '拡張機能', 'bluesky', 'twitter']
published: true
---

こんにちは。

最近𝕏（旧Twitter）でのポストのいいねが見られなくするという改悪（賛否両論がありますが）がありましたね。そこで、VS CodeからBlueskyに投稿できる拡張機能を作ったので紹介します。

Blueskyでもいいね欄が見られなくなっていると誤解されている方もいらっしゃると思いますが、公式クライアント以外では見られます。[API](https://docs.bsky.app/docs/api/app-bsky-feed-get-actor-likes)も存在します。

![スクリーンショット](https://storage.googleapis.com/zenn-user-upload/869f42ca2cc1-20240624.png)
*スクリーンショット*

Bluesky用のVS Codeクライアントです。投稿、タイムライン、通知、いいね、アカウント情報などの機能があります。マルチカラムやステータスバーもサポートしています。オープンソースとして公開していますので、ぜひ新しい機能の追加や改善の提案をお願いします。
GitHubのスターもお願いします🙏

https://marketplace.visualstudio.com/items?itemName=zuk246.blueriver

https://github.com/zuk246/BlueRiver


# 🧭 経緯

BlueskyのAPIが公開されており、Bluesky用のクライアント作れると思ったのがきっかけです。スマホやWebのクライアントも良さそうだと思いましたが、もうすでに存在していました。ですが、VS Codeクライアントを開発すればVS Codeで開発中でも気軽にBlueskyへポストやタイムラインが見られると思いました。また、VS Codeの拡張機能開発の日本語記事もそこそこ充実していました。

# 🛠️ 使った技術

### 言語

TypeScriptを使っています。JavaScriptからTypeScriptを触るとVS Codeからの提案が増え、エラーも少なくなったのでもうJSを使えなくなりました。WebViewのスクリプトのみJSのみの対応ですが（最初TSでやってたので、エラーで数時間消えました）。

### ライブラリなど

ライブラリは、VS Code拡張機能用のライブラリとBlueskyの操作をするライブラリを使っています。本当は、Reactとかを使ってWebViewを開発したかったのですが、使うと複雑になってしまうので使いませんでした。

# 🖥️ スクリーンショット

![通知とタイムライン](https://storage.googleapis.com/zenn-user-upload/be639b89fc87-20240624.png)
*通知とタイムライン*

![タイムライン](https://storage.googleapis.com/zenn-user-upload/8ea435b20fd2-20240624.png)
*タイムライン*


# 🦋 そもそも Bluesky とは？

Blueskyは、元々Twitter内での2019年からあるプロジェクトであり、2021年8月に独立し、法人化しました。グラバーがCEO、ドーシーが取締役に就任しました。

Blueskyは、𝕏の中央集権型とは違い、分散型のSNSです。ユーザーが情報の投稿・収集・共有などができます。また、それぞれ独自のサーバーを持ち、それら複数のサーバーが協調しあって1つのSNSを構成するサービスとなっています。

分散型SNSと聞くとMastodonやNoStrと思い浮かぶかもしれませんが、AT Protocol (Authenticated Transport Protocol)と呼ばれるプロトコルを使用しており、「いいね」や「共有」などと言った個人データはリポジトリ内に保存される仕組みとなっているようです。

こちらの記事で詳しく解説されてあります。
https://qiita.com/gpsnmeajp/items/1413960dd2cf4488ccd5

Blueskyの機能の詳しい説明は、こちらの記事で解説されています。

https://zenn.dev/kato_shinya/articles/lets-try-bluesky-social

## サードパーティ製のアプリ

Twitterと異なり、Blueskyは対照的で自由にタイムラインのアルゴリズムを改変し独自のアプリの作成ができます。なので、さまざまなサードパーティ製アプリを利用・開発できます。

Bluesky公式の [Community Showcase](https://docs.bsky.app/showcase) からサードパーティ製のアプリやライブラリ、拡張機能などの一覧を見られます。この拡張機能も登録をGitHubからしました。


![Heatmap](https://storage.googleapis.com/zenn-user-upload/ff4ca43bcc3a-20240623.png)
*[Bluesky Posts Heatmap Generator](https://bluesky-heatmap.fly.dev/)で生成*


サードパーティ製のアプリは、142件登録されているようで、GitHubの草のような画像を生成することも可能です。AndroidやIOSの非公式クライアントなどもあり、私は`Graysky`というクライアントをスマホで使っています。

𝕏のフォロー・フォロワーからBlueskyのアカウントを探す拡張機能もあります。

https://zenn.dev/ryo_kawamata/articles/2f0b96f8eb5179

![](https://storage.googleapis.com/zenn-user-upload/eb0c835b2f67-20240623.png)
*[Bluesky](https://bsky.social/about/blog/12-21-2023-butterfly)より引用*

「既存のSNSより使いやすさ・拡張性・機能の開発者エクスペリエンスで上回る」「アプリ開発とプロトコル開発を統合する」「アイデアやデザインがうまくいかない場合はすぐに捨てる」という原則が採用されているみたいです。

## 最近のBluesky
![](https://storage.googleapis.com/zenn-user-upload/4e1a037991e5-20240623.png)
*[The Pragmatic Engineer](https://newsletter.pragmaticengineer.com/p/bluesky)から引用した画像を日本語化してみました*

2024年2月に招待制が終了したのでBlueskyに登録した人も多いと思います。下のいいねの数のグラフでも2月に跳ね上がっていることがわかります。

現在590万人のユーザーがBlueskyに登録してしています。

![](https://storage.googleapis.com/zenn-user-upload/bc836ae9de79-20240623.png)
*[日単位のいいねの数のグラフ](https://bsky.jazco.dev/stats)*


先月（5月）ジャック・ドーシーがBlueskyの取締役会から降りてしまいました。理由として「（Twitterが犯してきた）あらゆる過ちを繰り返しているから」だそうですが、私は他の分散型SNSとよりAPIやドキュメントなどが充実しており使いやすいのでBlueskyを使い続けようと思っています。

# 🚀 機能

![タイムラインとZennの執筆](https://storage.googleapis.com/zenn-user-upload/ff611793caf4-20240624.png)
*タイムラインとZennの執筆*

- ポスト
- タイムライン
- 通知
- いいね
- アカウント情報
- ステータスバー
  通知数を確認でき、ステータスバーをクリックすると拡張機能で使えるコマンド一覧を出せます。
- マルチカラム + レスポンシブ
  作業しながらタイムライン、通知を眺めることができます。
- 多言語表示
  現在、英語、日本語、スペイン語、中国語（簡体字）、フランス語の5か国語対応しています。

# ⏩ これから

まだまだ基本的な機能しか付けられていないので、フィード・リストの表示やタイムラインやから直接いいねするなどの機能をつけ、しっかりしたクラアントにしたいと思っています。

ここまで読んでいただきありがとうございました！

https://bsky.app/profile/zuk246.net

https://marketplace.visualstudio.com/items?itemName=zuk246.blueriver


# 📚 参考文献

https://ja.wikipedia.org/wiki/Bluesky

https://gigazine.net/news/20240502-building-bluesky/

https://news.yahoo.co.jp/articles/b2da0937df3d9bd9166ed7ecf811e6c70954f013
