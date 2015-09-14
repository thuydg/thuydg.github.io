---
layout: blog
title: monaca app development UI and more ...
category: blog
tags: [monaca, app, develop]
summary: monaca app application development
image:
---

こちらのページでは、monacaでアプリ開発時のTIPsなどメモして行きます。

# 1. MonacaのJQuery mobileのデザインをカスタマイズしたい

JQuery mobileではdata-themeというふうにデザインスタイルを設定する。
a -> z 設定があり、ThemeRollerと呼ばれている。
設定は以下のページがあり、自分でテーム作成することが可能。

[themeroller](https://themeroller.jquerymobile.com/)


# 2. Background画像設定

* Background画像を用意する
Exp: "background.jpg"

* Stylesheet設定

.ui-body-t{
  background-image: url("path/to/background.jpg");
  background-size: contain;
}

きれいにフールで表示するために、background-sizeをcontainに指定する。
ほかにはcover, size(10px 10px), 50% autoがある。
