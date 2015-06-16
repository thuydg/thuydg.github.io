---
layout: blog
title: iPhoneで動かすロボット（Romo） apps - mbaas using memo
category: blog
tags: [blog]  
summary: How to add comment function to blog
image:
---

* こちらはニフティクラウドブースで展示したRomoのデモ実装の説明ブログ記事となります。
* ブログには出たサービスは以下となります。
 - [Nifty cloud mobile backend](http://mb.cloud.nifty.com/)
 - [Nifty cloud](http://cloud.nifty.com/)
 - [Nifty cloud MQTT](http://cloud.nifty.com/service/mqtt.htm)

# What is Romo? ロモって何？

公式サイトにより、ロモとは
     Romo（ロモ）はiPhoneやiPod touchを使って楽しくプログラミングを学べる知育ロボットです。
つまり、iPhoneやiPodをつければ、色々できるロボットの一種ですね！

# How to develop for Romo? ロモアップ開発ってどんなこと？

基本的に、iOSアップ開発になりますね。
付けるiPhone/iPodを利用することになるので、
iOSアプリを作ればロモを制御することは可能！
ロモ社からも二つロモ専用のSDKを提供している。

* RM Core Framework（本体を制御）

LEDの制御, iPhoneの角度の制御, 左右のキャタピラの回転

* RM CharacterFremework（アプリ内のキャラクターを制御）

視線や発話や目の開閉、表現と感情

こちらのSDKを使えば、ロモをコントロールするのは簡単そう！

# What I did with Romo?ロモと何をしたのか？

ロモ色々できそうだが、ロモをゲームにし、カートレースするとか、
色々記事がありました。ただゲームではなく、何か生活に役に立つものを
ロモとできるか考えてみた。
ロモがかなり自由に動けるし、iPhoneだとカメラもついているので、
それを組み合わせすると、ボディーガードではないが、家の状況や
子供、ペットの状況を監視することはできそう！
ロモを遠隔操作し自由に走らせ、ビデオ通信で状況を把握、
写真を撮って、登録した端末にプッシュ通知にて送ることも可能です。

上記の実装は全てmobile backendにて実装ではありません。

# How to? ロモとどうしたか？

まず、構成としては主に三つ部分があります。
 - コントロール: ビデオを受信し、Romo、写真を撮る命令を送る
 - Romoクライアント: ビデオを送信し、Romo制御を受け、写真を撮る
 - プッシュ通知受信クライアント

以下のニフティクラウドの展示会で使った説明図です。
![Romo構成](https://goo.gl/qjb3g6)

* Romoの制御：[ニフティクラウドMQTT](http://cloud.nifty.com/service/mqtt.htm)により実装。

* Romoのビデオ通信：[ニフティクラウド](http://cloud.nifty.com/)でWEB-RTCを構築。

* Romoでの画像写真をアップロード／Push通知を送信: [ニフティクラウドmobile backend](http://mb.cloud.nifty.com/) <- メインがここ！

# Romoで画像をファイルにアップする

```
       //保存するファイル名を生成する
       [self.localView setHidden:false];
       NSDate *currentTime = [NSDate date];
       NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
       [dateFormatter setDateFormat:@"yyyyMMddHHmmss"];
       NSString *resultString = [dateFormatter stringFromDate: currentTime];
       NSString *fileName = [resultString stringByAppendingString:@".jpg"];

       //mbaas初期化する
       [NCMB setApplicationKey:NCMB_ApplicationKey clientKey:NCMB_ClientKey];

       //データーストアに保存し、連携させる
       NCMBObject *imageData = [NCMBObject objectWithClassName:@"image"];
       [imageData setObject:fileName forKey:@"imagetitle"];
       [imageData saveInBackgroundWithBlock:nil];

       // ファイルストアに画像をアップする
       GLKView *tempview = self.localView.subviews[0];
       UIImage *image = [tempview snapshot];
       [self.localView setHidden:true];
       NSData *jpgData = [[NSData alloc] initWithData:UIImagePNGRepresentation(image)] ;
       NCMBFile *file = [NCMBFile fileWithName:fileName data:jpgData];
       [file saveInBackgroundWithBlock:nil];
```

# プッシュ通知の実装

```
       //Sendpush
       NSString *richUrlStr = [@"http://cy8srgt-ac3-app000.c4sa.net/romo-js/#/push/" stringByAppendingString:fileName];
       NCMBPush *push = [NCMBPush push];
       NSDictionary *data = @{};
       [push setData:data];
       [push setMessage:@"it`s a pic from romo"];
       [push setImmediateDeliveryFlag:true];
       [push setPushToAndroid:true];
       NCMBQuery *query = [NCMBInstallation query];
       [query whereKey:@"iot" equalTo:self.pushid]; //installation class setting: string "1"
       [push setRichUrl:richUrlStr];
       [push setSearchCondition:query];
       [push sendPushInBackgroundWithBlock:^(NSError *error) {
           NSLog(@"[Error] %@", error);
       }];
```

#pushが受信する処理

こちらはAndroidもiOSも受信することが可能
Androidの場合は以下のサンプル
* [Android Push](http://mb.cloud.nifty.com/doc/sdkguide/android/push.html)
* [iOS Push](http://mb.cloud.nifty.com/doc/sdkguide/ios/push.html)

# 実装コード公開中

以下のGithubにアップしていますので、ぜひご参考ください。
※サーバー設定、アプリキー設定には使う際に修正が必要。

* [Github romo controller](https://github.com/kuroei/NifRomoController)
* [Github romo client](https://github.com/kuroei/NifRomoClient)

# Reference - 参照

* [Romo](http://www.romotive.jp/)
