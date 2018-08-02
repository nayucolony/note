---
path: "/my-first-post"
date: "2018-08-02T22:35:00Z"
title: "Gatsbyとgithub pagesでブログをつくった"
tags: []
excerpt: "Gatsbyとgithub pagesでブログを作成してみた"
---

自分のブログを持ちたくなる病に犯され、人生何度目かわからない自分のブログを作った。noteとは別に、手元で文章を管理しておきたいためだ。

## Gatsby
Gatsbyというジェネレータを使った。Reactで動いている。

導入はマジで下記のページの記述をコピペしていたらできた。
[Gatsbyを使ってみる \- Qiita](https://qiita.com/abcb2/items/3731a12866d5c093af48)

Reactの技術を理解していないわけではないがさっさとデプロイしたかったので助かった。


## GraphQL
どうもGraphQLという技術を使っているっぽい。全然なんのことだかわからないが、APIの新しい技術っぽい。

> RESTではURLがひとつのリソースを表すため、複数のリソースが必要な複雑な画面では複数回のAPIリクエストが必要になる。結果的に、綺麗に設計されたRESTful APIほど複数回のリクエストが必要になり、パフォーマンスが落ちたりコードの複雑さが増す欠点があった。
>
> GraphQLでは必要なリソースだけを明示的に記載してリクエストし、必要なリソースを無駄なく1発で取得可能だ。

[GraphQLはRESTの置き換えではない｜こんぴゅ｜note](https://note.mu/konpyu/n/nc4fd122644a1) より

らしい。あと、特定のパラメータだけとかもいけるらしい。これ、すごくないか？

## マークアップ
コンテンツエリアはmarkdownなのでまあいい。ただ他のマークアップはもれなくdiv祭り。デフォルトテーマだし、そもそも自分で色々やってくれという趣旨なのは承知。つど改善していこうとおもう。

## netlify
デプロイはnetlifyで行なっている。なんだかよくわからないうちにnetlifyがリポジトリを作ってnetlifyがデプロイまで繋いでくれていた。すごい。

もともとの[nayucolony\.net](http://nayucolony.net/logo.svg)もそっちに移した。

