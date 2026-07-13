---
description: PR番号を指定してdiffを取得し、影響範囲調査 + 2パスレビューでコードレビューを行う
author: NUTFes
input:
  - pr_number
---

# Review PR

対象PRは `#${input:pr_number}` です。

## 手順

1. 対象repoで以下を実行し、PRの情報とdiffを取得する

   ```bash
   gh pr view ${input:pr_number}
   gh pr diff ${input:pr_number}
   ```

2. `.apm/skills/code-review/SKILL.md` の手順に従ってレビューする
   - レビュー用ワークツリーの作成（Step 0）
   - diffを読む前に影響範囲を調査する（Step 1）
   - 変更した技術スタックに応じたガイドラインを `.apm/skills/code-review/guidelines/` から動的選択する（Step 2）
   - 網羅的リストアップ → 批判的絞り込みの2パスレビュー（Step 3, 4）

3. ファイル名・行番号を明記した重要度付き（Critical / High / Medium / Low）コメントとして出力する（Step 5）
   - GitHub連携がある場合はPending Reviewのドラフトを作成し、最終確認・Submitは人間が行う
