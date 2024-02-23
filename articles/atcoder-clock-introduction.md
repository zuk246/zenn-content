---
title: 'タイマーが完了するとAtcoderの問題を提案するアプリを開発しました'
emoji: '🎉'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['atcoder', 'react', 'cloudflare']
published: true
---

Atcoder の問題を提案してくれるタイマーアプリです。

https://clock.zuk246.net

![](https://storage.googleapis.com/zenn-user-upload/5e265a90fdc7-20240219.png)

## 機能

普通のタイマーに Atcoder の問題の提案してくれる機能がついたアプリです。提案される問題は、ID で設定した Atcoder アカウントが現在から 2 週間までの提出した中からランダムで選んでいます。API は、[AtCoder Problems API](https://github.com/kenkoooo/AtCoderProblems) を使っています。

![](https://storage.googleapis.com/zenn-user-upload/13c4750cd26d-20240219.png)

## バックグラウンドで動作

タイマーは、Web Worker を使用してブラウザのバックグラウンド動作しています。なので、別タブで作業している時でも通知でタイマーが完了したことをお知らせします。

## UI/UX

正直現在のデザインだと使いにくいと感じる人もいると思います。ユーザビリティはあまり考えませんでした。それより Web で検索するとでるタイマーのように白い背景に数字が書かれているデザインだと Atcoder の問題を解くモチベーションが上がりません。また、個人的にグラスモーフィズムを取り入れたデザインにしてみたい気持ちもありました。

# 技術

-   TypeScript
-   Vite(React)
-   TailwindCSS
-   HeadlessUI
-   React Hook Form

## デプロイ

Cloudflare Pages にデプロイしました。無料枠が大きく無料で運用できると思ったからです。Github Pages や Netlify などもありますが、Cloudflare を個人的に使ってみたかったのでデプロイしてみました。

## パフォーマンス

![](https://storage.googleapis.com/zenn-user-upload/4a1c883c04e4-20240221.png)

思ったより Lighthouse のスコアがよくホッとしました。

# リポジトリ

MIT ライセンスで公開しています。
https://github.com/zuk246/atcoder-clock

# これから

時間などのセットを簡単に行えるようにしたら別のアプリを開発しようと考えています。もし機能を追加したい場合は、issues を立ててくれると助かります。このような開発は初めてなので間違ったことをしていたら教えてください。
