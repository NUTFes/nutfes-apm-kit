---
description: TypeScript / React 実装時の共通方針
applyTo: "**/*.{ts,tsx,js,jsx,mts,cts,mjs,cjs}"
---

# TypeScript / React 方針

- `any` は原則禁止です。やむを得ない場合は範囲を最小化し、代替型を検討した理由を残してください。
- 型は利用箇所の近くで読みやすく保ち、既存 repo に schema や domain type があるなら再利用してください。
- nullable / optional の扱いは曖昧にせず、UI とデータ境界で明示的に処理してください。
- React の state は最小限に保ち、derived state を増やしすぎないでください。
- 既存 repo が `react-hook-form`、server actions、query library、custom hooks などのパターンを持つ場合は、それに合わせてください。
- props は責務ごとに整理し、巨大な component にロジックを詰め込みすぎないでください。
- UI 実装では empty、loading、error、disabled の各状態を最初から考慮してください。
- 非同期処理は例外経路を含めて扱い、ユーザー操作失敗時の表示や再試行導線を意識してください。
- 不要な `useEffect`、過剰な client state、場当たり的な `console.log` を増やさないでください。
