---
marp: true
---

<!--
theme: gaia
_class: lead
-->

# Webの振り返りとHTTP

---

<!--_class: lead -->

最初に

## 最近のWebアプリ開発事情を棚卸し

Webアプリ開発？　→　HTTPに乗るもの、関連するものすべて

---

## 最近のWebアプリ開発事情

- フロントエンドWebアプリフレームワーク（React、Vue、Angular）
- バックエンドWebアプリフレームワーク（Laravel、Rails、Express）
- データベース（RDB、NoSQL）
- クラウド（AWS、GCP、Azure）
- コンテナー（Docker、Kubernetes）
- プロトコル（HTTP、TCP/IP、SSL/TLS、gRPC）
- …

**↑ 混沌**（この内容はほとんど出てきません）

---

## この資料について

- 目的
  - Webについて分かった気にさせる
    - 前編：Webを振り返って技術の流れを把握する
    - 後編：HTTP、TCPについての理解を深める

---

## このスライドの内容

- 前編：Webを振り返って技術の流れを把握する
  - ブラウザの仕事
  - ブラウザとWeb技術の移り変わり
- 後編：HTTP、TCPについての理解を深める
  - HTTP、TCPを知る
  - HTTP通信の流れ

- まとめ

---

<!--_class: lead -->

## 前編：Webを振り返って技術の流れを把握する

---

<!--_class: lead -->

## ブラウザの仕事

---

## 主な機能

HTMLやCSSなどを取得し、
パースして、画面に表示する。
JavaScritpの実行もする。

- レンダリングエンジン
  - HTML解析→DOM Tree
  - CSS解析→Style Rules
  - 画面表示
- JavaScriptエンジン

![bg left](images/001/google.com.png)

---

## DOM

Document Object Model

ブラウザ内部でHTMLは
DOMツリーとして保持される。

JavaScriptからDOMのルート
「Document」オブジェクト
を通じてDOMを操作できる！

```js
document.getElementById('foo')

$('#bar').innerHTML = 'sample'
```

![bg left 90%](images/001/dom.png)

---

## JavaScript実行環境

- JIT型
  - Chakra Legacy（IE11）
  - Chakra（Edge）
  - SpiderMonkey（Firefox）
  - V8（Chrome、Node.js）
- インタプリタ型

  - Ignition（V8）（Android Chrome）

---

<!--_class: lead -->

## ブラウザとWeb技術の移り変わり

---

<!-- W3Schoolsによるウェブブラウザの利用統計 -->

![bg width:98% ](images/001/browsershare.png)

---

## 〜2004年

- IE全盛期（IE 6）
- FLASH黄金時代

この頃のJavaScriptは
「ちょっと動きを加えるもの」

リッチなものは全部FLASH！
JavaScriptは無効に設定！

WebアプリはLAMPが最強

![bg left 51%](images/001/browser2004.png)

---

## 〜2006年

- IEまだ強い（IE 7）
- Firefox

- Ajax、jQuery

2005年にGoogle Mapsが登場。

![bg left 34%](images/001/browser2006.png)

---

## 2005年：XMLHttpRequest（Ajax）

Webブラウザのスクリプト言語（JavaScriptなど）から
サーバとHTTP通信を行うためのに用意されたブラウザのAPI。

Goole MapsでXMLHttpRequestが有名になり、
Ajaxという言葉が生まれる。（Asynchronous JavaScript + XML）

しかしまだクライアントプログラミングの敷居は高い…。

.
※ ほかのWebブラウザのスクリプト言語
　Javaアプレット、VBScript、JScript、ActionScript、Silverlight環境など

---

## 2006年：jQuery

クライアントプログラミングの敷居を一気に下げた存在

- かんたんDOM操作
- かんたんイベント処理
- かんたんAjax
- ブラウザによる挙動の差異を吸収

やりたいことがそこそこ良いカンジでできる。（まだまだ現役！）

```js
$('#hoge')
```

---

## 2006年：jQuery②

なにが辛いか

- 値の管理
- DOMの状態管理
- イベントの発火管理
- ...

コンポーネントが増えるたび、やることが指数関数的に増えていく。

**一部の職人にしか成し得ない超絶技巧プログラミング**

---

## 〜2009年

- PHPフレームワーク乱立問題
- 2004年生まれのRuby on Railsが頭角を表す
- IE（IE 8）以外のブラウザがシェアを伸ばし始めた時代

タブブラウジング、フィードリーダー、自前のレンダリングエンジン搭載のような独自機能を追加したブラウザがたくさん生まれた。

![bg left 50%](images/001/browser2009.png)

---

## 〜2012年

- IE（IE 9、10）完全に下火
- HTML5/CSS3の対応が進む
  - WebSocketが登場
- FuelPHP、Laravelはこのへん

