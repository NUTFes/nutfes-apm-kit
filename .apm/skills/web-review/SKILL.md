---
name: NUTFes Web Review
description: Next.js / React の変更を findings-first でレビューするための手順
---

# NUTFes Web Review

## 目的

NUTFes の Web 系変更をレビューするときに、問題発見を優先した一貫した観点を持たせます。

## いつ使うか

- PR レビュー
- 実装後の自己レビュー
- リリース前の差分確認

## レビュー手順

1. まず変更範囲の entrypoint、routing、form、API 呼び出し、state 管理を把握する
2. 次に不具合、仕様逸脱、セキュリティ、a11y、性能、保守性の順で問題を探す
3. findings は重大度順にまとめ、場所と影響を明確にする
4. 問題がなければその旨を明示し、残る未確認事項だけを短く整理する

## 観点

- `any` や unsafe cast で型安全が崩れていないか
- loading / error / empty / disabled state が抜けていないか
- `use client` の範囲が広すぎないか
- routing、認可、入力検証、失敗時表示が自然か
- keyboard accessibility と focus 管理が崩れていないか
- repo の既存 UI / data pattern から逸脱していないか

## 出力の原則

- findings-first
- 重大度順
- 修正に必要な情報を簡潔に含める
- 問題がない場合も「問題なし」を明示する
