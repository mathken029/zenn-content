---
title: "法人向けSaaSのクラウド基盤(+データベース)の選定"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Firebase", "サーバレス", "IaaS", "BtoB"]
published: false
---

# 概要

## 参考資料

### クラウド基盤

https://qiita.com/h1guchi/items/4c4fc1b11580b76409b9

https://qiita.com/toto_inu/items/77e31e92f908a1fda8f7

### データベース

https://zenn.dev/nyarla/scraps/326424edf5d2eb

https://blog.kon-shou.com/posts/20200519/

### ホスティング

https://zenn.dev/catnose99/scraps/6780379210136f

https://zenn.dev/knagano/scraps/d772707b4909b0

# クラウド基盤の選定

自己資金であるため、費用を抑えるためにサーバレスを活用します。
また、ホスティングについてはデプロイのしやすさから Vercel も検討対象に含めています。
また、認証の観点では以下の比較も行っています。

★★ 認証サービスの記事の URL を貼る

## 選定基準

★ 認証も悩んでるけど、諸々を Firebase でいくか AWS でいくかをまだ悩んでる。
なんとなく AWS に傾いてきてるけど、構成がいまいち決まりきらないから費用の不安が拭えない。

- 方針 1.最初 Firebase でやって、スケールしたら AWS に切り替える

  - スケールしたときに切り替えるのが地獄そう

- 方針 2.最初から AWS でいく
  - 費用を抑える方法を探したとしても、個人資金の範囲で収まるかどうか

ホスティングの観点では、Vercel は無料プランで商用利用はできません。
https://vercel.com/pricing

# データベースの選定

## SQL か NoSQL か

NoSQL の個人的な最大のメリットは、フロントエンドから直接 DB にアクセスできるためバックエンドの開発や学習を行わないで良い点です。

## 選定基準

# ホスティングの選定

## 選定基準
