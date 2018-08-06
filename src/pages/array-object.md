---
path: "/array-object"
date: "2018-08-06T23:55:00Z"
title: "一つしかオブジェクトがはいってない配列をオブジェクトとして扱う"
tags: ["JavaScript"]
excerpt: "一つしかオブジェクトがはいってない配列をオブジェクトとして扱う"
---

例えば、複数のオブジェクトが詰め込まれた配列があるとする。

そのオブジェクトのとあるパラメータがユニークなもので、そのパラメータを元に一つに絞り込みたかった。

## 結論
配列を代入するときに、変数を`[]`で囲む。

```javascript
const [obj] = array
```

例えば、次のような形

```javascript

const array= [
  {
    key1: 123
  }
];

const [obj] = array;

console.log(obj); // { key1: 123 }

```

## どういうこと？
**分割代入**という。

### 分割代入
> 分割代入 (Destructuring assignment) 構文は、配列から値を取り出して、あるいはオブジェクトからプロパティを取り出して別個の変数に代入することを可能にする JavaScript の式です。

[分割代入 \- JavaScript \| MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

サンプルコードが結構あるので参照するといい。スプレッド演算子と組み合わせたりもできる。オブジェクトでも使える。

数学でいう恒等式に似ている気がする。

## ブラウザ実装状況
Edgeで使えない。ちゃんとトランスパイルすること。

[分割代入 \- JavaScript \| MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)

## thx
ちなみにこれは[@_yuheiy](https://twitter.com/_yuheiy)にエアリプで教えてもらったものです。
