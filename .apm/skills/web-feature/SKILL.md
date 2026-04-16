---
name: NUTFes Web Feature
description: NUTFes の Web 系リポジトリで機能追加を進めるための実装フロー
---

# NUTFes Web Feature

## 目的

NUTFes の Next.js / React / TypeScript ベースのリポジトリで、新機能や改修を進めるときの標準フローを共有します。

## いつ使うか

- 新しい画面やフォームを追加するとき
- 既存 UI の改善や画面遷移の変更を行うとき
- API 接続や state 管理を伴う Web 実装を進めるとき

## 手順

1. 先に repo の README、ディレクトリ構成、package manager、scripts、既存パターンを確認する
2. 変更対象に近い画面、component、hook、API client を探し、既存の流儀を把握する
3. 追加する state、validation、data flow、loading / error / empty state を先に整理する
4. `use client` が本当に必要かを確認し、server-first で実装できないかを検討する
5. UI は semantic HTML、keyboard 操作、responsive を前提に構成する
6. 実装後は repo 既存の lint / typecheck / test / build を実行し、未実施があれば明記する

## 判断基準

- 型を曖昧にしない
- repo の既存パターンを壊さない
- 変更を最小限にする
- 例外系の UX を後回しにしない

## あわせて使うもの

- `review-web.prompt.md`
- `plan-feature.prompt.md`
- `release-check.prompt.md`
