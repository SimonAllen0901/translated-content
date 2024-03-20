---
title: 一貫性のあるリストのインデント
slug: Web/CSS/CSS_lists/Consistent_list_indentation
---

{{CSSRef}}

リストのスタイル変更でよくあるのが、インデントの幅 (リスト項目がどれだけ右に移動するか) の変更です。あるブラウザーではうまくいっても、別のブラウザーでは同じ効果が得られないことが多いので、これには不満が残ります。例えば、リストに左マージンをなくすと、Internet Explorer ではリストが移動しますが、Gecko ベースのブラウザーでは頑固に固定されてしまいます。この記事では、起こりうる問題を理解し、それを回避する方法をご紹介します。

なぜそうなるのか、もっと大切なことはどうすればその問題を回避できるのか、それを知るためには、リストの構造を詳しく知る必要があります。

## リストの作成

まず、単一の純粋なリスト項目を考えます。このリスト項目は、マーカー (「ビュレット」とも) を持たず、まだリスト自体の一部ではありません。図 1 に示すように、シンプルで飾り気のない、空虚な空間に単独でぶら下がっています。

![図 1](consistent-list-indentation-figure1.gif)

赤い点線の境界線は、リスト項目のコンテンツ領域の外縁を表しています。この時点では、リスト項目にはパディングも境界もないことを覚えておいてください。さらに 2 つのリスト項目を追加すると、図 2 のような結果になります。

![図 2](consistent-list-indentation-figure2.gif)

これらを親要素で囲みます。ここでは順序なしリスト (`<ul>`) で囲みます。CSS のボックスモデルによると、リスト項目のボックスは、親要素のコンテンツ領域内に表示されなければなりません。親要素にはまだパディングもマージンもないので、図 3 のような状況になります。

![図 3](consistent-list-indentation-figure3.gif)

ここでは、青い点線の境界線が、`<ul>` 要素のコンテンツ領域の端を示しています。`<ul>` 要素にはパディングがないので、そのコンテンツは 3 つのリスト項目をぴったりと包み込んでいます。

次に、リスト項目のマーカーを追加します。これは順序なしリストなので、図 4 に示すように、伝統的な塗りつぶした円の「ビュレット」を追加します。

![図 4](consistent-list-indentation-figure4.gif)

視覚的には、マーカーが `<ul>` のコンテンツ領域の外側にありますが、ここで重要なのはその点ではありません。重要なのは、マーカーが `<ul>` ではなく、`<li>` 要素の「主要なボックス」の外に置かれていることです。マーカーはリスト項目の付属品のようなもので、`<li>` のコンテンツ領域の外にぶら下がっていますが、`<li>` には所属しています。

このため、Windows 版の Internet Explorer を除くすべてのブラウザーでは、`list-style-position` の値が `outside` であることを前提に、`<li>` 要素に設定された境界の外側にマーカーが配置されます。これが `inside` に変更されると、マーカーは `<li>` のコンテンツの中に入り、あたかも `<li>` の一番最初に置かれたインラインボックスのようになります。

## 2 回のインデント

では、これらは文書の中でどのように表示されるのでしょうか。現時点では、以下のスタイルに似た状況になっています。

```css
ul,
li {
  margin-left: 0;
  padding-left: 0;
}
```

このリストをそのまま文書に落とし込むと、明らかなインデントがなく、マーカーがブラウザーのウィンドウの左端から外れてしまう危険性があります。

これを回避してインデントを行うためには、ブラウザーの実装者が利用できる選択肢は 3 つしかありません。

1. それぞれの `<li>` 要素に左マージンを設定する
2. `<ul>` 要素に左マージンを設定する
3. `<ul>` 要素に左パディングを設定する

結局のところ、第 1 の選択肢を使っている人はいないようです。2 番目の選択肢は、Internet Explorer と Opera が採用しました。3 つ目は Firefox が採用しました。

ちょっと 2 つのアプローチを見てみましょう。Internet Explorer と Opera では、40 ピクセルの左マージンを `<ul>` 要素に設定することで、リストをインデントしています。`<ul>` 要素に背景色を適用し、リスト項目と `<ul>` の境界線をそのままにしておくと、図 5 のような結果になります。

![図 5](consistent-list-indentation-figure5.gif)

一方で、Gecko は 40 ピクセルの左*パディング*を `<ul>` 要素に設定することで、図 5 と全く同じスタイルを作ることができます。この例を Gecko ベースのブラウザーに読み込むと、図 6 のようになります。

![図 6](consistent-list-indentation-figure6.gif)

見ての通り、マーカーはどの場合でも `<li>` 要素に付けられたままになっています。違いはひとえに `<ul>` の整形方法です。`<ul>` 要素に背景や境界を設定してみて初めて、その違いが分かります。

## 一貫性を探る

煮詰めていくと、こんな感じになります。Gecko、Internet Explorer、Opera の間でリストの表示を統一したい場合は、`<ul>` 要素の左マージンと左パディングの**両方**を設定する必要があります。このためには、`<li>` を意識する必要はありません。Netscape 6.xでの既定の表示を再現したい場合は、次のように書きます。

```css
ul {
  margin-left: 0;
  padding-left: 40px;
}
```

Internet Explorer や Opera のモデルの場合は、次のようになります。

```css
ul {
  margin-left: 40px;
  padding-left: 0;
}
```

もちろん、好きな値を入力することができます。お好みで両方とも `1.25em` に設定してください。ピクセルベースのインデントにこだわる必要はありません。もしリストをインデントがない状態にリセットしたい場合は、パディングとマージンの両方をゼロにする必要があります。

```css
ul {
  margin-left: 0;
  padding-left: 0;
}
```

ただし、そうすると、箇条書きがリストとその親要素の外にぶら下がってしまうことを忘れないでください。親要素が `body` の場合、箇条書きが完全にブラウザーウィンドウの外に出てしまい、表示されなくなる可能性が高くなります。

## まとめ

結局、リストのレイアウトについて、この記事で触れたブラウザーのどれが正しくてどれが正くないとは言えないことが分かりました。既定のスタイルが異なるため、そこに問題が潜んでいるのです。リストの左パディングと左マージンの両方を確実にスタイル付けすることで、リストのインデントをブラウザー間でより一貫性のあるものにすることができます。

## 推奨事項

- リストのインデントを変更する場合は、パディングとマージンの両方を設定するようにしてください。

## 原著情報

- Author(s): Eric A. Meyer, Netscape Communications
- 最終更新日: 2002 年 8 月 30 日発行
- 著作権情報: Copyright © 2001-2003 Netscape. All rights reserved.
- メモ: この記事は、DevEdge サイトに掲載されたものを転載したものです。