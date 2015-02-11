---
layout: blog
title: Web Frontend module management
category: blog
tags: [js]
summary: JavaScript モジュール管理について
image: /images/blog/web-frontend-module.jpg
---

(Src: Web+DBPressから)

# 1. モジュールシステムの必要性：

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

# 2. パッケージマネージャによる環境の準備

* パッケージマネージャPackage managerの準備
  - Package managerとは：ソフトウェアのインストールやアップデート、バージョン管理を行っているソフトウェアです。

## 2.1. npm - Node.jsのパッケージマネージャ

* npmとはNode.jsのパッケージマネージャ
  - Node.jsとはNode.jsはサーバー側で動作するJavaScriptであり、
  大量の処理に対応するために、ノンブロッキングI/Oというモデルを採用しています。
  - 特徴：event driven, non-blocking I/O
* npmの基本使い方

{% highlight JavaScript %}

$npm install browserify
$npm install browserify@6.1.0 //version based
$npm install -g browserify //global install
$npm uninstall browserify
$npm uninstall -g browserify

{% endhighlight %}

* package.json
  - Node.jsの環境設定ファイル
  - Node.jsのプロダクトのバージョンやパッケージ依存関係を管理するもの
  - npm initで対話的に作成可能
  - JSON形式で設定項目が書かれている
  - 依存パッケージ：depedencies（プロダクトを実行において依存）, devDepedencies（実行に依存せず、開発時に利用）
  - [自動的に説明してくれるAutomatic package.json](http://browsenpm.org/package.json)

{% highlight JavaScript %}
{
  "name": "module-name",
  "version": "10.3.1",
  "description": "An example module to illustrate the usage of a package.json",
  "author": "Your Name <you.name@example.org>",
  "contributors": [{
    "name": "Foo Bar",
    "email": "foo.bar@example.com"
  }],
  "dependencies": {
    "primus": "*",
    "async": "~0.8.0",
    "express": "4.2.x",
    "winston": "git://github.com/flatiron/winston#master",
    "bigpipe": "bigpipe/pagelet",
    "plates": "https://github.com/flatiron/plates/tarball/master"
  },
  "devDependencies": {
    "vows": "^0.7.0",
    "assume": "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0",
    "pre-commit": "*"
  },
  "license": "MIT"
}
{% endhighlight %}

  - 以下のようにnpmをinstallする時に自動的に追加可能

  {% highlight JavaScript %}
  $npm install --save browserify
  $npm install --save-dev browserify
  {% endhighlight %}

## 2.2. Bower - Frontend package management

Node.jsはパッケージだけではなく、jQueryやUnderscore.jsなどもパッケージとして管理したい。
フロントエンド向けパッケージ管理マネージャであるBowerを利用。

* 基本使い方：
  - コマンドラインでインストール、アンインストール。ただし、グロバールはありません！
  - 通常、current directoryにinstallされる。

{% highlight JavaScript %}
$ bower install jquery
$ bower uninstall jquery
{% endhighlight %}

* bower.json

  - npmのpackage.jsonと同じ位置づけ。
  - bower initと依存関係があります。

# 3. Browserifyによるモジュール管理

## 3.1. Browserifyの特徴：

### CommonJS style module can be used in browser

* Node.jsではrequire()で、モジュールがロードする
* CommonJS: browserやNode.jsといった実行環境に依存しない、JavaScriptの横断的な標準仕様
* ブラウザーのJavaScriptエンジンはrequire()が存在しないため、BrowserifyはCommonJSスタイルのモジュール管理をブラウザーで利用できる

### npmや組み込みのモジュールそのまま利用可能

* Nodejs依存しない処理は使えません
* FS/fds:require(fs) :NG

## 3.2. Browserifyを使ったビルド:

* require()でのパス解決は事前にビルドプロセスにて実行
* Browserが実行されるファイルはBrowserifyを使って、ビルドされたものである。

### Browserifyのインストール

      npm install -g browserify

{% highlight JavaScript %}
    //module.js
    module.exports = function() {
      console.log("Hellow");
    }
{% endhighlight %}

{% highlight JavaScript %}
    //index.js
    var module = require('./module');
    module();
{% endhighlight %}

### 依存関係の定義

     browserify index.js > bundle.js

# Keywords to remember

* モジュール：モジュールシステムの概要に参考
* Node.js ：
* CommonJS:JavaScriptにおけるモジュールシステムの標準的な概念


# 参考リソース：

* [Node.jsの基本](http://gihyo.jp/dev/serial/01/nodejs/0001)
* [CommonJS](http://www.commonjs.org/)
* []()
