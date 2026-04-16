---
description: Web UI のアクセシビリティと操作性の基準
applyTo: "{app,src/app,pages,src/pages,components,src/components}/**/*.{ts,tsx,js,jsx}"
---

# UI / Accessibility 基準

- クリック可能要素は適切な semantic element を使い、見た目だけの `div` 操作を避けてください。
- キーボードだけで操作できることを前提に、focus 移動、focus 可視化、dialog の閉じ方を確認してください。
- フォームには label、説明文、エラーメッセージを結び付け、必須項目や失敗理由を見落とさせないでください。
- hover 依存の UI にしすぎず、touch device と keyboard 操作でも成立させてください。
- レスポンシブ時の崩れだけでなく、文量増加、long text、empty state でも破綻しない構成にしてください。
- 色だけで状態を伝えず、テキストやアイコン、aria 属性など複数の手段で補ってください。
- skeleton、spinner、disabled 表示は「待っている理由」が分かるように設計してください。
- destructive action や irreversible action では確認導線と安全策を用意してください。
