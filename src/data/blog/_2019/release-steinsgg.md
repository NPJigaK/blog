---
pubDatetime: 2019-2-25T18:00:00.000Z
modDatetime: 2020-03-08T18:00:00.000Z
title: PUBG試合分析システムを公開しました
featured: true
tags:
  - PUBG
  - ゲームライフハック
  - 個人開発
category: ゲーム関連
description: PUBG試合分析システム Steins.GG を公開しました！
---

> [!note] **この記事は [`steins.gg`](<https://twitter.com/search?q=(steinsgg%20OR%20steins.gg%20OR%20%40SteinsGG)%20until%3A2021-01-01&f=live&src=typed_query>) から移行した記事です。**
>
> `.gg` ドメインの維持費が高いため `steins.gg` は閉鎖しました。

PUBG試合分析システム `Steins.GG` を公開しました！

特定のPUBGチームにのみ限定公開していた旧分析システム [`404system`](<https://twitter.com/search?q=twitter.com%2F404analyze%20until%3A2020-01-01&src=typed_query>) の試合（単体から複数まで）のスタッツ統計表示・分析機能に加えて、初動降り確認機能やどのチームがどのタイミングでどんなムーブをしたか視覚的に確認するMAP機能など誰でも使えるツールとして公開しました！！
今後も新機能の追加や改善を行っていくので、お気軽にご要望ください！

## 目次

## どこで使えるの？
`https://steins.gg/pubg/` で検索検索ぅ！

## 機能紹介

### 試合スタッツ統計表示

指定した試合（複数選択可）のスタッツを集計・表示します。  
偏差値（独自計算）スコアの高い順に並び替えて表示します。

![steinsgg-status-list](https://pbs.twimg.com/media/D1PXx8fU8AALi1G?format=png)
引用元ポスト：<a href="https://x.com/steinsgg/status/1104463801091411968">Xの投稿</a>

### 個人戦績詳細分析

指定した試合（複数選択可）の詳細な個人戦績を集計・表示します。 

よくあるキル・アシストやダメージに加え、どんな移動手段でどのくらいの距離を移動したか、どの武器でどの部位に対してどれくらいヒットしたかなど確認できます！

![steinsgg-status-list](https://pbs.twimg.com/media/D1WNK3GVsAAnM91?format=png)
引用元ポスト：<a href="https://x.com/KagiJPN/status/1104945295274565632">Xの投稿</a>

<video autoplay loop="loop" muted="muted" plays-inline="true" class="border border-skin-line" controls=”true”>
  <source src="https://video.twimg.com/ext_tw_video/1103282918095351808/pu/vid/1280x720/FTudwnSCRL_mAMmY.mp4" type="video/mp4">
</video>

### 初動降り分析

各プレイヤーの初動降りポジションを確認できます。  
表示される位置は、地面に接地した瞬間の座標です。  
ランドマークの確認、どの建物に降下したか、どの道から車両を確保したかなどの分析にご活用ください。

![steinsgg-syodouori](@/assets/images/blog/2019/release-stainsgg/steinsgg-syodouori.jpg)
引用元ポスト：<a href="https://x.com/steinsgg/status/1088861747820224513">Xの投稿</a>

見つけづらいときは、マップ下部のプレイヤー一覧でチームをクリックすると、赤い矢印で位置を表示します。
マウスホイールでマップの拡大・縮小が可能です。

<video autoplay loop="loop" muted="muted" plays-inline="true" class="border border-skin-line" controls=”true”>
  <source src="https://video.twimg.com/ext_tw_video/1103061383510278145/pu/vid/1280x720/0edL8iMzdGk2BKRU.mp4" type="video/mp4">
</video>

### ポジション to タイム

試合開始から任意の時刻（例：12分46秒）における各プレイヤーの位置を確認できます。  
マップ下部のプレイヤー一覧から目的のチームをクリックすると、その時点の位置が表示されます。  
画面下のタイムスライダーを動かして、時間を前後に移動できます。

<video autoplay loop="loop" muted="muted" plays-inline="true" class="border border-skin-line" controls=”true”>
  <source src="https://video.twimg.com/ext_tw_video/1103062864091176961/pu/vid/1280x720/COzXnMNd6cdJ9xdK.mp4" type="video/mp4">
</video>
引用元ポスト：<a href="https://x.com/steinsgg/status/1103063520411705344">Xの投稿</a>

### ムーブ分析
各チームのフェーズ別ムーブ（移動ルート）を確認できます。  

線の色はフェーズごとに分かれており、フェーズが切り替わるタイミングで色も切り替わります。  
例）青い移動線が青フェーズ円の外側＝安置ダメージを食らいながらの移動。

![steinsgg-move](@/assets/images/blog/2019/release-stainsgg/steinsgg-move.jpg)
引用元ポスト：<a href="https://x.com/steinsgg/status/1088861747820224513/photo/4">Xの投稿</a>

マップ下部のプレイヤー一覧から目的チームをクリックすると、該当ルートが表示されます。
<video autoplay loop="loop" muted="muted" plays-inline="true" class="border border-skin-line" controls=”true”>
  <source src="https://video.twimg.com/ext_tw_video/1103062299051417600/pu/vid/1280x720/IgKVlgXPiPrcBKgs.mp4" type="video/mp4">
</video>

## 追記（2020/1/15）

Steins.GG（旧404system）の公開サービス提供を終了しました。
理由は大きく二つあり、サーバー・ドメイン維持費がきつくなってしまったのことと機能のメンテナンス(公式APIの変更等の追従)
を続けることに対するモチベーション低下が原因です。
旧サービス時代を含めて一年以上サービスを公開し続けられたのは利用して頂いた皆様のおかげだと思っています。
3万ユーザー以上のアクセスをして頂けるようなサービスを提供出来たのはとても良い経験になりました。
![steinsgg-googleanalytics](@/assets/images/blog/2019/release-stainsgg/steinsgg-googleanalytics.jpg)

またモチベーションが上がればまたひっそりと再公開するかもしれません。その時はぜひよろしくお願い致します。

## 追記（2020/3/8）

多くのユーザーの方からSteins.GGをまた使わせてほしいという要望があったので、限定公開ツールとして再公開しました。
限定公開な理由はサーバー維持・運用費と極限まで抑えたいので、利用ユーザーを制限する必要があるためです。

モチベも復活したので新機能なども追加予定です。
気になる方はTwitterまでご連絡下さい。
