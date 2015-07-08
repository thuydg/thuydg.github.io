---
layout: blog
title: iBeacon app developing
category: blog
tags: [blog, iBeacon, ios]
summary: How to add comment function to blog
image:
---


# What is beacon and iBeacon?

簡単に間違えるんだけど、beaconはメインテクノロジーです。

　　　Beaconとは、Bluetooth Low Energy（BLE）を使ってスマートフォンの位置情報を特定し、
　　　ロケーションに合わせて必要な情報を配信する仕組みのこと。　
　　　アップルが「iBeacon」という名称でiOS 7に搭載したことから注目を集めた技術で、
　　　Android 4.3以降でもBLEを使った同様の仕組みを提供可能だ。
　　　＜ソース：ITmedia＞

位置情報関連はGPSがあるが、精度および室内ではGPSは対応しない場合があるので、
beaconを利用し、位置情報を把握し、活用することが多い。
beaconなぜ注目されているかというと、O2Oアプリは今後はやりじゃないかとのこと。

　　　O2Oとは、Online to Offlineの頭文字を取ったもので、
　　　「インターネット(オンライン)の活動を実店舗(オフライン)に活かすこと」を意味します。
　　　＜ソース：富士通＞

クーポンの情報情報などオンライン情報をオフラインの状況により、活かすことができるので、
beaconとO2Oには相性がいいと言われている。
ただし、クーポンなどだけではなく、様々な場面で利用可能と考えれる。


# Make your iphone become a beacon to test

iOS7からiBeaconが標準化され、CoreLocationというライブラリを使うことで、
iBeaconを制御することはできる。

以下のページを参考し、サンプルアプリを取得し、iPhone(iOS7以上)で
iBeaconデバイスとして試すことはできる。　
→ [iBeacon document](https://developer.apple.com/ibeacon/)
→ [Airlocate sample](https://developer.apple.com/library/ios/samplecode/AirLocate/Introduction/Intro.html)

# 事前準備

* ニフティクラウドmobile backendのアカウント登録
* ニフティクラウドmobile backendcでのデーターインポート
 - Beaconデーター（データーストア）
 - Couponデーター（ファイルストア）
* テンプレートアプリをダウンロード
 - 二つtable viewがある状態

# テスト条件
* Apple iOS developer program
* Xcode installed (v6.0以上)
* iOS device (iPhone, iPad) with Bluetooth ON

# Create iOS O2O apps

# <STEP1> iBeacon receiver developer
  - Applicationを作成（Single view）
  - CoreLocation frame workをLinked Frameworkをインストール
  - Background Capabilitiesを設定：
   「Capabilities」->「Background modes」ON
    ->「Location updates」「Use Bluetooth accessory」Checked!
  -  

# <STEP2> Mobile backend server データーを取得し、iBeaconを発見する時、情報を出す
  -
# <STEP3> Coupon情報を取得する

# Other

# Reference

* [O2Oだけじゃない BLEを使った「Beacon」の可能性](www.itmedia.co.jp/mobile/articles/1406/04/news090.html)
* [iOS app develop with ibeacon](http://ibeaconmodules.us/blogs/news/14279747-tutorial-ibeacon-app-development-with-corelocation-on-apple-ios-7-8)
