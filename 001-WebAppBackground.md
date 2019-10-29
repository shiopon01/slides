---
marp: true
---

<!--
theme: gaia
_class: lead
-->

# Webアプリを支える下回り

---

## この資料について

- 目的
  - フロントエンドWebアプリの歴史を簡単に振り返る
  - TCP、HTTPについての理解を深める

  - Webについて分かった気にさせる

---

<!--_class: lead -->

## （最初に）最近のWebアプリ開発事情、棚卸し

Webアプリ開発？　→ HTTPに乗るもの、関連するものすべてを指す

---

## 最近のWebアプリ開発事情、棚卸し

- フロントエンドWebアプリフレームワーク（React、Vue、Angular）
- バックエンドWebアプリフレームワーク（Laravel、Rails、Express）
- データベース（RDB、NoSQL）
- クラウド（AWS、GCP、Azure）
- コンテナー（Docker、Kubernetes）
- プロトコル（SSL/TLS、HTTPS、gRPC）
- …

↑混沌

---

## このスライドの内容

- Webアプリ技術の移り変わり
  - ブラウザ？
  - SPA？
- TCPとHTTP
  - プロトコル？
  - ソケット通信？

- まとめ

---

<!--_class: lead -->

## Webアプリ技術の移り変わり

---

## ブラウザの仕事

HTMLとCSSを取得し、
パースして、画面に表示する。
JavaScritpの実行もする。

- レンダリングエンジン
- JavaScriptインタープリター

![bg left](images/google.com.png)

---

## DOM

DOM
