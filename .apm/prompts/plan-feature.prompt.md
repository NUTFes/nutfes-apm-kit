---
description: repo 文脈を踏まえて Web 機能実装の計画を作る
author: NUTFes
input:
  - feature
  - constraints
---

# Plan Feature

`${input:feature}` を実装するための計画を作成してください。追加制約は `${input:constraints}` です。

## 進め方

1. 先に repo 構成、既存パターン、利用中のライブラリ、関連画面や API、`Makefile` / `mise.toml` / Docker 設定を確認する
2. 実装や検証に使う正式なコマンド入口が `make`、`mise run`、`docker compose` のどれかを確認する
3. 現状に対して何を変えるべきかを、挙動単位で整理する
4. 実装担当者が迷わない粒度で、変更点、データフロー、例外系、検証方法を決める
5. 破壊的変更、migration、環境変数、認可影響があれば明示する

## 出力要件

- 目的と成功条件
- 主要な変更点
- 影響を受ける UI / API / state / validation
- 実装と検証で使うべきコマンド経路
- テスト方針
- 未解決事項または要追加確認事項

実装者に判断を丸投げしない、decision-complete に近い計画にしてください。
