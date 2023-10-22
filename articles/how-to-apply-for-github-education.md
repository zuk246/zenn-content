---
title: "Github Education の申請方法"
emoji: "🏫"
type: "idea"
topics:
  - "github"
published: true
---
# はじめに
Github Educationとは、学生が無料でGithub Copilotなどを使えるサービスです。
中学生から大学生まで無料で使うことができるので、学生の方々はぜひ登録することをお勧めします。
https://education.github.com

## 条件
- 高等学校、中等学校、大学、ホームスクールまたはそれに類似した教育機関で、学位を取得できるコースに現在在籍している
- 学校が発行した検証可能なメールアドレスを持っているか、現在の在学状況を証明するドキュメントをアップロードしている
- GitHub 個人アカウントを作成します
- 最低でも 13 歳以上であること
> [Github Docs](https://docs.github.com/ja/education/explore-the-benefits-of-teaching-and-learning-with-github-education/github-global-campus-for-students/apply-to-github-global-campus-as-a-student) より引用

## Github Education の特典
- 学生の間は無料の GitHub Pro
- 貴重な GitHub Student Developer Pack パートナーのオファー
- 資格のある応募者向けの GitHub キャンパス エキスパート トレーニング


# 登録方法
## 学校のメールアドレスの追加
Githubの設定（サイドバーの`Settings`）から `Access` の `Emails` を開いてください。[ここ](https://github.com/settings/emails)です。
![](https://storage.googleapis.com/zenn-user-upload/baa8a32c2f30-20231022.png)
`Add email address` の欄に自分の学校のEmailを入力し、`Add` を押してください。

:::details なぜ新しいGithubアカウントを作らないのか
Github Docsによると複数Emailがある場合は、1つに[マージ](https://docs.github.com/ja/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-your-personal-account/merging-multiple-personal-accounts)することが推奨されています。
![](https://storage.googleapis.com/zenn-user-upload/00b77a102c4f-20231022.png)
:::


## Github Education のフォーム
[Github Education](https://education.github.com/benefits)から `Get student benefits` を押してください。
![](https://storage.googleapis.com/zenn-user-upload/c9fbf44e0329-20231022.png)

### 1ページ目
![](https://storage.googleapis.com/zenn-user-upload/910382d01297-20231022.png)
ほとんどの場合は、学校のメールアドレスを選択すると、自動で学校名が入力されると思います。
`Continue`を押すと位置情報を取得されます。この時、学校の近くで入力した方が申請が通る確率が上がるそうですが、学校のノートでGPSが使えないので、家からスマホでやりました。
学校の近くでスマホで入力するといいと思います。

```　:目的（例）
- To use Github Copilot X
- For more private use
- To use more GitHub Actions
- For learning
```

:::details 違う学校名が埋め込まれている場合
私が申し込んだ時は、学校のEmailを選択すると、自分が通っている学校ではない学校名が埋められていたので、[GitHub Education のヘルプ](https://support.github.com/contact/education?tags=dotcom-footer)からGithubに連絡しました。


``` :フォームの例
# 送信元：
学校のEmail

# GitHub Education を活用してどんなことができますか？：
選択した学校の情報が誤っているか、入力されていません

# 件名：
Another school name would be included in the form

# 説明：
I am a student at <Example School>. 
I am trying to enroll in Github Education's Student Developer Pack.
But, if I select Email for my school's domain, the name of another school(<別の学校名>) is entered in the "What is the name of your school?" field. 
Strictly speaking, the school for the <example.com> domain is "<Example School>", not "<別の学校名>".

My school information:
- school name: <Example School>
- domain: <example.com>
- home page: <example.com>
```

2時間後に公式からメールがあり、自分の学校名が埋め込まれるようになっていました。
:::

### 2ページ目
![](https://storage.googleapis.com/zenn-user-upload/15e6b3ec5e89-20231022.png)
`Take a picture` のボタンを押し、学生証の写真を撮ります。または、PCの場合は、学生証の写真をドロップします。この時、英訳をつけると申請が通る確率が上がるそうです。私は、学生証のみの写真で通りました。

:::message
何度も同じ写真をドロップするとエラーが起こりました。
:::
#### Payment information の設定
![](https://storage.googleapis.com/zenn-user-upload/2c12a5bda17f-20231022.png)
上のような画像が出る場合は、続けて読んでください。それ以外の方は、無視しても構いません。
:::details Payment information の設定
> （和訳）
> GitHub の請求情報に、所属書類に記載されているとおりのフルネームを正確に入力するまで、認証される可能性は高くありません。 支払い方法を追加する必要はありません。 再申請する前に、GitHub からログアウトして再度ログインする必要がある場合があります。

[Billing & plans / Payment information](https://github.com/settings/billing/payment_information) に移動します。必須になっている欄を埋めます。`Address` に自分の学校の名前（フォームの1ページ目に書いてあった名前）を入力します。
![](https://storage.googleapis.com/zenn-user-upload/ecd103217015-20231022.png)
:::

### フォーム完了
![](https://storage.googleapis.com/zenn-user-upload/cf0a922caff8-20231022.png)


## 待機
私の場合は、4日後にメールが来ましたが、ピークの時期（新しい学期の開始時期など）は、時間がかかるみたいです。~~海外によって新学期が異なるのでいつがピーク時かわからないですが...~~

## メールの確認
![](https://storage.googleapis.com/zenn-user-upload/ca9e03db5e2b-20231022.png)
このようなメールが来ると、Githubのプロフィールに `Pro` が付き、Github Educationの申請が完了しました。


# Github Copilot の登録
[Github Copilot](https://github.com/features/copilot) を開きます。
![](https://storage.googleapis.com/zenn-user-upload/f47fe500abcb-20231022.png)
`Start my free trial` をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/c61f1103b44a-20231022.png)
`Get access to Github Copilot` をクリックします。

![](https://storage.googleapis.com/zenn-user-upload/7036cfae54d7-20231022.png)
1. 公開コードに一致する提案：`Allow` を選択しました
2. GitHub が製品改善のために私のコード スニペットを使用することを許可：選択を外しました

`Save and get started` をクリックします。

## VScode のセットアップ
[この拡張機能](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot) をインストールすると使えるようになります。


# まとめ
以下の条件で申請が早く通ると思います。
- 学生証に英訳をつける
- 学校の近くで位置情報を共有する

また、エラーが起きた場合は、[GitHub Education Community](https://github.com/orgs/community/discussions/categories/github-education) を見るといいと思います。

