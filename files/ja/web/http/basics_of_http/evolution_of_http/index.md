---
title: HTTP の進化
slug: Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP
l10n:
  sourceCommit: eb9eef29f1ccdaf1c8a464dbe4483c78f7a13b2a
---

{{HTTPSidebar}}

**HTTP** は World Wide Web を支えるプロトコルです。1989 年から 1991 年にかけてティム・バーナーズ＝リーとそのチームによって開発された HTTP は、その柔軟性を形成しながら分かりやすさを維持するために、多くの変化を遂げてきました。HTTP が、実験室でファイルを交換するためのプロトコルから、高解像度や 3D の画像や動画を伝送する現代のインターネットの迷路へと進化していった経緯をご紹介します。

## World Wide Web の発明

1989 年、CERN で働いていたティム・バーナーズ＝リーは、インターネット上のハイパーテキストシステムを構築するための提案書を執筆しました。当初 _Mesh_ と呼ばれていたそのシステムは、1990 年に実装されている間に _World Wide Web_ へ改名されました。 World Wide Web は既存の TCP および IP プロトコル上に構築され、4 つの要素から構成されました。

- ハイパーテキスト文書を表現するテキスト形式である _[HyperText Markup Language](/ja/docs/Web/HTML)_ (HTML)。
- それらの文書を交換するシンプルなプロトコルである _HypertText Transfer Protocol_ (HTTP)。
- それらの文書を表示（および編集）するクライアントである、_WorldWideWeb_ と呼ばれた最初のウェブブラウザー。
- 文書へのアクセス機能を提供するサーバーである、_httpd_ の初期バージョン。

