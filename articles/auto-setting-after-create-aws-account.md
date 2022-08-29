---
title: "AWSアカウントで最初にやるべきことの自動化"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Terraform", "BtoB", "SaaS", "IaC"]
published: true
---

# 概要

法人向けクラウドサービス開発(BtoB SaaS)を開発するにあたり、必要な AWS アカウントの設定を行うため以下の記事を参照しました。
https://dev.classmethod.jp/articles/aws-baseline-setting-202206/

以下の目的で上記の記事の作業の自動化を図りたいと考え、友人から勧められた Terraform で試してみることにしました。

- 一人での開発になるため、できるだけ自動化の習慣をつけて省力化を図る
- 今後別の AWS アカウントを作成した場合に、同じ作業を手動で行わないで良いようにする
- 同じ作業を行う人の手間を少なくする

Terraform で自動化できない部分については、スキップして手動もしくは代替手段を後ほど検討することとします。

不足している設定があるかもしれないのでこの設定も追加したほうが良い、する必要があるというご指摘ございましたらコメントなどでお願いします。

## 免責事項

- 本記事に記載された内容は、情報の提供のみを目的としています。従って、本書を用いた業務やサービス選定などは必ずご自身の責任と判断によって行ってください。これらの情報による業務やサービス選定などの結果について、著者はいかなる責任も負いません。
- 本記事は、ページに記載されている更新日時点での内容です。本書の中で登場するサービス・知識については、著者は一切の責任を負いません。
- 会社名、商品名については、一般に各社の登録商標です。TM 表記などについては記載しておりません。また、特定の会社、製品について不当に貶める意図はありません。

## 自動化の方針

記事内でレベルが下記のように設定されているため、その中で MUST 及び SHOULD を自動化対象とします。

- MUST：必須レベルでやること
- SHOULD：（理由がない限り）やったほうがいいこと
- MAY：条件（要件）によってやる/やらないが決まること
- INFO：関連する役立ち情報

## 参考資料

