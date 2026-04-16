---
description: NUTFes の Web 系リポジトリ向け findings-first レビュー
author: NUTFes
input:
  - scope
  - focus
---

# Web Review

NUTFes の Web 系リポジトリをレビューしてください。対象範囲は `${input:scope}`、重点観点は `${input:focus}` です。

## レビュー方針

1. まず不具合、仕様逸脱、UX 破綻、セキュリティ、a11y、保守性の問題を列挙する
2. 指摘は重大度順に並べ、再現条件や影響範囲を明確にする
3. 問題がなければ「重大な findings はなし」と明言する
4. その後に residual risk、未確認事項、追加で見るべきテストを短くまとめる

## 注目観点

- Next.js / React の実装が既存パターンと整合しているか
- TypeScript の型安全が保たれているか
- loading / error / empty state が考慮されているか
- フォーム、認可、API 呼び出しが安全に扱われているか
- responsive と keyboard accessibility が崩れていないか

## 出力形式

- Findings を先に出す
- 各 finding には、場所、問題、影響、必要な修正方針を含める
- 最後に未確認事項と追加テスト候補を必要最小限でまとめる
