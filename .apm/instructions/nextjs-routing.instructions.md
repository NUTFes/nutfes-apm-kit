---
description: Next.js の routing / rendering 方針
applyTo: "{app,src/app,pages,src/pages}/**/*.{ts,tsx,js,jsx}"
---

# Next.js Routing 方針

- App Router を使う repo では Server Component を優先し、`use client` は本当に必要な境界だけに限定してください。
- client component にする理由は、フォーム操作、browser API、interactive UI など明確な要件がある場合に限ってください。
- 取得可能なデータは server 側で解決し、client 側で同じ取得を重複させないでください。
- `app/` や `src/app/` 配下では、route segment、`layout`、`page`、`loading`、`error`、`not-found` の役割を崩さないでください。
- `pages/` や `src/pages/` 配下では、既存の data fetching 方式と routing convention を維持してください。
- ルート追加時は URL 設計、認可要件、breadcrumb や navigation への影響も確認してください。
- 画面単位で loading / error を置ける場合は、ユーザー体験として自然な粒度で配置してください。
- API route や server action を追加する場合は、入力検証、認可、失敗時レスポンス、監査しやすさを意識してください。
