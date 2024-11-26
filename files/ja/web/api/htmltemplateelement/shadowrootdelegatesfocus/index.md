---
title: "HTMLTemplateElement: shadowRootDelegatesFocus プロパティ"
short-title: shadowRootDelegatesFocus
slug: Web/API/HTMLTemplateElement/shadowRootDelegatesFocus
l10n:
  sourceCommit: 26091e4af9c73bb6c5d1466df5070c949498fdbd
---

{{APIRef("Web Components")}}

**`shadowRootDelegatesFocus`** は {{domxref("HTMLTemplateElement")}} インターフェイスのプロパティで、関連付けられた [`<template>`](/ja/docs/Web/HTML/Element/template) 要素の [`shadowrootdelegatesfocus`](/ja/docs/Web/HTML/Element/template#shadowrootdelegatesfocus) 属性の値を反映します。

このプロパティは開発者にとって有用ではないことに注意してください。
`<template>` 要素を使用して宣言的に [`ShadowRoot`](/ja/docs/Web/API/ShadowRoot) を作成する場合は、このオブジェクトおよびプロパティは存在しません。
それ以外の場合、`HTMLTemplateElement` が作成された場合は、オブジェクトがシャドウルートではないため、このプロパティの値は無関係であり、シャドウルートに変更することはできません。

## 値

関連付けられた [`<template>`](/ja/docs/Web/HTML/Element/template) 要素の [`shadowrootdelegatesfocus`](/ja/docs/Web/HTML/Element/template#shadowrootdelegatesfocus) 属性の値を反映します。

## 仕様書

{{Specifications}}

## ブラウザーの互換性

{{Compat}}

## 関連情報

- [`shadowrootdelegatesfocus`](/ja/docs/Web/HTML/Element/template#shadowrootdelegatesfocus)（`<template>` 要素の属性）
- [`ShadowRoot.delegatesFocus`](/ja/docs/Web/API/ShadowRoot/delegatesFocus)