- **クラウド**ブーム

CSS3のメディアクエリ `@media`
→ レスポンシブデザインが主流

![bg left 48%](images/001/browser2012.png)

---

## HTML5とSingle Page Application

2011年の時点ですでに多くのブラウザがHTML5に対応していた。
（IE 9、Firefox 3.5、Chrome 3.0など）（HTML5の正式な勧告は2014年）

HTML5では `history.pushState()` を使ってURLの動的書き換えが可能

→ ネイティブアプリのように、ブラウザのページ遷移を使わず
　複数ページあるWebアプリを作成することが可能に！

→ **シングルページアプリケーション**！！

---

## jQueryとSingle Page Application

jQuery + Single Page Application…？

- ただでさえ辛いjQuery
- **考慮しないといけない点が増えすぎる**
  - ページ管理
  - ページを跨いだデータ、イベント管理
  - 今までブラウザが管理していた情報をクライアントが管理
    - `history.back()` でのスクロール位置保持など

正気の沙汰ではない。

---

## 〜2016年

- **React**（2013年）
- Docker（2013年）
- Vue.js（2014年）
- TypeScript（2014年）
- Kubernetes（2015年）

Reactの台等もあり、SPA +
APIサーバーのアプリが主流に

![bg left 59%](images/001/browser2016.png)

---

## React

- Facebook製ライブラリ
- ユーザインタフェースを構築
- コンポーネント指向

- **VirtualDOM**

jQueryを使って自分でDOMを
操作しなくていい時代が到来！

![bg right 100%](images/001/react.png)

---

## Virtual DOM（仮想DOM）

ブラウザのDOMと対になる、Reactが保持する構造体。

1. ブラウザでアクションが発生するとReactは仮想DOMを変更
2. 変更前の仮想DOMと変更後の仮想DOMを比較し、差分を抽出
3. ReactがブラウザのDOMを変更

Reactが内部でdiff/patchしてくれるため、直接DOMを触る必要がない。

→ **把握・管理しないといけないものが減り、SPAが作りやすくなった**

---

## 前半の内容

- ブラウザの仕事
  - レンダリングエンジン
  - JavaScriptエンジン
- ブラウザとWeb技術の移り変わり
  - Ajax、jQuery
  - SPA、React
  - 主要なWeb技術の登場シーン

---

<!--_class: lead -->

## 後編：HTTP、TCPについての理解を深める

---

<!--_class: lead -->

## HTTP、TCPを知る

---

## HTTP

主にWebでブラウザ・サーバー間の通信に使われる**プロトコル**。

- http://example.com
- https://google.com

https（HTTP Secure）はHTTPの暗号化通信をするやつ。
（最近のブラウザは `http` だと怒る

![width:1000](images/001/example.com.png)

---

## プロトコル？

現代のネットワーク技術を説明するにはレイヤーという概念がとても便利。
プロトコルの仕事を分けた **TCP/IP参照モデル** などが存在する。

階層|担当|プロトコル例
--|--|--
アプリケーション層|アプリ|**HTTP**, TLS, SMTP, DNS
トランスポート層|OS|**TCP**, UDP
インターネット層|OS|IP（IPv4、IPv6）
ネットワークインターフェイス層|ドライバー|Ethernet, Wifi, PPP

---

## TCP

- 送受信の通信規約
- コネクションを繋げて通信
- データロスを検知し、再送
  （データの到着を保障）
- 到着順序を保障
- 通信速度を考慮

- いろいろ機能付いてる
  高機能プロトコルTCP

![bg left 80%](images/001/tcp.png)

---

## UDP

- コネクションレス
  繋がってる相手を管理しない
- 一方的にデータを送りつける
- データロスの検知なし
- 通信速度の制限なし
- 到着順序の管理なし

- 高機能なTCPと比べて
  かなりシンプルで早い

![bg left 80%](images/001/udp.png)

---

## HTTP通信

- HTTPはTCPの上に乗るプロトコル
- HTTPリクエスト/レスポンスの書式、ヘッダーの項目などを定めている

- **データ通信のプロトコルではなく、**
  **送受信するデータをどう解釈するかを定めたプロトコル**
  （インターネット間のデータ通信自体はTCP/IPで行われる）
  - どう解釈するかは使用するWebサーバーの実装次第

基本はHTTPリクエストを送り、HTTPレスポンスを受け取る1往復の通信

---

![bg 75%](images/001/http.png)

---

## （悪い例）

![bg 75%](images/001/http_bad.png)

---

## ！！何か切らないと…

長すぎいい

- POSIX
- プロセス（プロセスディスクリプター）
- ファイルディスクリプター
- システムコール、シグナル
- ソケット通信

---

<!--_class: lead -->

## HTTP通信一連の流れ

？
