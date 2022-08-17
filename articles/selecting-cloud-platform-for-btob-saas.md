---
title: "法人向けクラウドサービスのインフラ(ホスティング・DB・認証・サーバレスアーキテクチャ)選定"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Firebase", "Amplify", "SaaS", "BtoB"]
published: true
---

# 概要

結論だけ知りたい方のために先に書くと、 以下のサービスを選定しました。
結果的に Amplify 系のサービスで固まりましたが、法人向けサービスとして必要と考える要件で各サービスをできるだけ比較しました。

- ホスティング：[AWS Amplify ホスティング](https://aws.amazon.com/jp/amplify/)
- DB：[Amazon DynamoDB](https://aws.amazon.com/jp/dynamodb/)
- 認証：[Amazon Cognito](https://aws.amazon.com/jp/cognito/)
- サーバレスアーキテクチャ：[Amplify](https://aws.amazon.com/jp/amplify/)

ただ、開発していく中でとても費用が高かったり使いづらいようなポイントが見つかれば変えるようにします。

## きっかけ

現在は私は法人向けの クラウドサービス(BtoB SaaS) を開発しようとしており、認証機能について無料枠が大きく個人開発でも多く使われている Firebase Authentication を採用しようとしていました。
しかし、Firebase Authentication で SAML を利用する場合無料枠が制限されるとの記載を Firebase 上で見かけました。

![Firebase AuthenticationでSAMLを利用する場合の無料枠制限](/images/selecting-cloud-platform-for-btob-saas/firebasePlan.png)

そのため、どうせ制限を受けるのであれば Firebase Authentication 以外のサービスも含めて比較しようと考えました。

## 選定の全体の考え

以下ではホスティング・データベース・認証の 3 要素をそれぞれ選定した後、その内容を元にサーバレスアーキテクチャを選定します。
できるだけサーバレスにしたい理由は、開発するサービスの収益がどの程度となるかわからないため費用を抑えたいことと
開発者は私一人となるため運用周りの作業をできるだけ減らしたいためです。

また、Google Cloud Platform(GCP)や Azure のサービスを入れていないのはそれらを使用する多くのケースでは
AWS サービスでも対応できるケースが多いと理解しております。
体感ですが、AWS はコミュニティーが盛んであり AWS で同様のことができるのであれば AWS を選択するという考えです。

# ホスティングサービスの選定

## 参考資料

https://zenn.dev/catnose99/scraps/6780379210136f

https://zenn.dev/knagano/scraps/d772707b4909b0

## ホスティングサービスの選定基準

以下を選定基準としました。上から順に優先順位が高いです。

- 費用が抑えられるか
- 開発の初心者でも簡単にデプロイできるか
- サーバレスアーキテクチャとの親和性が高いか

## ホスティングサービスの選定候補

他にもホスティングサービスはありますが、プログラミングの学習の過程で操作したものや人から良いと言われて試したみたサービスのみを選んでいます。

- [Vercel](https://vercel.com/dashboard)
- [Firebase Hosting](https://firebase.google.com/docs/hosting?hl=ja)
- [AWS Amplify ホスティング](https://aws.amazon.com/jp/amplify/)

## ホスティングサービスの選定結果

結論としては下記となります。

- サーバレスアーキテクチャとして Firebase を採用した場合は Firebase Hosting
- AWS Amplify を選んだ場合は AWS Amplify ホスティング

以下、各選定基準に沿った説明を行います。

### 費用を抑えられるか

以下の観点から、無料枠で費用が抑えられる Firebase Hosting 及び AWS Amplify が残ります。

|                  | [Vercel 料金](https://vercel.com/pricing) | [Firebase Hosting 料金](https://firebase.google.com/pricing?hl=ja#hosting) | [AWS Amplify ホスティング料金](https://aws.amazon.com/jp/amplify/pricing/?nc=sn&loc=4) |
| ---------------- | ----------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| 無料プラン       | 商用利用不可                              | ストレージ 10 GB<br>データ転送 360 MB/日                                   | 15 GB のホスティングサービス/月など                                                    |
| 最小の有料プラン | $20<br>1 ユーザ / 月                      | ストレージ $0.026/GB<br>データ転送 $0.15/GB                                | ホスティングサービス<br>1 GB あたり$0.15 など                                          |

### 開発の初心者でも簡単にデプロイできるか

法人向けクラウドサービスがどんどん出てきて市場が盛り上がってほしいため、経験が少ない人にも勧められるサービスを自分でも使っていきます。

使い勝手について 3 サービスとも使ってみた結果、特に詰まることなくデプロイができたため同列という結論です。
ただ、Vercel でデプロイできていた React のプログラムが AWS Amplify ではできなかったこともありました。
そのため、多少作りがまずいものでもデプロイできるという点では Vercel が少し優れているという感触です。

### サーバレスアーキテクチャとの親和性が高いか

ホスティングは特にサーバレスアーキテクチャとの関係が密接であるため、重視したいポイントです。
各ホスティングサービスは、そのサービスが内包されるサーバレスアーキテクチャと親和性が高いため、
Firebase というサーバレスアーキテクチャとして採用した場合は Firebase Hosting を、AWS Amplify を選んだ場合は AWS Amplify ホスティングを選ぶことになります。

サーバレスアーキテクチャはこの後決めるため、ここではどのホスティングサービスを使うかは決まらないということになります。

# データベースの選定

## 参考資料

https://zenn.dev/nyarla/scraps/326424edf5d2eb

https://blog.kon-shou.com/posts/20200519/

https://dev.classmethod.jp/articles/2020-modern-application-db/

https://dev.classmethod.jp/articles/aws-summit-online-2020-day1-track3-1130-1200/

## データベースの選定基準

以下を選定基準としました。上から順に優先順位が高いです。

- 費用が抑えられるか
- フロントエンドから呼び出しやすいか

## データベースの選定候補

選定候補としては、コストや運用作業の効率化の観点からサーバレスかつフロントエンドから直接 DB にアクセスできてバックエンドの開発や学習を行わないで良いものを選出します。
特に NoSQL を選ぶというわけではないのですが、サーバレスで主要なサービスとして以下を候補とします。

- [Cloud Firestore](https://firebase.google.com/docs/firestore)
- [Amazon DynamoDB](https://aws.amazon.com/jp/dynamodb/)
- [Supabase](https://supabase.com/)

## データベースの選定結果

結論として、Amazon DynamoDB を選定しました。
以下、各選定基準に沿った説明を行います。

### 費用が抑えられるか

Amazon DynamoDB については、料金体系が 2 つありますがアクセス数が読めない初期は従量課金のプラン(オンデマンドキャパシティーモード)として、
必要に応じて固定課金のプラン(プロビジョニング済みキャパシティーモード)に変更することを想定します。
そのため、以下は従量課金のプランを記載します。

比較をシンプルにするため、各サービスでそれ以外の条件はあるのですが、以下を比較しています。
また、22/08/16 時点での東京リージョンの料金を記載します。

- Cloud Firestore 及び Amazon DynamoDB ：読取り・書き込みの費用
- Supabase では読取り・書き込みと近い概念であるユーザー数の費用

|                  | [Cloud Firestore 料金](https://firebase.google.com/docs/firestore/pricing#tokyo)                                             | [Amazon DynamoDB 料金](https://aws.amazon.com/jp/dynamodb/pricing/on-demand/)                                                   | [Supabase 料金](https://supabase.com/pricing)       |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| 無料プラン       | ドキュメントの読み取り 50,000/日<br>ドキュメントの書き込み 20,000/日                                                         | 読取り・書き込み自体に無料枠はなく、ストレージ容量などに無料枠有り                                                              | 50,000 monthly active users：$0/month per project   |
| 最小の有料プラン | ドキュメントの読み取り：ドキュメント 100,000 点あたり $0.038<br>ドキュメントの書き込み：ドキュメント 100,000 点あたり $0.115 | 読み出し要求単位 (RRU)：読み出し要求ユニット 100 万あたり $0.285<br>書き込み要求単位：書き込み要求ユニット 100 万あたり $1.4269 | 100,000 monthly active users：$25/month per project |

Cloud Firestore 及び Supabase には無料枠があり、サービスの初期では無料枠の範囲に収まりそうです。
また、Amazon DynamoDB には無料枠はありませんが、サービスの初期においてはそれほど問題にならない費用であると予想できます。
そのため、ここでは特に落ちるサービスは無いということになります。

### フロントエンドから呼び出しやすいか

Cloud Firestore については、実際に React から呼び出してみて特に迷うことはありませんでした。

Amazon DynamoDB について、実際に動かしてみてはいないのですが以下を見る限り Cloud Firestore と大きく呼び出しやすさに違いは無いと理解しました。
強いて言うなら、初期設定のステップが多いかなという点ですがあまり問題にならないでしょう。

https://dev.classmethod.jp/articles/react-amplify-appsync-dynamodb-tutorial/

Supabase について、SQL ですが SQL を直接書かずに下記のように他のサービスと同様にフロントエンドからデータの取得が可能と理解しました。
https://reffect.co.jp/html/supabse-beginner#React

そのため、呼び出しやすいかの観点で差異は無いと考えます。

### SQL ⇔ NoSQL 間の移行ができるか

何らかの理由で SQL ⇔ NoSQL 間で移行することになった際に移行方式が確立されているかを確認します。

Cloud Firestore については、SQL への移行についての明確な情報は見つかりませんでした。

Amazon DynamoDB の場合は公式の機能ではないですが、以下のように移行する方法があります。
https://qiita.com/homoluctus/items/fe2f9eee7f9e91bd272e

Supabase については、NoSQL のサービスなどへの移行についての明確な情報は見つかりませんでした。

そのため、移行についての明確な情報が見つかったのは Amazon DynamoDB のみです。

# 認証サービスの選定

## 参考資料

Web 検索ではあまり情報が出てこないため、情報がまとまっていそうな以下の書籍の情報をベースに必要に応じて各サービスのサイトを参照するようにします。

https://techbookfest.org/product/6354233804718080?productVariantID=5804352044269568

## 認証サービスの選定基準

以下を選定基準としました。上から順に優先順位が高いです。

- セキュリティと利便性の観点から OIDC が使えるか
- 攻撃を受けた際に顧客情報の保護やサービスの継続稼働を行うための対策機能を備えているか

## 認証サービスの選定候補

参考資料の書籍にメインで取り上げられているサービスを対象とします。
ただ冒頭記載の通り、GCP 及び Azure のサービスは取り上げません。

- [Firebase Authentication](https://firebase.google.com/docs/auth?hl=ja)
- [Amazon Cognito](https://aws.amazon.com/jp/cognito/)
- [Auth0](https://auth0.com/jp)

## 認証サービスの選定結果

結論として、Amazon Cognito を選定しました。
以下、各選定基準に沿った説明を行います。

### OIDC でのログインが行えるか

OIDC の説明については以下をご参照ください。
https://www.macnica.co.jp/business/security/manufacturers/okta/blog_20210901.html

認証については、企業の情報システム担当者が気にする部分ですので知人の情報システム担当者に話を聞きました。
その際に OIDC が重要というコメントが出たため、もっとも重要な基準としました。

Firebase Authentication については、冒頭の画像の通り OIDC を使用する場合は
2DAU（デイリーアクティブユーザー数）までが無料枠の範囲となります。
2DAU では容易に超えてしまう可能性があるため、難しいです。

https://firebase.google.com/docs/auth/web/openid-connect

Amazon Cognito については、以下の通り機能があることが確認できます。
https://docs.aws.amazon.com/ja_jp/cognito/latest/developerguide/cognito-user-pools-oidc-flow.html

以下の通り 50 MAU(Monthly Active Users) の無料利用枠が利用できます。
少し辛いですが、ギリギリ初期であれば無料枠の範囲に収まらなくもないでしょう。
https://aws.amazon.com/jp/cognito/pricing/

Auth0 についても、以下の通り機能があることが確認できます。
特にユーザ数での制限は見つかりませんでした。
https://auth0.com/docs/authenticate/single-sign-on#openid-connect

Amazon Cognito 及び Auth0 が条件を満たすため以降ではその 2 点を比較します。

### 攻撃への対策機能を備えているか

外部からサービスへの攻撃を受けた際に、サービスを保護することができるかは費用よりも重要と考えます。
特にその中でも、基本的な総当たり攻撃(ブルートフォース)や疑わしい IP アドレスの除去に加えてアダプティブ MFA が重要と捉えています。
アダプティブ MFA については以下をご参照ください。
https://docs.aws.amazon.com/ja_jp/cognito/latest/developerguide/cognito-user-pool-settings-adaptive-authentication.html

Amazon Cognito においては、下記の通り攻撃を受けた際の高度な対策が行なえます。
https://docs.aws.amazon.com/ja_jp/cognito/latest/developerguide/cognito-user-pool-settings-advanced-security.html

ただ、その場合は以下記載の通り料金が上乗せとなります。
https://aws.amazon.com/jp/cognito/pricing/

計算してみると、500 ユーザ程度で 50%が SAML または OIDC でログインして高度なセキュリティ機能を利用した場合の費用は
$28 でした。そのため、有効にしても大きな費用インパクトは無いでしょう。

![Cognitoで高度なセキュリティ機能をオンにした場合の費用](/images/selecting-cloud-platform-for-btob-saas/cognitoPrice.png)

Auth0 の場合は、下記の通り基本的な総当たり攻撃(ブルートフォース)や疑わしい IP アドレスの除去は無料機能に含まれますが、
アダプティブ MFA は Enterprise からの機能です。Enterprise の料金は非公開ですがひとつ下の PROFESSIONAL プランの料金を見るに
初期のサービスで支払いは難しい金額です。

https://auth0.com/jp/pricing

上記の結果からサービスの初期でも払える金額で重要なセキュリティ対策機能を全て揃えられるのは
Amazon Cognito となります。

# サーバレスアーキテクチャの選定

自己資金であるため、費用を抑えるためにサーバレスアーキテクチャを活用します。

## 参考資料

https://qiita.com/h1guchi/items/4c4fc1b11580b76409b9

https://qiita.com/toto_inu/items/77e31e92f908a1fda8f7

## サーバレスアーキテクチャの選定基準

サーバレスアーキテクチャはいくつものサービスと連携するため、基準は以下に絞られます。

- 選定したホスティング・DB・認証のサービスと相性が良いか

## サーバレスアーキテクチャの選定候補

主要なサーバレスアーキテクチャは以下となります。

- [Firebase](https://firebase.google.com/?hl=ja)
- [Amplify](https://aws.amazon.com/jp/amplify/)

## サーバレスアーキテクチャの選定結果

ホスティングについてはサーバレスアーキテクチャによって決まるため未定ですが、DB・認証は AWS のサービスを使用するため
それらと相性が良いのは同じ AWS の Amplify となります。
そのため、ホスティングについても AWS Amplify ホスティングとなります。
