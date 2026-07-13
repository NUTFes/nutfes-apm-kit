# Rails レビュー観点

> このファイルはテンプレートです。実際のリポジトリで採用している設計方針
> （Service層をどこまで使うか、Fat Modelを許容するかなど）に合わせて書き換えてください。
> 過去のPRレビューで繰り返し指摘してきたパターンがあれば、ここに追記していくと精度が上がります。

## レイヤー責務

- [ ] Controllerにビジネスロジックが書かれていないか
- [ ] N+1を誘発するクエリがController/Viewに書かれていないか
- [ ] Modelのスコープ・クエリを直接組み立てている箇所で、共通化できるものはないか

## API設計（Rails APIモード + フロントエンド分離構成）

- [ ] レスポンスの形がOpenAPI/OAS定義と一致しているか
- [ ] ステータスコードが処理内容に対して適切か（404/422/500の使い分け）
- [ ] 破壊的変更がある場合、フロントエンド（Next.js）側の呼び出し元に影響がないか

## マイグレーション

- [ ] ロールバック可能な設計になっているか
- [ ] 対象テーブルが大きい場合、ロックが長時間発生しないか
- [ ] Seed/Fixtureへの影響（コールバックの副作用など)が考慮されているか

## テスト・コード生成

- [ ] scaffdogなどで生成した雛形に対して、生成後の手動修正がテストに反映されているか

## NGパターン例（プロジェクトごとに追記）

```ruby
# 例: Controllerにロジックが漏れている
class OrdersController < ApplicationController
  def create
    order = Order.find(params[:id])
    if order.status == "pending" && current_user.premium?
      order.update!(status: "confirmed", discount: 0.1)
    end
  end
end
```
