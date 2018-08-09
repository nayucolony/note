---
path: '/a-tour-of-go'
date: '2018-08-09T23:20:00Z'
title: 'Go言語の勉強をはじめた'
tags: ['golang']
excerpt: 'A Tour of Goをがんばっている話'
---

## why

- 案件で Go 触らないといけないかもしれなかったから

というのもあるが、なんでもよかったのでサーバーサイドの言語を扱って見たかった。API サーバー作れるようになりたい。

## Start

[動的言語だけやってた僕が、38 日間 Go 言語を書いて学んだこと \- Qiita](https://qiita.com/suin/items/22662f43b6a6e8728798)

- 静的言語…？
- 楽しい言語らしい

## A tour of Go

[A Tour of Go](https://go-tour-jp.appspot.com/welcome/1)をとりあえずやってみることにした。

ちなみに結構ある。

### 内容

- Basics
  - Packages, variables, and functions(**17 ページ**）
  - Flow control statements: for, if, elsem switch and defer(**13 ページ**)
  - More types’ sturctsm slices, and maps.(**27 ページ**)
- Methods and interfaces
  - Methods and interfaces(**26 ページ**）
- Concurrency
  - concurrency(**11 ページ**）

だいたい 100 ページくらいある。１個１個はそんなにおもくない

## Welcome！

- gofmt をつかう
- コンパイルがいるらしい

## Packages, variables, and functions.

変数とか関数の書き方とか

### Packages

- package という単位で構成されるらしい
  - React でいう「コンポーネント」
  - ES でいう「モジュール」あたりに近い
- パッケージ名はインポートパスの最後の要素と同じ名前

### Imports

- factored インポートステートメントという言葉が出てきた
  - 要素化、グループ化、整理済みという意味
  - 一宣言でたくさん読み込むあれ

### Exported names

- 最初の文字が大文字で始まる名前は、外部のパッケージから参照できるエクスポートされた名前
  - JS でいうオブジェクト読み込んで中のプロパティを参照するみたいな感じ

### Functions

- 関数では変数の後ろに型を書く f

### Functions continued

- 引数が全て同じ型の場合は型宣言を一つにまとめていい

### Multiple results

- 関数は腹痛の戻り値を返せる
- JS にはないので（ないよね？）新鮮

### Named return values

- 戻り値に名前をつけられる
- 返り値は型だけを書いてもいいし、返す変数と型を書いてもいい
- 変数名を書いた場合、return に何を返すか書かなくていい
- デファクトはなんなんだろう
- naked return という
- 短い関数でのみ使うべき

### Variables

- var で宣言し、型を書く（関数の時のようにまとめていい）
- 関数とパッケージ内両方で書く

### Variables with initializers

- 初期化子（initializer)
- 変数には初期値を書ける
- 書き方注意
- TS でいう型推論が働くのでこの場合は型宣言不要

### Short variable declearations

- var の代わりに関数内でのみつかえる
- 暗黙の型宣言

### Basic types

- 見たことない奴が結構ある
  - int, uint, uintpr
  - byte
  - rune
  - float32,float64
  - complex64,complex128
- 整数は基本 int で使う
- rune は文字そのもののこと
- %T で変数名、%v で値かな
- 仮引数の宣言の仕方が独特

### Zero values

- 初期値なしで宣言すると与えられる初期値
- 数値は 0
- bool は false
- string は””

### Type conversions

- JS でいう Number()とか String()とかにちかい感じ
- 小数点の削られ方などに注意

### Type interface

- 型推論が行われる話

### Constants

- const で宣言もできる
- 変数ではなく定数
- 文字・文字列・Boolean・数値で使える

### Numeric Constants

- **意味がわからない**
- 多分二進数とかの話

ここまでで、Basics - Packages, variables, and functions が終わり。

続きはまた次回。
