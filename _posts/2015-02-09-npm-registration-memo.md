---
layout: blog
title: npm registrations notes
category: blog
tags: [node.js]
summary: A memo of what is needed to register a node.js package to npm
image: http://manaten.net/wp-content/uploads/2013/07/nodejs-image-processing.png
---


# Javascript template（モジュールの書き方）：


ブラウザでも Web Worker でも node.js でも使えるような書き方でグローバルオブジェクトを取得

{% highlight JavaScript %}
(function(global) {
    "use strict";

    // ...
})((this || 0).self || global);
{% endhighlight %}

global オブジェクトに Module を突っ込みると

{% highlight JavaScript %}
(function(global) {
    "use strict;"

    // Your Module
    function YourModule() {
        // ...
    };

    // Exports
    if ("process" in global) {
        module["exports"] = YourModule;
    }
    global["YourModule"] = YourModule;

})((this || 0).self || global);
{% endhighlight %}

ヘッダーを入れる
{% highlight JavaScript %}
(function(global) {
    "use strict;"

    // Class ------------------------------------------------
    function YourModule() {
    };

    // Header -----------------------------------------------
    YourModule["prototype"]["method"] = YourModule_method; // YourModule#method(someArg:any):void

    // Implementation ---------------------------------------
    function YourModule_method(someArg) {
        // ...
    }

    // Exports ----------------------------------------------
    if ("process" in global) {
        module["exports"] = YourModule;
    }
    global["YourModule"] = YourModule;

})((this || 0).self || global);
{% endhighlight %}


# npm 必要もの一覧：

1. .package.json
2. .npmignore
3. .gitignore
4. .travis.yml
5. index.js
6. test/
⇒　Mocha　テストCode + Makefileのように作る
7. LICENSE
8. README.md
9. node_modules
   External modules
10. lib/
   <index.js  //main code>
   Internal modules // internal code


## 1. package.json

* Node.jsのプロダクトのバージョンやパッケージ依存関係を管理するもの
* 例：
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

## 2. npmignore

* npmにアップする時に、無視するフォルダー一覧の設定


## 3. gitignore

* gitにプッシュする時に、無視する設定

## 4. .travis.yml

Githubにプッシュするときに自動的にテストしてくれるものらしい

> Travis CIは、GitHubにプッシュすると自動的にテストをかけてくれるサービスです。.travis.ymlがその設定ファイルにあたります。
GitHubに上がっているリポジトリだと、ほぼ必ず Build Status みたいのがついてますが、テストをパスしているとこれが緑(passing)になっていて、カッコイイ...もとい安心感があります。

## 5. index.js★



## 6. test/ folder★


## 7. LICENSE

License情報まとめ

## 8. 【README.md】

{% highlight JavaScript %}
[Node package name]

=========
A small library providing utility methods to ....

## Installation
npm install ncmb
## Usage
<Sample code to use the library>
## Tests
npm test
## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style.
Add unit tests for any new or changed functionality. Lint and test your code.
## Release History
* 0.1.0 Initial release
=========
{% endhighlight %}

## 9. node_modules
   External modules

## 10. lib/★
   Internal modules // internal code


# Node configuration

npm set init.author.name "Name"
npm set init.author.email "name@gmail.com"
npm set init.author.url "http://..."

# References:

* [3時間でできるnpmパッケージ公開](http://qiita.com/cognitom/items/75736e27cc7de151a7d5)
* [最近の行儀のよい JavaScript の書き方](http://qiita.com/kaiinui/items/22a75d2adc56a40da7b7)
* [TravisCI](https://travis-ci.org/recent)
