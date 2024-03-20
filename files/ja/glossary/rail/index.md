---
title: RAIL
slug: Glossary/RAIL
---

{{GlossarySidebar}}

**RAIL** とは、**Response, Animation, Idle, Load** の頭文字をとったもので、2015 年に Google Chrome チームが発案した、ブラウザー内のユーザーエクスペリエンスとパフォーマンスにフォーカスしたパフォーマンスモデルです。RAIL におけるパフォーマンスとは、"特定のデバイスでサイトを高速化させることではなく、ユーザーを幸せにすること"です。インタラクションには、ページロード、アイドル状態、入力への応答、スクロールとアニメーションの 4 つのステージがあります。各項目については、以下に頭文字順に解説します。

- **Response**
  - : ユーザーからの何らかの入力を確認した場合、その入力に対する応答が **100 ミリ秒**以内であることです。
- **Animation**
  - : アニメーション中に行われる各フレームの処理が **16 ミリ秒**以内であることです。それは、一貫性もたせ、ジャンクの回避につながります。
- **Idle**
  - : JavaScript のメインスレッドを使用する場合、1 チャンクあたりの処理が **50 ミリ秒**以内であることです。それは、ユーザーインタラクションのためにメインスレッドを開放することにつながります。
- **Load**
  - : インタラクティブなコンテンツの読み込みが **1 秒**以内であることです。

## 関連情報

- [Recommended Web Performance Timings: How long is too long](/ja/docs/Web/Performance/How_long_is_too_long)