---
title: '【コピペ用】Cloud firestore セキュリティルールの関数'
emoji: '🌇'
type: 'tech' # tech: 技術記事 / idea: アイデア
topics: ['firebase', 'firestore']
published: true
---

# はじめに

Cloud firestore セキュリティルールは、Zod のよう簡単にはスキーマを作成できません。私は、Cloud firestore のセキュリティールールで UUID などの ID の判定、認証の判定などの関数をよく利用します。なので、個人的なメモ用として書こうと思います。

### やること

Cloud firestore セキュリティルールにコードを貼り付ける用のコードとそれについての説明を記載します。

### やらないこと

セキュリティルールについての構文や説明は入れません。

# ID 系の判定

`UUID` / `CUID` / `Firestore ドキュメントの自動生成 ID` の 4 つを判定する関数です。

## UUID v4 の判定

UUID の v4 は、`xxxxxxxx-xxxx-xxxx-4xxx-xxxxxxxxxxxx`で表現されます。したがって、`matches`関数の re2 の正規表現を利用して判別します。

```firestore-security-rules
function isUUIDv4(value) {
    return value.matches('[a-z0-9]{8}-[a-z0-9]{4}-4[a-z0-9]{3}-[a-z0-9]{4}-[a-z0-9]{12}');
}
```

## CUID の判定

正規表現を利用して判別します。CUID2 には、対応していないと思います。CUID のみの判定です。

```firestore-security-rules
function isCUID(value) {
    return value.matches('c[a-z0-9]{8}[0-9]{4}[a-z0-9]{4}[a-z0-9]{8}');
}
```

## Firestore ドキュメントの自動生成 ID の判定

Firestore の自動生成 ID について詳しく知りたい方は、こちらの記事がおすすめです。
https://qiita.com/yukin01/items/dcac3366adcf0fe827a3

特徴としては、20 文字の英語大小文字と半角数字のみです。それ以上判定しにくいと考えたので、簡易的な形にしました。

```firestore-security-rules
function isFirestoreAutoID(value) {
    return value.matches('[a-zA-Z0-9]{20}');
}
```

# 認証系の判定

