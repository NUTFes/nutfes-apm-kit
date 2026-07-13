# nutfes-apm-kit

NUTFes の Web 系リポジトリで再利用するための APM パッケージです。共通の開発方針、Web レビュー用プロンプト、Next.js/React 実装フローのスキルをまとめて配布します。

このパッケージは、各プロダクトが Docker ベースの開発環境を持ち、日常の作業コマンドも `make` / `mise` / `docker compose` などの repo 既存ラッパー経由で実行される前提で設計しています。

## 何を提供するか

- `.apm/instructions/`
  - チーム共通の開発フロー
  - TypeScript / React 実装時の基本方針
  - Next.js のルーティングと Server Component 優先方針
  - Web UI のアクセシビリティ基準
- `.apm/prompts/`
  - findings-first の Web レビュー
  - repo 文脈を踏まえた実装計画
  - PR 前のリリースチェック
  - PR番号を指定して発火する PR コードレビュー（`/review-pr <pr_number>`）
- `.apm/skills/`
  - NUTFes 系 Web リポジトリ向け実装フロー
  - Next.js / React 向けレビュー手順
  - Rails / Next.js / Go(Echo) 向け PR コードレビュー（影響範囲調査 + 2パスレビューを必須化）

v1 では agents / hooks / MCP / transitive dependencies は含めません。

## 標準の使い方

通常は `develop` を更新チャネルとして使います。

```bash
apm install NUTFes/nutfes-apm-kit#develop
```

利用側の `apm.yml` は次のようになります。

```yaml
name: your-project
version: 1.0.0
dependencies:
  apm:
    - NUTFes/nutfes-apm-kit#develop
```

依存関係を追加済みの repo では、以後は通常の install で再展開できます。

```bash
apm install
```

## 開発フローの前提

このパッケージが想定する各プロダクトの作業方針は次の通りです。

- 開発環境は Docker ベースで扱う
- コマンド実行は、まず `make`、次に `mise run`、その次に `docker compose exec` / `docker compose run` を探す
- ホストでの `npm` / `pnpm` / `yarn` / `python` / `go` 直実行は、repo がそれを正式入口にしている場合を除いて避ける
- lint / typecheck / test / build も同じく repo の公式ラッパー経由で実行する

つまり、このパッケージは「Docker 上で動くプロダクトに対して、repo が用意したコマンドツールを使って開発を進める」ための共通ルール集です。

## 固定版の使い方

安定版を固定したい場合はタグを使います。

```bash
apm install NUTFes/nutfes-apm-kit#v0.1.0
```

利用側の `apm.yml` 例:

```yaml
name: your-project
version: 1.0.0
dependencies:
  apm:
    - NUTFes/nutfes-apm-kit#v0.1.0
```

## 更新方法

### `#develop` を使っている repo

最新の `develop` を取り込みたいときは次を実行します。

```bash
apm install --update
```

`apm.lock.yaml` が更新され、最新の commit に解決し直されます。

### タグ固定の repo

`apm.yml` の ref を目的のタグへ更新してから install を実行します。

```yaml
dependencies:
  apm:
    - NUTFes/nutfes-apm-kit#v0.2.0
```

```bash
apm install
```

## Codex / OpenCode / Gemini での利用

Copilot / Claude / Cursor は `apm install` のネイティブ配置だけで利用できます。

Codex / OpenCode / Gemini では instruction を `AGENTS.md` にコンパイルするため、install 後に次を実行してください。

```bash
apm compile
```

必要に応じて Codex 向けを明示する場合:

```bash
apm compile --target codex
```

`apm compile` が成功表示でも `AGENTS.md` が生成されない場合は、利用側の APM を最新版に更新して再試行してください。

## このパッケージを更新する運用

標準運用は `develop` ブランチです。利用例でも常に `#develop` を明示し、既定ブランチに依存しないようにします。

リリースを切るときは次の順で運用します。

1. `apm.yml` の `version` を更新する
2. README のタグ例を必要なら更新する
3. `develop` を安定化させる
4. `vX.Y.Z` タグを切る

タグは「固定配布用」、`develop` は「継続更新用」です。

## authoring / 検証

この repo 自体を APM パッケージとして検証するときの基本コマンド:

```bash
apm install --dry-run
```

consumer 側の確認例:

```bash
apm init
apm install /path/to/nutfes-apm-kit
apm audit
apm compile --target codex
```

確認対象:

- `apm.yml`
- `apm.lock.yaml`
- `.github/`
- `.claude/`
- `.cursor/`
- `.opencode/`
- `.agents/skills/`
- `.codex/agents/`
- `AGENTS.md`

## 構成

```text
.
├── apm.yml
└── .apm
    ├── instructions
    ├── prompts
    └── skills
        ├── code-review
        │   └── guidelines
        ├── web-feature
        └── web-review
```
