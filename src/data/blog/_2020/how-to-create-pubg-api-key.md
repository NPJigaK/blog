---
pubDatetime: 2020-03-08T18:00:00.000Z
title: 【PUBG】PUBG API の使い方【API Key 作成から】
featured: false
tags:
  - PUBG
category: 技術関連
description: PUBGのAPIキーの取得方法を紹介します。
---

PUBG の試合データなどを分析するためには、公式の開発者APIキーが必要です。  
今回は、PUBGのAPIキーの取得方法をわかりやすく解説します！

## 目次

## 1. 準備：必要なもの

- PUBGアカウント（Steamアカウント）
- メールアドレス（連絡用）

## 2. PUBG Developer Portal にアクセス

1. ブラウザで [**PUBG Developer Portal**](https://developer.pubg.com/）にアクセス。
2. ページ上部の「Sign in」をクリックしてSteamアカウントでログイン。
3. PUBGの利用規約に同意し、「Allow」をクリック。

## 3. アプリケーションの作成

1. ログイン後のダッシュボードにある「Get your own API key」をクリック。
2. 必要事項を入力するフォームが表示されるので、以下を入力します。
   - **Application Name**（任意）：自分のツールやプロジェクト名
   - **Application Description**：どのような用途でAPIを利用するか簡単に説明
   - **Application Website**（任意）：自分のウェブサイトやGitHubリポジトリのURL（あれば記入）

3. 「Create Application」ボタンを押してアプリケーションを作成。

## 4. API キーの取得

アプリケーション作成後、以下のような画面が表示されます。

![pubg-apikey](@/assets/images/blog/2020/pubg-apikey.jpg)

- 表示されたAPIキーを安全な場所にコピーして保存します。
- APIキーは絶対に他人と共有しないでください。漏洩した場合はすぐにキーを削除して新しく再発行してください。

## 5. テストリクエスト

APIキーが正しく発行されたことを確認するために、テストリクエストを送ります。

```bash
curl -H \"Authorization: Bearer <YOUR_API_KEY>\" \\
     \"https://api.playbattlegrounds.com/shards/pc-na/players?filter[playerNames]=yourPlayerName\"
```

- レスポンスとして200 OKが返れば成功です。

## 6. どんな情報が取得できる？
APIリファレンスは公式のドキュメントで確認出来ます。
https://documentation.pubg.com/en/introduction.html

### 公式サイトから試したい API をリクエスト可能です

例えばプレイヤー情報を取得したい時は、以下のページに行きます。
https://documentation.pubg.com/en/players-endpoint.html#/Players/get_players__accountId_

Authorizeボタンを押下して、取得したAPI KEYを入力して認可します。

Try it out ボタンを押下してAPIから情報を取得したいプレイヤーの名前を入力してExecuteボタンを押下します。

Responsesから返ってくる情報を確認出来ます。

実際にアプリを作る際に、公式サイトでどのAPIをどのように使ったらどのような情報が返ってくるかを確認しながら作れるのでとても便利です。