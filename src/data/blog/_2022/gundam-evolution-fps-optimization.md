---
pubDatetime: 2022-12-26T00:00:00.000Z
title: 【GUNDAM EVOLUTION】低スぺCPUでもFPSを出す方法
featured: false
category: ゲーム関連
tags:
  - GUNDAM EVOLUTION
  - ゲームライフハック
  - 最適化
description: foo
---

おはこんばんちは！最近、`GUNDAM EVOLUTION` にハマっている主です！  
今回は、**設定ファイル（ユーザー側で編集できる範囲）** から、描画処理を軽くする設定を追加する手順を紹介します。

## 目次

## 今回やる事　
`GUNDAM EVOLUTION` は `Unreal Engine 4` 製です。`UE4` の一般的な設定はユーザー側で変更することが可能です。(よくある例として、マウスの加速設定をOFFにするなど)

今回やる事は、`%LOCALAPPDATA%\EvoGame\Saved\Config\WindowsNoEditor\` 配下の `Engine.ini` を編集して、描画処理を軽くするオプションを設定し、低スペック `CPU` でも `FPS` を安定させます。

> [!warning] 執筆時点で GUNDAM EVOLUTION 公式サイトの利用規約を確認した範囲では、ユーザー設定ファイルの編集を明確に禁止する記載は見当たりませんでした。ただし、本記事の内容の適用は全て自己責任でお願いします。

## Engine.ini の設定

### `[ConsoleVariables]` セクションの追加

`Engine.ini` に `[ConsoleVariables]` セクションを追加して、以下の設定を追加します。

```ini
[ConsoleVariables]
r.HZBOcclusion=1            ; 見えないオブジェクトを描画しない判定を有効化。無駄な描画を減らす。

r.ViewDistanceScale=0.7     ; 描画距離の倍率を下げる。遠くの不要なオブジェクトを描画しない。

r.Fog=0                     ; 霧を消す
r.VolumetricFog=0           ; 立体的な霧を消す

foliage.ForceLOD=4          ; 木の描画を常に荒いモデルに固定。いくつか試したところガンエボでは4が最低。
grass.DensityScale=0        ; 草の描画を消す

r.ShadowQuality=0           ; 影の描画をほぼ消す

r.ParticleLightQuality=0    ; パーティクル(火や煙)のライティングを無効化
r.ParticleLODBias=1         ; パーティクル(火や煙)の粒度を荒くする

r.BloomQuality=0            ; 光のにじみ表現を消す
r.SSR.Quality=0             ; 画面反射を無効化
r.EyeAdaptationQuality=0    ; 明るさの自動調整を無効化

r.RenderTargetPoolMin=1000  ; レンダー用の一時バッファを最低 1GB 確保（VRAMに余裕があるGPU向け）
r.SceneColorFormat=2        ; 画面の色データを軽量化。色の表現が荒くなる。
```

### `[/Script/Engine.RendererSettings]` セクションの追加

`Engine.ini` に `[/Script/Engine.RendererSettings]` セクションを追加して、以下の設定を追加します。

```ini
[/Script/Engine.RendererSettings]
r.DefaultFeature.AntiAliasing=0  ; アンチエイリアスをOFF
r.DefaultFeature.MotionBlur=0    ; モーションブラーをOFF
```


## 余談

公式曰く「グラフィックカードのスペック差が勝敗に直結しにくい設計」という公平性を重視したゲームを目指しているそうです。 ← 🤔？？？

その分、`CPU` の性能差が出やすく、今回紹介したオプションの恩恵を実感しやすいはずです（特に低スペック `CPU` 環境では）。
