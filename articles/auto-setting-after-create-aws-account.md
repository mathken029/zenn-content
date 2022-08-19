---
title: "AWSアカウントで最初にやるべきことの自動化"
emoji: "🌊"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["AWS", "Terraform", "BtoB", "SaaS", ""]
published: false
---

# 概要

法人向けクラウドサービス開発(BtoB SaaS)を開発するにあたり、必要な AWS アカウントの設定を行うため以下の記事を参照しました。
https://dev.classmethod.jp/articles/aws-baseline-setting-202206/

以下の目的で上記の記事の作業の自動化を図りたいと考え、友人から勧められた Terraform で試してみることにしました。

- 一人での開発になるため、できるだけ自動化の習慣をつけて省力化を図る
- 今後別の AWS アカウントを作成した場合に、同じ作業を手動で行わないで良いようにする
- 同じ作業を行う人の手間を少なくする

Terraform で自動化できない部分については、手動もしくは代替手段を用いることとします。

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

# 自動化の設定

## ログ・モニタリング

### (AWS CloudTrail) ログ長期保管のための設定（証跡の作成）【MUST】

### (AWS CloudTrail) CloudTrail Insights の有効化【SHOULD】

### (AWS Config) 有効化（レコーダーの作成）【MUST】

### (AWS Health Dashboard) 通知設定【SHOULD】

## セキュリティ

### (AWS IAM (ルートユーザー)) MFA 認証の設定【MUST】

### (AWS IAM (ルートユーザー)) アクセスキーの削除【MUST】

### (AWS IAM) IAM パスワードポリシーの設定【MUST】

### (AWS IAM) IAM ユーザー/グループの作成【MUST】

### (AWS IAM) MFA 認証の設定【MUST】

### (AWS IAM Access Analyzer) 有効化（アナライザーの作成）【SHOULD】

### (Amazon GuardDuty) 有効化【SHOULD】

### (Amazon GuardDuty) S3/Kubernetes 保護の有効化【SHOULD】

### (Amazon GuardDuty) 通知設定【SHOULD】

### (AWS Security Hub) 有効化【SHOULD】

### (Amazon Detective) 有効化【SHOULD】

### (Amazon VPC) デフォルト VPC の削除【SHOULD】

## 契約・コスト

### (マイアカウント) 秘密の質問の設定【SHOULD】

### (AWS Cost Explorer) 有効化（起動）【SHOULD】

### (AWS Cost Explorer) サイズの適正化に関する推奨事項を有効化【SHOULD】

### (AWS Compute Optimizer) 有効化【SHOULD】

### (AWS Cost Anomaly Detection) 有効化（モニターとサブスクリプション設定）【SHOULD】

### (AWS Budgets) 予算アラートの設定【SHOULD】

## その他

### (リソース命名規則) 大まかな命名規則の決定【SHOULD】

# MUST、SHOULD ではないが自動化するもの

自己資金での開発となるため費用関連は細かくチェックしたく、以下の項目の設定も自動化します。

## 契約・コスト

### (請求コンソール (Billing)) AWS Cost and Usage Reports の有効化【MAY】

### (請求コンソール (Billing)) コスト配分タグの設定【MAY】

### (請求コンソール (Billing)) PDF 請求書の設定【MAY】

### (請求コンソール (Billing)) 無料利用枠の使用アラートの設定【MAY】

### (請求コンソール (Billing)) 請求アラートの設定【INFO】
