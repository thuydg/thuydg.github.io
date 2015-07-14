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

# <STEP2> iBeaconを検出する処理
  - iBeaconのregionを設定する。iBeaconを監視するための領域を設定し、
  - -application:didFinishLaunchingWithOptions メソッドにてUUID, another pair of IDs (major, minor)を設定

```
//AppDelegate
#import <CoreLocation/CoreLocation.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    NSUUID *beaconUUID = [[NSUUID alloc] initWithUUIDString:
                          @"*****-******-******"];

    NSString *regionIdentifier = @"com.nifty.mbaas";
    CLBeaconRegion *beaconRegion = [[CLBeaconRegion alloc]
                                    initWithProximityUUID:beaconUUID identifier:regionIdentifier];

    self.locationManager = [[CLLocationManager alloc] init];
    // New iOS 8 request for Always Authorization, required for iBeacons to work!
    if([self.locationManager respondsToSelector:@selector(requestAlwaysAuthorization)]) {
        [self.locationManager requestAlwaysAuthorization];
    }
    self.locationManager.delegate = self;
    self.locationManager.pausesLocationUpdatesAutomatically = NO;

    [self.locationManager startMonitoringForRegion:beaconRegion];
    [self.locationManager startRangingBeaconsInRegion:beaconRegion];
    [self.locationManager startUpdatingLocation];

    return YES;
}

```

- Setup plist entry for LocationAlways

Supporting FilesフォルダにInfo.plistを開き、Informatio Property ListからAdd a row.

- Define what happens when the region entered

CLLocationManagerのインスタンスのようにAppDelegateを設定する


```
-(void)sendLocalNotificationWithMessage:(NSString*)message {
    UILocalNotification *notification = [[UILocalNotification alloc] init];
    notification.alertBody = message;
    [[UIApplication sharedApplication] scheduleLocalNotification:notification];
}
```

```
-(void)locationManager:(CLLocationManager *)manager didRangeBeacons:
(NSArray *)beacons inRegion:(CLBeaconRegion *)region {
    NSString *message = @"";

        //Send push message
        if(beacons.count > 0) {
            CLBeacon *nearestBeacon = beacons.firstObject;

            if(nearestBeacon.proximity == self.lastProximity ||
               nearestBeacon.proximity == CLProximityUnknown) {
                return;
            }
            self.lastProximity = nearestBeacon.proximity;

            switch(nearestBeacon.proximity) {
                case CLProximityFar:
                    message = @"You are far away from the beacon";
                    break;
                case CLProximityNear:
                    message = @"You are near the beacon";
                    break;
                case CLProximityImmediate:
                    message = @"You are in the immediate proximity of the beacon";
                    break;
                case CLProximityUnknown:
                    return;
            }
        } else {
            message = @"No beacons are nearby";
        }
        NSLog(@"%@", message);
        [self sendLocalNotificationWithMessage:message];
}
```

```
-(void)locationManager:(CLLocationManager *)manager
        didEnterRegion:(CLRegion *)region {
    [manager startRangingBeaconsInRegion:(CLBeaconRegion*)region];
    [self.locationManager startUpdatingLocation];
    NSLog(@"You entered the region.");
    [self sendLocalNotificationWithMessage:@"You entered the region."];
}
```

```
-(void)locationManager:(CLLocationManager *)manager
         didExitRegion:(CLRegion *)region {
    [manager stopRangingBeaconsInRegion:(CLBeaconRegion*)region];
    [self.locationManager stopUpdatingLocation];
    NSLog(@"You exited the region.");
    [self sendLocalNotificationWithMessage:@"You exited the region."];
}
```

# <STEP3> Foreground display

UIではリストを作成し、iBeaconのデーターを入れ、表示
 - Storyboardでリスト作成：TableViewをドラグ＆ドロップ
 - ViewControllerでは

 ```
 @property IBOutlet UITableView *tableView;
 ```

 -  View Controller to implement the protocols required, UITableViewDataSource and UITableViewDelegate.

 ```
 @interface ViewController : UIViewController<UITableViewDataSource, UITableViewDelegate>
 ```
 - beacons変数を作成（ビーコンの管理用変数）

```
@property (strong) NSArray *beacons;
```

  - beaconは検出した時の処理を追加

```
//AppDelegate.m didRangeBeaconsメソッド

ViewController *viewController = (ViewController*) self.window.rootViewController;
   //Beacons info show
   viewController.beacons = beacons;
   [viewController.tableView reloadData];
```

 - viewControllerにある　-tableView:numberOfRowsInSection: and -tableView:cellForRowAtIndexPath: を実装する

```
- (NSInteger) tableView:(UITableView *)tableView
  numberOfRowsInSection:(NSInteger)section {
    return self.beacons.count;
}
```

