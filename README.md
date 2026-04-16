# nutfes-apm-kit

NUTFes の Web 系リポジトリで再利用するための APM パッケージです。共通の開発方針、Web レビュー用プロンプト、Next.js/React 実装フローのスキルをまとめて配布します。

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
- `.apm/skills/`
  - NUTFes 系 Web リポジトリ向け実装フロー
  - Next.js / React 向けレビュー手順

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
```
