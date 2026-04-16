---
description: NUTFes の Web 系リポジトリで共通に守る開発フロー
applyTo: "**/*"
---

# NUTFes Web 開発フロー

- まず repo の既存構成、README、`Makefile`、`mise.toml`、`docker-compose.yml` / `compose.yml`、package manager、lint、test、build スクリプトを確認し、その repo の流儀を優先してください。
- 新しいツールや依存関係を追加する前に、既存のスクリプトや仕組みで解決できないかを確認してください。
- NUTFes の各プロダクトは Docker ベースの開発環境を前提にしてください。ホストで直接コマンドを叩くより、repo が用意した Docker 経由の実行方法を優先してください。
- コマンド実行は、まず `make <target>`、次に `mise run <task>`、その次に `docker compose exec` / `docker compose run`、最後に repo 既存 script を検討してください。
- `npm test`、`pnpm lint`、`python manage.py`、`go test` などをホストで直接叩く前に、同等の `make` / `mise` / Docker ラッパーが無いか必ず確認してください。
- package manager は repo が採用しているものを維持してください。不要な `npm` / `pnpm` / `yarn` の切り替えは禁止です。
- 変更は最小限にとどめ、無関係なリファクタや命名変更を混ぜないでください。
- 実装後は、影響範囲に応じて lint、typecheck、test、build など既存の検証コマンドを必ず実行してください。検証も Docker / `make` / `mise` の公式経路を使ってください。
- 実行できなかった検証や、環境依存で未確認の点は明確に報告してください。
- `.env`、シークレット、トークン、認証情報、個人情報を新規に出力・埋め込み・共有しないでください。
- migration、seed、外部 API 更新、認証周りの変更は、破壊的変更の有無を必ず明示してください。
- レビューや実装計画では、結論より先に前提、制約、リスク、未確認事項を整理してください。