```
- (UITableViewCell *)tableView:(UITableView *)tableView
         cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    UITableViewCell *cell = [tableView
                             dequeueReusableCellWithIdentifier:@"MyIdentifier"];

    if (cell == nil) {
        cell = [[UITableViewCell alloc]
                initWithStyle:UITableViewCellStyleSubtitle
                reuseIdentifier:@"MyIdentifier"];
        cell.selectionStyle = UITableViewCellSelectionStyleNone;
    }
    //To display beacons list in TableView
    CLBeacon *beacon = (CLBeacon*)[self.beacons
                                   objectAtIndex:indexPath.row];

    //Get shop data from mbaas
    if(self.beacons && self.beacons.count > 0) {
        NSString *uuid = beacon.proximityUUID.UUIDString;
        NCMBQuery *query = [NCMBQuery queryWithClassName:@"Beacon"];
        [query whereKey:@"beacon_uuid" equalTo:uuid];
        NSArray *objects = [query findObjects:nil];
        NCMBObject *object = (NCMBObject*)[objects objectAtIndex:0];
        NSString *storeName = [object objectForKey:@"store_title"];
        cell.textLabel.text = storeName;
        cell.detailTextLabel.text = uuid;
    }
    return cell;
}
```


# <STEP4> Mobile backendサーバーのCoupon情報を取得する

上記のTableViewで表示したbeaconをクリックすると、
mobile backendに保存しているクーポンデーターを表示させる

StoryBoardで新規画面作成、TableView作成：CouponTableViewControler
Segueによる画面遷移実装
CouponTableViewControlerではcouponsという変数を使って、モバイルバックエンドサーバーからのクーポンリストデーターを入れる

```
- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath {
    if (self.beacons && self.beacons.count>0) {
        CLBeacon *beacon = (CLBeacon*)[self.beacons objectAtIndex:indexPath.row]; //Get coupon for first beacon only, need to changed to work with multi ibeacon
        //CONNECT TO SERVER AND GET COUPON
        NSString *beacon_uuid = beacon.proximityUUID.UUIDString;
        NCMBQuery *query = [NCMBQuery queryWithClassName:@"Beacon"];
        [query whereKey:@"beacon_uuid" equalTo:beacon_uuid];
        NSArray *objects = [query findObjects:nil];
        if (objects && objects.count>0) {
            for (NCMBObject *object in objects) {
                self.selectedCoupons = [object objectForKey:@"coupon_list"];
                //ToViewController segue
                [self performSegueWithIdentifier:@"toCouponViewController" sender:self];
            }
        }
    }
}

```

Segue実装

```
// Segue で次の ViewController へ移行するときに選択されたCellの画像情報を渡す
- (void)prepareForSegue:(UIStoryboardSegue *)segue sender:(id)sender{
    // identifier が toViewController であることの確認
    if ([[segue identifier] isEqualToString:@"toCouponViewController"]) {
        CouponTableViewController *vc = (CouponTableViewController*)[segue destinationViewController];
        // 移行先の ViewController にcouponsを渡す
        vc.coupons = self.selectedCoupons;
    }
}
```

CouponTableViewController

```
- (NSInteger) tableView:(UITableView *)couponView
numberOfRowsInSection:(NSInteger)section {
    return self.coupons.count;
}
```

```
- (UITableViewCell *)tableView:(UITableView *)couponView
    cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    UITableViewCell *cell = [couponView
                             dequeueReusableCellWithIdentifier:@"MyIdentifier"];

    if (cell == nil) {
        cell = [[UITableViewCell alloc]
                initWithStyle:UITableViewCellStyleSubtitle
                reuseIdentifier:@"MyIdentifier"];
        cell.selectionStyle = UITableViewCellSelectionStyleNone;
    }

    //To display coupon image
    NSString *coupon_name = (NSString *) [self.coupons objectAtIndex:indexPath.row];
    dispatch_queue_t q_global = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
    dispatch_queue_t q_main = dispatch_get_main_queue();
    cell.imageView.image = nil;

    dispatch_async(q_global, ^{
        NCMBFile *file = [NCMBFile fileWithName:coupon_name data:nil];
        NSData *data = [file getData:nil];
        UIImage *img = [UIImage imageWithData:data];
        dispatch_async(q_main, ^{
            cell.imageView.image = img;
            [cell layoutSubviews];
        });
    });
    return cell;
}
```

# Reference

* [O2Oだけじゃない BLEを使った「Beacon」の可能性](www.itmedia.co.jp/mobile/articles/1406/04/news090.html)
* [iOS app develop with ibeacon](http://ibeaconmodules.us/blogs/news/14279747-tutorial-ibeacon-app-development-with-corelocation-on-apple-ios-7-8)
