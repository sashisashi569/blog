---
layout: post
title: "Jekyll と GitHub Pages でブログを作る"
date: 2026-04-10 10:00:00 +0900
categories: [技術]
tags: [Jekyll, GitHub Pages, 静的サイト]
excerpt: "Jekyll と GitHub Pages を使って静的ブログを構築する方法をまとめました。"
---

Jekyll は Ruby 製の静的サイトジェネレーターです。GitHub Pages と組み合わせることで、無料でブログを公開できます。

## セットアップ手順

1. リポジトリを作成する
2. `Gemfile` と `_config.yml` を用意する
3. `bundle install` を実行する
4. `bundle exec jekyll serve` でローカル確認
5. GitHub にプッシュすると自動でビルド・公開される

## Markdown で書ける

**太字**、*イタリック*、`インラインコード` など Markdown の基本的な記法がすべて使えます。

```ruby
# Jekyllのサーバー起動
bundle exec jekyll serve --livereload
```

| 機能 | Jekyll | WordPress |
|---|---|---|
| ホスティング費用 | 無料 | 有料の場合も |
| データベース | 不要 | 必要 |
| 速度 | 高速 | サーバー依存 |

Jekyll を使うと、記事はすべてファイルなので Git で管理できるのが嬉しいところです。
