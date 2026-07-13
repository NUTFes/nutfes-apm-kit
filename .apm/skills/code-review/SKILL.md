---
name: NUTFes Code Review
description: PR や diff のコードレビューを行うための Skill。「このPRをレビューして」「diffを見て」「レビューコメントちょうだい」といった依頼で必ずトリガーする。Rails / Next.js / Go(Echo) の技術スタックに対応し、影響範囲調査と2パスレビューを必須手順とする。
---

# NUTFes Code Review

diff の表面だけを見たレビューではなく、呼び出し元や既存コードへの影響まで踏まえたレビューを行う。
指摘は重要度付きで整理し、好みレベルのノイズを削って本当に必要なものだけを残す。

## レビューの流れ

### Step 0. レビュー用ワークツリーの作成（省略しない）

作業中のブランチを崩さずにレビューするため、対象ブランチを別ディレクトリに展開する。

```bash
git fetch origin <対象ブランチ>
git worktree add ./review-<PR番号> origin/<対象ブランチ>
cd review-<PR番号>
```

レビュー後は `git worktree remove ./review-<PR番号>` で片付ける。

### Step 1. 影響範囲の調査（diff を読む前に必ず実施する）

> この手順を省略しない。変更ファイルの中身だけを見てレビューを始めない。

以下を Grep / Read でリポジトリ全体に対して調査する。

- 変更した関数・クラス・メソッドを呼び出している既存コード
- 変更したテーブル・スキーマを参照している他のクエリ・モデル
- 変更した API エンドポイントを利用しているフロントエンド・他サービス
- 既存テストが意図せず壊れる可能性がある箇所

### Step 2. ガイドラインの動的選択

`.apm/skills/code-review/guidelines/cross-cutting.md` は常に読み込む。変更内容に応じて以下も追加で読み込む。

| 変更対象 | 追加で読むガイドライン |
|---|---|
| Rails (Controller / Model / Service) | `guidelines/rails.md` |
| Next.js (コンポーネント / API Route) | `guidelines/nextjs.md` |
| Go / Echo (ハンドラ / ミドルウェア) | `guidelines/go-echo.md` |

技術スタックが増えたら `guidelines/` にファイルを追加し、この表を更新する。

### Step 3. 第1パス：網羅的リストアップ

気になった点を重要度を問わずすべて列挙する。この段階では絞り込まず、見落としを防ぐことを優先する。

### Step 4. 第2パス：批判的な絞り込み

第1パスの指摘を見直し、以下を行う。

- 本当に必要な指摘だけに絞る（好み・些末な指摘は削る）
- 重要度を `Critical / High / Medium / Low` で付与する
- 各指摘に、Step 1 で調べた影響範囲の根拠を添える（省略しない）

### Step 5. 出力

- ファイル名・行番号を明記した重要度付きコメントとしてまとめる
- GitHub 連携がある場合は Pending Review のドラフトを作成し、最終確認・Submit は人間が行う

## ガイドラインの自己改善ループ

レビュー完了後、以下に該当する指摘があれば `guidelines/` への追記案を提示する。

- 直近のレビューで同種の指摘が繰り返し発生している
- 既存ガイドラインでカバーされていない新しい観点
- チーム全体に共有すべき設計判断・NG パターン

追記案が採用されたら、リポジトリルートの `apm.yml` の `version` をパッチアップして commit する。
この kit を依存に持つ他プロジェクトは `apm install --update`（`#develop` 利用時）または
`apm.yml` のタグ更新 + `apm install`（タグ固定時）で最新のガイドラインに追従できる。

## あわせて使うもの

- `.apm/prompts/review-web.prompt.md`（Next.js / React 単体の findings-first レビューが必要な場合）