:::message
[Firebase Authentication](https://firebase.google.com/docs/auth/?hl=ja) も併用してください。
:::

## 認証済であるかどうかの判定

```firestore-security-rules
function isAuthenticated() {
    return request.auth != null;
}
```

## 認証している UID の判定

```firestore-security-rules
function isAuthenticatedUID(uid) {
    return request.auth != null && request.auth.uid == uid;
}
```

## Email であるかの判定

Gmail 以外にも独自ドメインや Outlook のメールなども含めます。

```firestore-security-rules
function isFooEmail(value) {
    return value.matches('.+@.+[.].+');
}
```

## Gmail であるかどうかの判定

```firestore-security-rules
function isGmail(value) {
    return value.matches('.+@gmail.com');
}
```

## 認証している Email であるかどうかの判定

```firestore-security-rules
function isAuthenticatedEmail(email) {
    return  request.auth != null && request.auth.token.email == email;
}
```

# 参照

ドキュメントの参照とドキュメントの存在の確認についての関数です。

## ドキュメントの参照

```firestore-security-rules
function getData(collection, documentID) {
    return get(/databases/(default)/documents/$(collection)/$(documentID));
}
```

## ドキュメントの存在の確認

```firestore-security-rules
function isExist(collection, documentID) {
    return exists(/databases/(default)/documents/$(collection)/$(documentID));
}
```

# その他

## スキーマの定義　

```firestore-security-rules
function isValidFoo(data) {
    return data.size() == 4
    && 'foo' in data && data.foo is string
    && 'bar' in data && data.bar is number
    && 'baz' in data && data.baz is timestamp
    && 'qux' in data && data.qux is list;
}
```

## 国名コード

[ISO 3166-1 alpha-2 code](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) に沿って判定します。

```firestore-security-rules
function isCountryCode(value) {
    let all_country_code = ['IS', 'IE', 'AZ', 'AF', 'US', 'VI', 'AS', 'AE', 'DZ', 'AR', 'AW', 'AL', 'AM', 'AI', 'AO', 'AG', 'AD', 'YE', 'GB', 'IO', 'VG', 'IL', 'IT', 'IQ', 'IR', 'IN', 'ID', 'WF', 'UG', 'UA', 'UZ', 'UY', 'EC', 'EG', 'EE', 'ET', 'ER', 'SV', 'AU', 'AT', 'AX', 'OM', 'NL', 'GH', 'CV', 'GG', 'GY', 'KZ', 'QA', 'UM', 'CA', 'GA', 'CM', 'GM', 'KH', 'MP', 'GN', 'GW', 'CY', 'CU', 'CW', 'GR', 'KI', 'KG', 'GT', 'GP', 'GU', 'KW', 'CK', 'GL', 'CX', 'GD', 'HR', 'KY', 'KE', 'CI', 'CC', 'CR', 'KM', 'CO', 'CG', 'CD', 'SA', 'GS', 'WS', 'ST', 'BL', 'ZM', 'PM', 'SM', 'MF', 'SL', 'DJ', 'GI', 'JE', 'JM', 'GE', 'SY', 'SG', 'SX', 'ZW', 'CH', 'SE', 'SD', 'SJ', 'ES', 'SR', 'LK', 'SK', 'SI', 'SZ', 'SC', 'GQ', 'SN', 'RS', 'KN', 'VC', 'SH', 'LC', 'SO', 'SB', 'TC', 'TH', 'KR', 'TW', 'TJ', 'TZ', 'CZ', 'TD', 'CF', 'CN', 'TN', 'KP', 'CL', 'TV', 'DK', 'DE', 'TG', 'TK', 'DO', 'DM', 'TT', 'TM', 'TR', 'TO', 'NG', 'NR', 'NA', 'AQ', 'NU', 'NI', 'NE', 'JP', 'EH', 'NC', 'NZ', 'NP', 'NF', 'NO', 'HM', 'BH', 'HT', 'PK', 'VA', 'PA', 'VU', 'BS', 'PG', 'BM', 'PW', 'PY', 'BB', 'PS', 'HU', 'BD', 'TL', 'PN', 'FJ', 'PH', 'FI', 'BT', 'BV', 'PR', 'FO', 'FK', 'BR', 'FR', 'GF', 'PF', 'TF', 'BG', 'BF', 'BN', 'BI', 'VN', 'BJ', 'VE', 'BY', 'BZ', 'PE', 'BE', 'PL', 'BA', 'BW', 'BQ', 'BO', 'PT', 'HK', 'HN', 'MH', 'MO', 'MK', 'MG', 'YT', 'MW', 'ML', 'MT', 'MQ', 'MY', 'IM', 'FM', 'ZA', 'SS', 'MM', 'MX', 'MU', 'MR', 'MZ', 'MC', 'MV', 'MD', 'MA', 'MN', 'ME', 'MS', 'JO', 'LA', 'LV', 'LT', 'LY', 'LI', 'LR', 'RO', 'LU', 'RW', 'LS', 'LB', 'RE', 'RU'];
    return all_country_code.hasAny([value.upper()]);
}
```

## 言語コード

[ISO 639-1](https://ja.wikipedia.org/wiki/ISO_639-1%E3%82%B3%E3%83%BC%E3%83%89%E4%B8%80%E8%A6%A7) コードに沿って判定します。

```firestore-security-rules
function isLanguageCode(value) {
    let all_language_code = ['ab', 'aa', 'af', 'ak', 'sq', 'am', 'ar', 'an', 'hy', 'as', 'av', 'ae', 'ay', 'az', 'bm', 'ba', 'eu', 'be', 'bn', 'bh', 'bi', 'bs', 'br', 'bg', 'my', 'ca', 'ch', 'ce', 'ny', 'zh', 'cv', 'kw', 'co', 'cr', 'hr', 'cs', 'da', 'dv', 'nl', 'dz', 'en', 'eo', 'et', 'ee', 'fo', 'fj', 'fi', 'fr', 'ff', 'gl', 'ka', 'de', 'el', 'gn', 'gu', 'ht', 'ha', 'he', 'hz', 'hi', 'ho', 'hu', 'ia', 'id', 'ie', 'ga', 'ig', 'ik', 'io', 'is', 'it', 'iu', 'ja', 'jv', 'kl', 'kn', 'kr', 'ks', 'kk', 'km', 'ki', 'rw', 'ky', 'kv', 'kg', 'ko', 'ku', 'kj', 'la', 'lb', 'lg', 'li', 'ln', 'lo', 'lt', 'lu', 'lv', 'gv', 'mk', 'mg', 'ms', 'ml', 'mt', 'mi', 'mr', 'mh', 'mn', 'na', 'nv', 'nb', 'nd', 'ne', 'ng', 'nn', 'no', 'ii', 'nr', 'oc', 'oj', 'cu', 'om', 'or', 'os', 'pa', 'pi', 'fa', 'pl', 'ps', 'pt', 'qu', 'rm', 'rn', 'ro', 'ru', 'sa', 'sc', 'sd', 'se', 'sm', 'sg', 'sr', 'gd', 'sn', 'si', 'sk', 'sl', 'so', 'st', 'es', 'su', 'sw', 'ss', 'sv', 'ta', 'te', 'tg', 'th', 'ti', 'bo', 'tk', 'tl', 'tn', 'to', 'tr', 'ts', 'tt', 'tw', 'ty', 'ug', 'uk', 'ur', 'uz', 've', 'vi', 'vo', 'wa', 'cy', 'wo', 'fy', 'xh', 'yi', 'yo', 'za', 'zu'];
    return all_language_code.hasAny([value.lower()]);
}
```

# 終わりに

以上で、コピペ用のセキュリティールールの関数の紹介を終わります。
不明点や誤りを見つけた際にはお知らせ下さいますと幸いです。
