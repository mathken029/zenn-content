---
title: "法人向けSaaSの認証サービス選定"
emoji: "📝"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Cognito", "firebase", "Auth0", "SAML", "SaaS"]
published: false
---

# 概要

結論として ★★ の理由で ★★ のサービスを選定しました。

## きっかけ

現在は私は法人向けの SaaS を開発しようとしており、認証機能について無料枠の大きい Firebase Authentication を採用しようとしていました。
しかし、Firebase Authentication で SAML を利用する場合無料枠が制限されるとの記載を Firebase 上で見かけました。

![Firebase AuthenticationでSAMLを利用する場合の無料枠制限](/images/selecting-authentication-service-for-btob-saas/firebasePlan.png)

そのため、どうせ制限を受けるのであれば Firebase Authentication 以外のサービスも含めて比較しようと考えました。

## 参考資料

Web 検索ではあまり情報が出てこないため、情報がまとまっていそうな以下の書籍の情報をベースに必要に応じて各サービスのサイトを参照するようにします。

https://techbookfest.org/product/6354233804718080?productVariantID=5804352044269568

# 認証サービスの選定

## 選定基準

以下を選定基準としました。

- 法人で多く使われている SAML によるログインが行えるようにすること
- どの程度の収益となるかが開発開始時点では読めないため、できるだけ費用を抑えられること
- 攻撃を受けた際に顧客情報の保護やサービスの継続稼働を行うための対策機能を備えていること
- Azure AD からのプロビジョニングが行えること（設立予定の法人で Azure AD を使用する予定であるため）

## SAML でのログインが行えるか

## 費用を抑えられるか

## 攻撃への対策機能を備えているか

## Azure AD からのプロビジョニングが行えるか

# まとめ
