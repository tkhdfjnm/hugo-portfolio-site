---
title: "VRoid to VRChat"
description: "VRoid で作成したアバターを VRChat で利用する覚書"
images: [/img/creation-companion.jpg]
categories: "Tech"
date: 2023-03-01T01:00:00+09:00
lastmod: 2023-03-01T01:15:00+09:00
draft: false
---
## 想定する読者
僕のように「モデリングはできないけど、オリジナルのアバターで遊びたい！」という人向け

## 実際にやること
ざっくり以下の 3 ステップで完結！

- VRoid で作成したモデルを VRM 形式でエクスポート
  - 標準のママだと少し重いので出力パラメータを調整しておくとよい
- UniVRM (0.x 用) パッケージを用いて Unity にモデルをインポート
  - Unity は標準では VRM の読み込みに対応していないため、パッケージを用いる
  - VRoid の吐き出す VRM は Ver. 0.x なので注意
- VRChat SDK を用いてモデルをアップロード
  - ビルド前にモデルについて警告などが出るので適宜対応する
  - アップロード前にテストモードでのビルドもできる

後半 2 ステップがもろに Unity を使うので、面食らうかもしれない

わかってしまえばそんなに大変ではない

Unity 環境を先に整える必要があることさえ知っておけば大丈夫

## 気を付けたいこと = ハマったこと
- Unity は VRChat 指定のバージョン (2019.4.31) であること
  - Unity Hub からはインストールできないので個別でインストールする
- UniVRM は開発が盛んなパッケージなので、動作しなかったらダウングレードすること
  - 僕がダウンロードした時はたまたまバージョン事故が起きていて、インポートが落ちるバージョンを掴んでしまった

## Unity 環境の整備
あらかじめやっておくのだ
1. [Unity Editor](https://unity.com/releases/editor/whats-new/2019.4.31) のインストール
1. [VRChat Creator Companion](https://vrchat.com/home/download) のインストール
1. VRChat Creator Companion で新規プロジェクト作成
![creation-companion上の表示](/img/creation-companion.jpg)
1. 作成したプロジェクトに [UniVRM](https://github.com/vrm-c/UniVRM/releases) パッケージをインポート

## その他参考にしたサイト様
- [VroidをVRChatへアップロードするまとめ](https://rekor64y.web.fc2.com)
- [UnityでVRMファイルを読み込む・出力する方法 | AY3の6畳細長部屋](https://www.ay3s-room.com/entry/unity-vrm-import-export)
- [VRoid Studioで作ったモデルをVRChatに上げてVRで動かしてみたメモ | 神部まゆみのブログ](https://knb-mayumi.com/vroid-vrchat/)
- [アバター導入方法 Step.4b : SDK3版 - VRChat初心者向けガイド](https://vrc.wiki/beginner/838/)
