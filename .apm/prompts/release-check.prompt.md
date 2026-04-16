---
description: PR 前に lint / typecheck / test / build / env / migration を確認する
author: NUTFes
input:
  - change_summary
---

# Release Check

`${input:change_summary}` を踏まえて、PR 前の最終確認を行ってください。

## チェック項目

1. repo が採用している lint / format / typecheck / test / build コマンドが何か
2. 今回の変更で最低限実行すべきコマンドは何か
3. 実行結果に失敗や未実施があるか
4. migration、seed、schema 変更、環境変数追加、権限変更があるか
5. release note や reviewer への申し送りが必要か

## 出力形式

- 実行すべき確認項目のチェックリスト
- 既に満たした項目
- 未確認またはリスクが残る項目
- PR 説明に含めるべき注意点
