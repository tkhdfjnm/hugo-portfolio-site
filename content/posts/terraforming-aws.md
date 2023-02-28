---
title: "Terraforming AWS"
description: "Terraform を利用した AWS 側の構成と管理について説明します"
images: [/img/terraform-deployment.jpg]
categories: "Tech"
date: 2023-03-01T01:30:00+09:00
lastmod: 2023-03-01T01:30:00+09:00
draft: false
---

## 構成管理
Terraform および Terraform Cloud を利用しています

![TerraformCloud を利用したデプロイメント](/img/terraform-deployment.jpg)

Terraform のコードを変更して GitHub で PR を切るだけで、自動テストよろしく自動で plan してくれる

反映は PR のマージによって Terraform Cloud 上で apply 待ちになるので、それを確認してから apply してあげる

非常に簡単かつ快適です

※ インフラ関連のコードはプライベートリポジトリで管理しています

## どこまでをコード化できるのか (ブートストラップ問題)
かならずぶち当たる、 Terraform Cloud をどう管理するか、 AWS アカウントをどう管理するか、の話

僕の場合は、 AWS ルートアカウントがカラッポで最初から組み立てられる環境だったので、手作業を最小限に抑えることができた

Terraform Cloud
- Terraform Cloud 自体の管理用ワークスペースは手作業で作成
- その他のワークスペースは Terraform で作成

AWS
- ルート AWS アカウントは手作業で作成
- Terraform Cloud 用の IAM ユーザまで手作業で作成
以降の諸々 (config や CloudTrail、子アカウントの設定など) は全て Terraform で管理

## AWS アカウントの設定と用途
![AWS アカウントの構成](/img/aws-structure.jpg)

- ルートは以下を Organization 全体に適用する以外の用途では利用しない
  - Config の有効化 (CloudFormation StackSets)
  - CloudTrail の有効化
  - Jump アカウントから AssumeRole する IAM ロール (CloudFormation StackSets)
  - Terraform Cloud から利用する IAM ユーザ (CloudFormation StackSets)
- Jump アカウント (コンソールを利用する際にログインする踏み台アカウント) を利用して、各種アカウントの作業用ロールに AssumeRole する運用
- 原則用途ごとにアカウントを切る予定
  - 現状このポートフォリオサイトしかないので misc というアカウントを切って Route53 なども一緒に管理している