- [Terraform の概要](https://dev.classmethod.jp/articles/terraform-getting-started-with-aws/)
- [Terraform のベストプラクティス](https://dev.classmethod.jp/articles/terraform-bset-practice-jp/)

# Terraform Cloud のセットアップ

Terraform をローカル環境で実行するための良い記事が見つからなかったため、Terraform Cloud で行うことにして以下の記事に従ってセットアップを行い、AWS 上で VPC が作成されていることを確認できました。

https://qiita.com/boccham/items/190f04bfbc9ffc0b5baf

環境変数の設定においては、以下のように変数を sensitive に設定して GUI や API 上でも設定されないようにしました。
間違えて設定した場合は、見えにくいですが右側に「…」がありますのでそちらから削除可能です。

![環境変数の設定](/images/auto-setting-after-create-aws-account/terraform-cloud-variable.png)

また、記事の中で「Queue plan から Cloud 上で terraform plan を実行することが可能です」という記載がありましたが私の環境では表示されなかったため、タブ「Run」から実行しました。

Terraform の設定方法は下記のドキュメントを参照しています。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs

# 自動化の設定

以下のファイルにて設定を管理していますので、実装をみたい方は以下をご参照ください。
https://github.com/mathken0290141/terraform_public/blob/main/main.tf

以下では各設定の補足を記載し、実装内容自体は取り上げません。

## ログ・モニタリング

### (AWS CloudTrail) ログ長期保管のための設定（証跡の作成）【MUST】

以下ページの Basic を main.tf に貼り付け、foobar や foo の箇所を適宜書き換えることで証跡の作成を行えました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudtrail

### (AWS CloudTrail) CloudTrail Insights の有効化【SHOULD】

以下の値を追加することで有効化できました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudtrail#insight_selector

![CloudTrail Insights](/images/auto-setting-after-create-aws-account/cloudtrail-insights.png)

### (AWS Config) 有効化（レコーダーの作成）【MUST】

以下を適用することで有効化されました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/config_configuration_recorder_status

![AWS Config](/images/auto-setting-after-create-aws-account/aws-config.png)

### (AWS Health Dashboard) 通知設定【SHOULD】

Terraform のドキュメントに該当項目がなかったため、今後手動または代替策で設定とします。
関連してそうな EventBridge にも該当項目はなさそうでした。

## セキュリティ

### (AWS IAM (ルートユーザー)) MFA 認証の設定【MUST】

Terraform のドキュメントに該当項目がなかったため、今後手動または代替策で設定とします。

以下の手順にて AWS CLI で設定することは可能なようです。
https://aws.amazon.com/jp/premiumsupport/knowledge-center/authenticate-mfa-cli/

### (AWS IAM (ルートユーザー)) アクセスキーの削除【MUST】

Terraform のドキュメントに該当項目がなかったため、今後手動または代替策で設定とします。
念のため、ユーザー名を「root」にして試しましたが「root」という名前の IAM ユーザが作成されるだけでした。
以下にて CLI から削除する方法があるようです。

http://prototype-handson-cli.s3-website-ap-northeast-1.amazonaws.com/handson_light-aws_service/handson_light-aws_service-iam-getting_started/iam-access_key-delete-novice.html

### (AWS IAM) IAM パスワードポリシーの設定【MUST】

Terraform のドキュメントの内容をそのまま貼り付けました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_account_password_policy

一点、以下の IPA の文書を元に桁数を 10 にしています。
https://www.ipa.go.jp/chocotto/pw.html

以下の通り、設定した通りのパスワードポリシーになっています。
![IAM Password Policy](/images/auto-setting-after-create-aws-account/IAM-passwordPolicy.png)

### (AWS IAM) IAM ユーザー/グループの作成【MUST】

IAM グループを作成してマネージドロールを付与し、IAM グループ内にユーザーを作成しました。

独自ロールを作成するより、AWS が作成しているマネージドロールを使う方が良いと考えたのですが Terraform のドキュメントに記載がなかったため、以下ページを参照しました。
https://intellipaat.com/community/28131/how-do-you-add-a-managed-policy-to-a-group-in-terraform

また、付与する権限はかなり大きな権限となるのですが、最初に広めの権限を付与して後から絞るという考えで付与しています。

マネージドロールを識別するための文字列は以下から取得しています。

![IAM AdministratorAccess](/images/auto-setting-after-create-aws-account/IAM-AdministratorAccess.png)

以下の通りユーザー作成及びポリシー付与ができていることが確認できます。

![IAM-userCreated](/images/auto-setting-after-create-aws-account/IAM-userCreated.png)

![IAM-attached-managedRole](/images/auto-setting-after-create-aws-account/IAM-attached-managedRole.png)

### (AWS IAM) MFA 認証の設定【MUST】

「(AWS IAM (ルートユーザー)) MFA 認証の設定【MUST】」と同様に、Terraform のドキュメントに該当項目がなかったため、今後手動または代替策で設定とします。

### (AWS IAM Access Analyzer) 有効化（アナライザーの作成）【SHOULD】

以下のサンプルをそのまま実行しました。
Organization Analyzer は不要そうでしたので、Account Analyzer のみ実行しています。

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/accessanalyzer_analyzer

ルールは、サンプルのものをそのまま適用しています。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/accessanalyzer_archive_rule

以下の通り、AccessAnalyzer 及びアーカイブルールの設定が完了しました。

![IAM-AccessAnalyzer](/images/auto-setting-after-create-aws-account/IAM-AccessAnalyzer.png)

![IAM-AccessAnalyzer-rule](/images/auto-setting-after-create-aws-account/IAM-AccessAnalyzer-rule.png)

### (Amazon GuardDuty) 有効化, S3/Kubernetes 保護の有効化【SHOULD】

以下をそのまま貼り付けました。
一点、kubernetes の audit_logs を true に変更しました。

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/guardduty_detector

有効前の状態が以下です。

[GuardDuty-before-enable](/images/auto-setting-after-create-aws-account/GuardDuty-before-enable.png)

以下の通り、それぞれ有効化されています。

![GuardDuty-S3](/images/auto-setting-after-create-aws-account/GuardDuty-S3.png)

![GuardDuty-Kubernetes](/images/auto-setting-after-create-aws-account/GuardDuty-Kubernetes.png)

![GuardDuty-MalwareProtection](/images/auto-setting-after-create-aws-account/GuardDuty-MalwareProtection.png)

### (Amazon GuardDuty) 通知設定【SHOULD】

通知設定についてドキュメントにはなかったのですが、以下ページを見るに Cloud Watch などを活用して通知を行うようです。こちらは Slack を通知先として想定するため、Slack のワークスペースの準備ができたら行うこととします。

https://github.com/trussworks/terraform-aws-guardduty-notifications/blob/main/main.tf

Cloud Watch の関連ドキュメントは下記です。

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_rule

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_event_target

### (AWS Security Hub) 有効化【SHOULD】

以下のドキュメントを活用しました。
「resource "aws_securityhub_standards_control" "ensure_iam_password_policy_prevents_password_reuse"」についてはエラーとなったため、適用していません。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/securityhub_standards_control

下記のように有効化されていることが確認できました。
![SecurityHub](/images/auto-setting-after-create-aws-account/SecurityHub.png)

### (Amazon Detective) 有効化【SHOULD】

以下のドキュメントの内容を貼り付けました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/detective_graph

アカウントが Amazon GuardDuty に少なくとも 48 時間登録されていないと有効化できず、有効化に失敗しますので注意してください。

以下の通り有効化にを完了しました。
![detective](/images/auto-setting-after-create-aws-account/detective.png)

### (Amazon VPC) デフォルト VPC の削除【SHOULD】

以下情報を参照して「force_destroy = true」を試してみたのですが、デフォルト VPC の削除はできませんでした。
なにかやり方が間違えている気がするので、もし実際に成功している方が居たら教えてください。

https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/default_vpc

https://discuss.hashicorp.com/t/destroy-default-vpc/2474/4

## 契約・コスト

### (マイアカウント) 秘密の質問の設定【SHOULD】

Terraform のドキュメントを「security question」及び「secret question」、「question」で検索しましたがヒットしなかったため、設定できないものと判断しました。

### (AWS Cost Explorer) 有効化（起動）【SHOULD】

「Cost Explorer」で Terraform のドキュメントを検索しましたが、Cost Explorer 自体を有効化するような設定は見つかりませんでした。
本作業を実施する前に Cost Explorer を起動していたため、どれが有効化に関係するのかわからなかったというのもあります。

### (AWS Cost Explorer) サイズの適正化に関する推奨事項を有効化【SHOULD】

Terraform のドキュメント内に有効化する項目が見当たらなかったため、該当項目のマネジメントコンソール上の英語表記である「Amazon EC2 resource recommendations」で検索してみましたが、情報が出てきませんでした。

マネジメントコンソールから Cost Explorer を表示して以下から有効化できるので、手動で有効化するのが良いと考えます。

![CostExplorer-size](/images/auto-setting-after-create-aws-account/CostExplorer-size.png)

### (AWS Compute Optimizer) 有効化【SHOULD】

Terraform のドキュメントを「Compute Optimizer」で検索しましたがヒットしませんでした。
以下ページより手動で有効化できます。

https://us-east-1.console.aws.amazon.com/compute-optimizer/home/

### (AWS Cost Anomaly Detection) 有効化（モニターとサブスクリプション設定）【SHOULD】

以下のドキュメントの内容をそのまま貼り付けました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/ce_anomaly_subscription

以下の通り、コストモニターが追加されてます。

![CostAnomalyDetection](/images/auto-setting-after-create-aws-account/CostAnomalyDetection.png)

### (AWS Budgets) 予算アラートの設定【SHOULD】

以下の「Create a budget for $100」をそのまま貼り付けます。
また、同ページ内の別サンプルからメール通知を行うための「notification」の箇所をコピーして貼り付けました。
https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/budgets_budget

以下の通り、予算が作成されています。

![Budgets](/images/auto-setting-after-create-aws-account/Budgets.png)

通知先のメールアドレスが表示されませんが、予算の編集を行うとメールアドレスが登録されているのが分かります。

![Budgets-email](/images/auto-setting-after-create-aws-account/Budgets-email.png)

## その他

### (リソース命名規則) 大まかな命名規則の決定【SHOULD】

Terraform での設定ではないですが、実運用する際は以下を参考に命名をします。
https://dev.classmethod.jp/articles/aws-name-rule/

# MUST、SHOULD ではないが自動化するもの

自己資金での開発となるため費用関連は細かくチェックしたく、以下の項目の設定も自動化します。

## 契約・コスト

### (請求コンソール (Billing)) PDF 請求書の設定【MAY】 & 無料利用枠の使用アラートの設定【MAY】

Terraform 内のドキュメントには該当設定が見当たリませんでした。
Billing の「請求設定」から PDF 請求書の発行及び無料利用枠の使用アラートの設定が行なえます。

# まとめ

以上で全ての設定を完了しました。必要に応じて今後更新していきます。
