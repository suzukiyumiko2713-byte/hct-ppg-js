# hct-ppg-js
# Browser-Based Heartbeat Counting Task with Camera-PPG (HCT-ppg-js)

**A self-contained, browser-based implementation of the heartbeat counting task
(HCT; Schandry, 1981) with concurrent smartphone-camera photoplethysmography
(PPG) for objective heart rate acquisition, built for unsupervised online
administration (no app install required).**

このリポジトリは、性的快感とウェルビーイングの神経基盤に関する研究（内受容感覚予測誤差の変容）の一部として開発された、**心拍カウント課題（HCT）を、スマートフォンのカメラのみでオンライン・無監督下で実施するためのツール**です。

## 概要

- 教示 → 練習試行（30秒）→ 本番試行（25秒・35秒・45秒）→ 各試行後の回答入力・信頼度評定、という一連の流れをブラウザ上で完結させます
- 客観的な心拍データの取得には [ppg-js](https://github.com/sontakey/ppg-js)（MIT License, sontakey氏による）を使用し、スマートフォン背面カメラでのPPG計測を行います
- インストール不要（`index.html` をHTTPS環境でホストするだけで動作）

## 依存ライブラリ

- [`@sontakey/ppg-js`](https://www.npmjs.com/package/@sontakey/ppg-js)（MIT License）— CDN (`cdn.jsdelivr.net`) 経由で読み込み

## ⚠️ 検証状況（重要）

- **本ツールの心拍数推定は、まだ臨床的な妥当性検証を経ていません。** ppg-js自体が「医療機器ではなく、デモ・研究用途のみ」と明記しており、開発チーム独自のテストデータ（合成信号、iPhone実測2件）による検証に留まっています
- 予備的な動作確認において、実測心拍数との乖離（約10〜15%程度）が観察されており、**本番のデータ収集に使用する前に、独自の精度検証（基準測定器との比較）が必須**です
- カウント課題の試行タイミング（`trialWindows`、ミリ秒単位で記録）と、ppg-jsの`getTachogram()`が返す拍動タイムスタンプ（`t`、秒単位）が同一の基準（セッション開始からの経過時間）で揃っているという前提でスコアリングを行っています。この前提は実機での検証が必要です

## 使い方

1. `index.html` をHTTPS対応のWebホスティング（GitHub Pages等）で公開する
2. スマートフォンのブラウザで開く
3. 教示に従い、背面カメラとフラッシュを指で覆い、信号が安定したら課題を開始する

## ファイル構成

```
index.html   # 課題本体（教示・タイマー・回答入力・信頼度評定・簡易採点をすべて含む単一ファイル）
LICENSE      # MITライセンス
```

## 引用・謝辞

本ツールは以下を利用しています。

- ppg-js: sontakey, *ppg-js: Photoplethysmography (PPG) waveform javascript package from mobile phone camera*, MIT License. https://github.com/sontakey/ppg-js
- ppg-jsが参照する検証枠組み: Vandenberk T, et al. "Clinical Validation of Heart Rate Apps," *JMIR mHealth and uHealth*, 2017;5(8):e129.
- 心拍カウント課題の原法: Schandry, R. (1981). Heart beat perception and emotional experience. *Psychophysiology*, 18(4), 483–488.

## AI利用に関する開示

**本ツールのコードは、Anthropic社のClaude（AIアシスタント）との対話を通じて実装されました。** 課題設計（試行構造、教示文、UI）は研究者が指定し、それに基づくHTML/JavaScriptの実装、ppg-jsライブラリとの統合、採点ロジックの実装をClaudeが行っています。人間（研究者）によるレビュー・実機での動作確認・精度検証を経て、研究に使用可能かどうかを判断しています。

投稿先ジャーナルのAI利用開示ポリシーに従い、論文中でも本ツールの開発過程を適切に開示してください。

## ライセンス

MIT License. `LICENSE` ファイルを参照してください。ppg-js自体のライセンス条項も別途ご確認ください。
