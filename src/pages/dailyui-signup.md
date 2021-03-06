---
path: '/dailyui-signup'
date: '2018-08-07T23:40:00Z'
title: '[WIP]SignUpの実装について'
tags: ['DailyUI']
excerpt: '#DailyUI #001 SignUpを実装の面から考える'
---

[Daily UI](http://www.dailyui.co/)の 100 の UI について実装者としての検討を行なっていくシリーズ。第一回目は「Sign Up」。

## 1. Sign Up とは

サインアップとは「署名すること」。契約書に署名をすることで「契約」を交わすことを指します。

サービスにおいては、サービスの顧客となるための操作がサインアップです。

そのため、 アカウント作成フォームをここではつくります。

## 2. 対象ユーザーの検討

対象ユーザーには次の 2 つの状態があります。

- アカウントをもっていない
- アカウントをもっている（間違ってアクセスしてしまった）

前者はアカウントを作成したい、後者はサインアップではなくログインをしたいというステータスです。

## 3. 必要エレメントの検討

### 3-1. アカウントを持っていない人

- メールアドレス
- パスワード
- パスワードの再確認
- 送信ボタン

### 3-2. アカウントを持ってる人

- ログイン画面への導線

#### Q. ログインフォームを併設した方がいいのでは？

**A. 「その場であらゆる状態に対応できる」** より **「取るべき行為がすぐわかる」** が大事。

サインアップフォームとログインフォームが同じ画面にあると、「アカウントをもっている」「もっていない」両方が混乱して得がありません。

シンプルに機能ごとに画面をつくる方が、ユーザーの行動も実装もシンプルになります。

## 4. エレメントの構成

次の点に注意します。

- ラベルとフォームをペアで置く

### 4-1. ラベルとフォームをペアで置く

**「背景に薄く表示する」**ではなく**「ラベルはフォームの外に置く」**ようにしましょう。

#### 「背景に薄く表示する」デメリット

- 入力を開始すると何のフォームかわからなくなる
  - ラベルが外にあれば大丈夫

#### 「ラベルはフォームの外に置く」メリット

- ラベルをクリックするとフォームにフォーカスがあたる
- フォームにフォーカスしようとしなくてもいい

### 4-2. form と button で実装する

例えば、`input`の入力値を取得し、api に投げ込めればサインアップ処理は可能です。
ですが、フォームは`form`と`button`で実装することに大きな意味があります。

#### セマンティクスの明示

「ここからここまでは、サーバーとの情報のやりとりに使う区間ですよ」ということを表すため

#### Enter でリクエストを送信するため

`form`要素で囲まれた`type="submit"`の`button`要素がある場合を考えます。
このとき、ボタンをクリックしたり、フォーカスを当てなくても、`form`要素内のエレメントにフォーカスされた状態で Enter するだけでリクエストを送信できます。

これは、だいぶユーザビリティに関わってきます。下手な UI 検討よりもよほど大事です。
`form`要素で囲まれていなかったり、`button`要素が`type=submit`でない場合はこれがつかえません。

### 4-3. autocomplete 属性をつける

#### メールアドレスの入力エリアには`autocomplete="email"`をつける

`type="emai`" `がついていればメールアドレスはサジェストしてくれはしますが、このように明記できます。

#### パスワードには`autocomplete="new-password"` をつける。

これは新しくパスワードを作る際につける値です。例えばここを`current-password`にすると、あらかじめユーザーに紐づいたパスワードがサジェストされたりします。
ログインの時はそれで ok です。

しかし、サインアップはユーザーの意志でパスワードを選択する必要があります。
不用意なサジェストは避けましょう（ズボラな人は、めっちゃ使い回すので、逆にそっちの方がいいけど……）

1Password はこの部分を頼りに新規生成したりもしているため、ここは明示しましょう。

## 5. メールアドレス系のエラーハンドリング

- すでにそのメールアドレスが登録されている場合
- メールアドレスとして成立していない場合

### 5-1. すでにメールアドレスが登録されている場合

同じメールアドレスでいくつもアカウントを作れたとすると、一つのメールアドレスに複数のアカウントが紐づくことになります。

#### Q.複数アカウントを持つことを前提にするサービスの場合は？

**A. No**

次のような理由から、その仕様は推奨できません。

- 既存のアカウントの存在に気づかずに新しいアカウントが作られる
  - ユーザーはこれを望んでいない
- アカウントはあくまで一つとすべき
  - マイページでインスタンスを作る形式にするのが自然。

### 5-2. メールアドレスとして成立していない場合

例えば次のようなものはメールアドレスとして成立しません。

- @がない
- ドメインがない

この状態ではサインアップするためのリクエストを投げても意味がありません。
リクエストの前に、エラーを表示して修正を促します。

#### Q.すべてのエラー事由に対してユニークなエラー文言を表示すべきか？

**A.No**

エラーが発生する理由は次のようなものが挙げられます。

- メアドじゃなくてアカウント名だとおもった
- メアドじゃなくて電話番号だとおもった
- タイポ

少なくとも、メールアドレスの書き方がわからなくて……は考慮する必要はないでしょう。
「確認してね」で通じると考えられます。

### 5. パスワード系のエラーハンドリング

- 短すぎる場合
- 全角が混ざっている場合
- パスワードとパスワードの再確認が異なる場合

### 5-1. パスワードが短すぎる場合

#### 短すぎる場合

短すぎる（a とか 123 とか）と当然すぐ破られるので避けるべきです。

例えば、1Password のマスターパスワードは 10 文字以下だと短いそうです。

![](https://d2mxuefqeaa7sj.cloudfront.net/s_8F2379537B7E051512EE79ADC42765231AA07C899FC66DA3FEE69A7D84D3ACB6_1533657961554_+2018-08-08+1.05.41.png)

#### A.長すぎる場合は？

**Q.UI 側で制限するべきではない**

パスワード管理アプリの「1password」では最大 64 字のパスワードを生成できます。

たとえば、 `<input type="password" maxlength=12>`のように長さを制限している場合。

この時、生成したパスワードの 13 桁目以降は使われません（12 桁までが入力される）。
すると、手元のパスワードと登録されたパスワードに整合性がなくなったりします。

#### Q.パスワードの強度は何を持って判断するのか？

**A.Dropbox が強さを測るライブラリを提供している**

これを組み込んで可視化するといいでしょう。

[dropbox/zxcvbn: Low\-Budget Password Strength Estimation](https://github.com/dropbox/zxcvbn)

## 参考文献

[The HTML autocomplete attribute \- HTML: HyperText Markup Language \| MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/autocomplete)

[Create Amazing Password Forms \- The Chromium Projects](https://www.chromium.org/developers/design-documents/create-amazing-password-forms)
