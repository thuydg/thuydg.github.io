---
layout: blog
title: Web Frontend module management
category: blog
tags: [js]
summary: JavaScript モジュール管理について
image: /images/blog/web-frontend-module.jpg
---

(Src: Web+DBPressから)

# モジュールシステムの必要性：

* モジュールシステムとは：
  - ある機能を持ったコードをモジュールとして定義し、ほかのモジュールがそれを呼び出せる仕組みを提供するシステム
  - このような機能はサーバーサイドの言語では珍しくないが、JavaScriptには存在しない。

* フロントエンドの比重が高まった；
  - Webアプリの大規模化。
  - 近年、サーバーからREST APIとフロントエンドのAjax処理が多くあり、画面遷移処理やユーザーアクションがクライアント側でも引き受けるようになった。
  - また、フロントエンドのコードが増加によって、クライアントMVCという設計手法が注目され、オブジェクトの役割が明確になり、それにあわせて、ファイルも細かく分割するようになる。

* <script>による読み込み順序管理の限界
  - たくさん書かないとけいけないし、依存関係も考慮した読み込み順にする必要がある。
  - JavaScriptのNode.js野場合、CommonJSスタイルのrequireやmodule, exportsという仕組みがあります。
  - ブラウザでも、モジュール管理システムを利用して、管理することは可能。

# パッケージマネージャによる環境の準備

* パッケージマネージャPackage managerの準備
  - Package managerとは：ソフトウェアのインストールやアップデート、バージョン管理を行っているソフトウェアです。

## npm - Node.jsのパッケージマネージャ

* npmとはNode.jsのパッケージマネージャ
  - Node.jsとはNode.jsはサーバー側で動作するJavaScriptであり、
  大量の処理に対応するために、ノンブロッキングI/Oというモデルを採用しています。
  - 特徴：event driven, non-blocking I/O


# Keywords to remember

* モジュール：モジュールシステムの概要に参考
* Node.js：
* Common.jsのデザイン:

# 参考リソース：

* Node.js:
http://gihyo.jp/dev/serial/01/nodejs/0001
