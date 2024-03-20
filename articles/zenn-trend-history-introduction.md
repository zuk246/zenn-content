---
title: 'Zennで過去にトレンドになった記事・本を閲覧できる拡張機能を作りました'
emoji: '📋'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['zenn', 'hono', 'cloudflare', 'chrome拡張']
published: true
---

https://chromewebstore.google.com/detail/cclhgjnllleppaplaonmpdmdgngnodjf

![](https://storage.googleapis.com/zenn-user-upload/708b723f32c0-20240319.png)

![](https://storage.googleapis.com/zenn-user-upload/d73f108eedf2-20240319.png)

:::message
非公式の拡張機能です。
:::

# 概要

Zenn で過去にトレンドになったテック記事、アイデア記事、本を表示する Chrome 拡張機能です。[ここ](https://chromewebstore.google.com/detail/cclhgjnllleppaplaonmpdmdgngnodjf)からインストールできます。2024/03/07 からの[Zenn の RSS](https://zenn.dev/feed)で取得できるデータをランダムで表示します。正確には、今日のトレンド以外からランダムで 12 個選択します。

Zenn のルートページの Featured の下に表示されます。
気になった方は、インストールしてみてください！

## RSS を使った理由

Zenn には、[正式に公開されていない API](https://zenn.dev/manase/scraps/489f556f7ff15b) があります。`https://zenn.dev/api/**`を叩くと記事などを取得できますが、公式のドキュメントがなく、バージョンが変わってしまうと使えなくなってしまうことやフィードリーダーなどで RSS の方が多く叩かれている気がするので、RSS を使いました。（Zenn にも迷惑をかけないためにも）

# システム構成

![](https://storage.googleapis.com/zenn-user-upload/ef9ed91d32fa-20240319.jpg)
_システム構成_

⇧ こういうのあまり書かないので矢印とか違うかもしれません

## 拡張機能

-   React
-   Emotion
-   Vite
-   Typescript

## API（バックエンド）

-   Hono

## スケジュール（バックエンド）

Workers の Cron Triggers を使って毎日の 0 時に自動実行します。
RSS で 20 個のトレンドの記事や本を取得し、D1 に保存しています。

# API

API は公開してます。
拡張機能は、`https://zenn-trend-history.zuk246.net/v1/random`を使っています。
https://github.com/zuk246/zenn-trend-history/blob/main/doc/api.md

# リポジトリ

MIT ライセンスで公開しています。
https://github.com/zuk246/zenn-trend-history