これら 4 つの構成要素は 1990 年の末に完成して、最初のサーバーが早くも 1991 年の初期に CERN の外部で稼働しました。1991 年 8 月 6 日に、ティム・バーナーズ＝リーは _alt.hypertext_ 公開ニュースグループへ[投稿](https://www.w3.org/People/Berners-Lee/1991/08/art-6484.txt)しました。これが、公開プロジェクトとしての World Wide Web の公式な開始日になると考えられています。

初期段階で使用された HTTP プロトコルはとてもシンプルでした。後に HTTP/0.9 と名付けられ、また時にはワンラインプロトコルとも呼ばれました。

## HTTP/0.9 – ワンラインプロトコル

初期バージョンの HTTP にはバージョン番号がありませんでした。以降のバージョンと区別するため、後に 0.9 と呼ばれるようになりました。HTTP/0.9 はとても単純です。リクエストは唯一使用可能なメソッドである {{HTTPMethod("GET")}} で始まって、リソースへのパスが後に続く 1 行で構成されます。サーバーに接続すればプロトコル、サーバー名、ポートが必要ではなくなるため、 URL ではありませんでした。

```http
GET /mypage.html
```

レスポンスも、とても単純でした。こちらはファイル自身だけで構成されます。

```html
<html>
  A very simple HTML page
</html>
```

以降の進化形とは異なり、HTTP ヘッダーがありませんでした。つまり、HTML ファイルだけが転送可能であり、他の種類の文書は転送できませんでした。また、ステータスやエラーのコードはありませんでした。問題が発生すると、人間が使用するために問題の説明を収めた専用の HTML ファイルを生成していました。

## HTTP/1.0 – 拡張性を築く

HTTP/0.9 はとても限定的なものでしたが、ブラウザーとサーバーはすばやくそれをより多用途に使えるようにしました。

- バージョン情報は各リクエストの中で送信されました（`HTTP/1.0` は `GET` 行に付加されました）。
- ステータスコード行もレスポンスの始めに送られるようになりました。これにより、ブラウザーはリクエストの成否を認識し、それに応じて動作を変化させることができるように、例えば、固有の方法でローカルキャッシュを更新したり使用したりすることができるようになりました。
- リクエストとレスポンスの両方に、HTTP ヘッダーの概念が導入されました。メタデータを送信できるようになり、プロトコルは非常に柔軟で拡張性が高くなった。
- {{HTTPHeader("Content-Type")}} ヘッダーのおかげで、プレーンな HTML ファイル以外の文書も送信できるようになりました。

この時点で、一般的なリクエストとレスポンスはこのようになりました。

```http
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

次の接続が続いて、画像の読み込みをリクエストします (前のリクエストのレスポンスに続きます)。

```http
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(画像コンテンツ)
```

1991 年から 1995 年にかけて、これらは試行錯誤で導入されました。サーバーとブラウザーが機能を追加して、それが取得されるかどうかを確認するのです。相互運用性の問題はよくあることでした。これらの問題を解決するために、1996年11月に一般的な方法を記述した情報文書が公開されました。これは {{RFC(1945)}} として知られ、HTTP/1.0 を定義しました。

## HTTP/1.1 – 標準化されたプロトコル

その間に、適切な標準化が進んでいました。これは、HTTP/1.0 の多様な実装を行うために並行して行われました。HTTP の最初の標準バージョンである HTTP/1.1 は、HTTP/1.0 からわずか数カ月後の 1997 年初頭に公開されました。

HTTP/1.1 では、曖昧な点が明確にされ、多くの改良が加えられました。

- 接続を再利用することができ、その時間が短縮されました。単一の元文書に埋め込まれたリソースを表示するために、何度も開く必要がなくなりました。
- パイプラインが追加されました。これにより、最初のリクエストに対する回答が完全に送信される前に、2つ目のリクエストを送信することができるようになりました。これにより、通信の待ち時間を短縮することができるようになりました。
- チャンクレスポンスにも対応しました。
- 追加のキャッシュ制御メカニズムが導入されました。
- コンテンツネゴシエーション（言語、エンコーダー、種類を含む）が導入されました。これで、クライアントとサーバーは、どのコンテンツを交換するかについて合意できるようになりました。
- {{HTTPHeader("Host")}} ヘッダーのおかげで、同じIPアドレスから異なるドメインをホスティングできるようになり、サーバーのコロケーションが可能になりました。

すべて単一の接続で行われる典型的なリクエストの流れは、次のようなものになりました。

```http
GET /ja/docs/Glossary/Simple_header HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/ja/docs/Glossary/Simple_header

200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Wed, 20 Jul 2016 10:55:30 GMT
Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
Keep-Alive: timeout=5, max=1000
Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
Server: Apache
Transfer-Encoding: chunked
Vary: Cookie, Accept-Encoding

(コンテンツ)

GET /static/img/header-background.png HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/ja/docs/Glossary/Simple_header

200 OK
Age: 9578461
Cache-Control: public, max-age=315360000
Connection: keep-alive
Content-Length: 3077
Content-Type: image/png
Date: Thu, 31 Mar 2016 13:34:46 GMT
Last-Modified: Wed, 21 Oct 2015 18:27:50 GMT
Server: Apache

(3077 バイトの画像コンテンツ)
```

HTTP/1.1 は、1997 年 1 月に {{rfc(2068)}} として初版が発行されました。

## 15 年以上にわたる拡張

HTTP の拡張性により、新しいヘッダーやメソッドを簡単に作成することができました。HTTP/1.1 プロトコルは、1999 年 6 月に公開された {{RFC("2616")}} と HTTP/2 のリリース前の 2014 年 6 月に公開された {{RFC("7230")}}-{{RFC("7235")}} という 2 回の改訂を経て改良されたとはいえ、15年以上も極めて安定していました。

### 安全な転送のための HTTP の使用

HTTP の最大の変化が、1994 年末に起こりました。コンピューターサービス会社の Netscape Communications は、HTTP を基本的な TCP/IP スタック上で送信する代わりに、その上にさらに暗号化された送信レイヤーを作成したのです。SSL です。SSL 1.0 は一般にリリースされることはなかったのですが、SSL 2.0 とその後継の SSL 3.0 によって、電子商取引のウェブサイトを作成することができるようになりました。そのために、サーバーとクライアントの間でやり取りされるメッセージを暗号化し、その真正性を保証していました。SSL はやがて標準化され、TLS となりました。

同じ時期に、暗号化されたトランスポート層が必要であることが明らかになりました。ウェブはもはやほとんど学術的なネットワークではなく、広告主や不特定多数の個人、犯罪者が使用可能な限りの個人データを奪い合うジャングルと化していたのです。HTTP で構築されたアプリケーションがより強力になり、アドレス帳、電子メール、ユーザーの位置情報などの個人情報に使用されるようになると、TLS は電子商取引以外のの用途でも必要とされるようになりました。

### 複雑なアプリケーションのために HTTP を使用する

ティム・バーナーズ＝リーは元々、HTTP を読み取り専用のメディアとして想定していたわけではありません。彼は、人々がリモートで文書を追加したり移動したりできるウェブ、つまり分散ファイルシステムのようなものを作成したかったのです。1996 年頃、HTTP はオーサリングを可能にするために拡張され、WebDAV と呼ばれる標準が作成されました。さらに、アドレス帳の項目を処理する CardDAV、カレンダーを扱う CalDAV など、固有のアプリケーションを記載するようになりました。しかし、これらの \*DAV 拡張はすべて、サーバーが実装しなければ使えないという欠点がありました。

2000 年、HTTP を使用するための新しいパターンが設計さ れました。{{glossary("REST", "representational state transfer")}}（またはREST）です。このAPIは、新しいHTTPメソッドに基づくものではなく、基本的なHTTP/1.1メソッドによる固有のURIへのアクセスに頼っていました。これにより、どんなウェブアプリケーションでも、ブラウザーやサーバーを更新することなく、APIにデータを取得したり変更したりさせることができるようになりました。必要な情報はすべて、ウェブサイトが標準のHTTP/1.1で提供するファイルに埋め込まれていました。RESTモデルの欠点は、各ウェブサイトが自分自身で非標準のRESTful APIを定義し、それを完全に制御していたことです。この点は、クライアントとサーバーが相互運用可能であった⽶⽶DAV拡張とは異なる形であった。RESTful APIは、2010年代にとても一般的になりました。

2005 年以降、より多くの API がウェブページで利用できるようになりました。これらの API のうちいくつかは、特定の目的のために HTTP プロトコルを拡張しました。

- [サーバー送信イベント](/ja/docs/Web/API/Server-sent_events)。サーバーがクライアントに対して、特別なメッセージを送信できます。
- [WebSocket](/ja/docs/Web/API/WebSockets_API)。既存の HTTP 接続を更新することでセットアップできる、新たなプロトコルです。

### ウェブのセキュリティモデルの緩和

HTTP はウェブのセキュリティモデルである[同一オリジンポリシー](/ja/docs/Web/Security/Same-origin_policy)とは独立した存在です。実は、現在のウェブのセキュリティモデルは HTTP を作成した後に開発されたのです。長年かけて、一定の条件の下でこのポリシーの制限の一部を解除できるようにすることにより、より寛大にできることが有効であると立証されました。いつどのようにしてこれらの制限を解除するかは、新たな HTTP ヘッダー群を使用してサーバーからクライアントに送信されます。これは[オリジン間リソース共有](/ja/docs/Glossary/CORS) (CORS) や[コンテンツセキュリティポリシー](/ja/docs/Web/HTTP/CSP) (CSP) といった仕様で定義されています。

これらの大きな拡張に加えて、ほかにも実験用に限るものを含めて多くのヘッダーが追加されました。主なヘッダーとしてプライバシーを制御するための Do Not Track ({{HTTPHeader("DNT")}}) ヘッダー、{{HTTPHeader("X-Frame-Options")}}、{{HTTPHeader('Upgrade-Insecure-Requests')}} がありますが、さらに多くのヘッダーが存在します。

## HTTP/2 – 高パフォーマンスなプロトコル

長い年月をかけて、ウェブページはより複雑になっていきました。中には、自分自身でアプリケーションを作成するものもありました。より多くの視覚的なメディアが表示され、インタラクティブな機能を追加するスクリプトの量とサイズも増加しました。より多くのデータがより多くの HTTP リクエストで送信されるようになり、HTTP/1.1 接続はより複雑でオーバーヘッドになりました。この問題を解決するために、Google は 2010 年代前半に実験的なプロトコルSPDYを実装しました。クライアントとサーバー間でデータを交換するこの代替方法は、ブラウザーとサーバーの両方で作業している開発者の関心を集めました。SPDY は、レスポンスの向上とデータの重複送信の問題を定義し、HTTP/2 プロトコルの基礎となりました。

HTTP/2 プロトコルには、HTTP/1.1 との大きな違いがいくつかあります。

- テキスト形式ではなく、バイナリ形式のプロトコルです。このハードルにより内容を読んだり手作業で作成したりすることができなくなりましたが、改良された最適化技術が実装できるようになりました。
- 多重化されたプロトコルです。同じ接続でリクエストを並行して扱うことができ、HTTP/1.x プロトコルの制約を排除しています。
- ヘッダーを圧縮します。一連のリクエスト内で似たものが存在することが多いため、これはデータ転送の重複やオーバーヘッドを削減します。
- サーバープッシュと呼ばれる仕組みによって、リクエストより先にサーバーがクライアントのキャッシュにデータを加えることができます。

2015 年 5 月に正式に標準化された HTTP/2 の使用は、2022 年 1 月にピークを迎え、すべてのウェブサイトの 46.9% に達しました（[こちらの統計情報](https://w3techs.com/technologies/details/ce-http2)をご参照ください）。トラフィックの多いウェブサイトは、データ転送のオーバーヘッドとその後の経費を節約するために、最も急速に普及しました。

このように急速に普及したのは、HTTP/2 がウェブサイトやアプリケーションを変更する必要がなかったからだと思われます。使用するために必要なものは、最新のブラウザーに通信する最新のサーバーだけだったからです。発生させるグループも限られており、古いブラウザーやサーバーのバージョンが更新されれば、ウェブ開発者に大きな作業をさせることなく、自然に利用が拡大しました。

## HTTP/2 以降の進化

HTTP の拡張性は高く、現在も新機能の追加に使用されています。特筆すべきは、2016 年に現れた HTTP プロトコルの新しい拡張機能を挙げることができます。

- {{HTTPHeader("Alt-Svc")}} に対応することで、指定されたリソースの場所と同一性を分離することができ、よりスマートな {{Glossary("CDN")}} のキャッシュ機構を可能にします。
- [クライアントヒント](/ja/docs/Web/HTTP/Client_hints)の導入により、ブラウザーやクライアントがサーバーに対して、クライアントの要件やハードウェアの制約に関する情報を率先して伝えることができます。
- {{HTTPHeader("Cookie")}} ヘッダーにセキュリティ関連の接頭辞が導入され、安全な Cookie が改変されていないことを保証する助けになります。

## HTTP/3 - HTTP over QUIC

HTTP の次のメジャーバージョンである HTTP/3 は、以前のバージョンの HTTP と意味づけは同じですが、トランスポート層部分には {{Glossary("QUIC")}} を {{Glossary("TCP")}} の代わりに使用しています。2022 年 10 月時点で、[すべてのウェブサイトの 26% が HTTP/3 を使用していました](https://w3techs.com/technologies/details/ce-http3)。

QUIC は、HTTP 接続の待ち時間を大幅に短縮することを目的に設計されています。HTTP/2 と同様に多重化されたプロトコルですが、HTTP/2 は単一の TCP 接続上で実行するため、TCP 層で処理するパケットロス検出と再送信によってすべてのストリームをブロックする可能性があります。QUIC は {{Glossary("UDP")}} 上で複数のストリームを実行し、ストリームごとに独立してパケットロス検出と再送を実装するために、エラーが発生した場合、そのパケット内のデータがあるストリームだけがブロックされます。

{{RFC("9114")}} を定義し、Chromium（およびその亜種である Chrome や Edge）や Firefox を含む[ほとんどの主要ブラウザーが HTTP/3 に対応](https://caniuse.com/http3)しています。