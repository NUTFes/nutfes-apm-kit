# Next.js レビュー観点

> このファイルはテンプレートです。App Router / Pages Routerどちらを使っているか、
> Storybookの運用ルールなど、実際のプロジェクトに合わせて調整してください。
> `.apm/instructions/nextjs-routing.instructions.md` / `typescript-react.instructions.md` /
> `ui-accessibility.instructions.md` とあわせて使うことを想定しています。

## コンポーネント設計

- [ ] Server Component / Client Componentの使い分けが適切か（不要な `"use client"` がないか）
- [ ] propsのバケツリレーが深くなっていないか
- [ ] 新規・変更コンポーネントにStorybookのstoryが追加されているか

## データフェッチ

- [ ] APIのエラーレスポンスに対するハンドリング（ローディング・エラー状態）があるか
- [ ] バックエンド（Rails API等）の型定義とフロントエンドの型がずれていないか

## パフォーマンス

- [ ] 不要な再レンダリングを招く実装がないか（依存配列・memo化の漏れ）
- [ ] 画像最適化・バンドルサイズへの影響が大きい変更でないか

## 移行系タスク特有の観点（Nuxt→Next.js移行など）

- [ ] 移行元と移行先で挙動差分（SEO・ルーティング・状態管理）がないか
- [ ] 段階移行中の場合、新旧実装の混在箇所が明示されているか
