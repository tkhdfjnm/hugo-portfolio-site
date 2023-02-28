---
title: "Home Network"
description: "自宅ネットワークの構成について紹介します"
images: [/img/physical-sw.jpg]
categories: "Tech"
date: 2022-02-26T14:18:00+09:00
lastmod: 2023-02-28T18:00:00+09:00
draft: false
---
## 論理的なネットワーク構成
用途ごとに VLAN を 4 つ切っています

それぞれ以下のような目的で利用しています
- Home: クライアントとサーバが同居する、普段使いの NW
- Access: The Internet へのアクセスのみ提供する NW
  - ゲーム機や会社貸与 PC などを接続
- Quarantine: 外部公開を前提とし他の VLAN との通信をしない NW
  - 外部公開しているサービスがないので実質寝てる
- Management: 接続されている各機器のメンテナンス用途を想定した NW
  - VLAN trunk 時のデフォルト VLAN として設定

![論理構成図](/img/logical-nw.jpg)

## 物理的なネットワーク構成
- BB ルータ: NEC UNIVERGE IX2105
- 無線 AP: HP MSM430
- 子ハブ: NETGEAR GS108E x2, GS108PE

![物理構成図](/img/physical-nw.jpg)

BB ルータ、各子ハブ間は VLAN trunk ポートで接続
子ハブは状況に応じてポート VLAN と使い分け

![スイッチングハブ](/img/physical-sw.jpg)

ポート VLAN はわかりやすいようにラベリング
