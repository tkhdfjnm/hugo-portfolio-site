---
title: "Why AWS and Hugo"
description: "このサイトを構築するにあたっての技術選定について説明します"
images: [/img/default.png]
categories: "Tech"
date: 2022-02-25T16:46:00+09:00
draft: false
---
## なぜ AWS S3 と CloudFront を選んだのか
- Terraform でのリソース管理をやってみたかった
- AWS を使ってみたかった

という、技術ありきでの選定でした

労力を考えると、他のホスティングサービス (Netlify なり GitHub Pages なり) でもよかったと思います
特に比較はしていません

Terraform のコードは GitHub のプライベートリポジトリで管理しており、 PR 作成・マージを Terraform Cloud と連携することで AWS リソースの変更管理をしています

## なぜ Hugo を選んだのか
当初は Wordpress ないしヘッドレス CMS のようなものがないか、と探していました
その中で静的サイトジェネレータ (SSG) というツールを知りました

見つけた SSG の中から、実際に 11ty と Hugo を触ってみて、
- バイナリひとつで動作する
- 標準で欲しいサイト構成を生成してくれる

という点が魅力で Hugo を採用することにしました
11tyは
- node.js 環境を構築する必要がある (やりたくない)
- 出力結果がシンプルなのでテンプレートづくりに労力がかかる (やりたくない)

という理由で候補から外れました

## 今後の課題
### Hugo テーマをリポジトリに切り出す
そもそもサイト自体のコードもまだリポジトリ管理できていない...

### ビルド・デプロイの自動化
GitHub Actions で S3 に sync までやれるとカッコイイ...
(現状は手動でビルドコマンドを叩いてビルド、 Web コンソール経由でアップロード)