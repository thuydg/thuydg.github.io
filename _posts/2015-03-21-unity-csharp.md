---
layout: blog
title: Unity C# 勉強会参加したメモ
category: blog
tags: [unity, csharp]
summary: Android-Unity-bu 勉強会 memo
image: http://origin.arstechnica.com/news.media/scripting-broad.jpg
---

# Time:

  - 2015-3-21 @Nifty Seminar Room
  - Nifty Mobile backend Introduction　[]ニフティクラウドmobile backend紹介](http://mb.cloud.nifty.com/)

# Content 1:

  * LinQ: Language integrated Query: Microsoft .NET の中のモジュール
  * ラムダ形式

# Content 2:

  * UniRx


# Reference

  * [Lambda csharp](http://www.atmarkit.co.jp/fdotnet/rapidmaster/rapidmaster_01/rapidmaster_01.html)
  * [Unity Rx使ってみた](http://qiita.com/RyotaMurohoshi/items/7e1509e03d8e3a1eae4f)
  * Unity5.0 + uGUI + UniRxについてちょっと学んできました
  * Reactive Extensions: Linq: あらゆるものデーターソースとして提供し、イベントを広がる
    イベントを時間軸、シーケンスと見なす。イベントストリームにメッセージが流れてくる。
    Event stream:
      IObservable<T>　簡単に時間軸のイベントを管理するもの
    For .NET: ２００９年から提供開始
    For others: ...Rx libraryがある

  * Reactive extensions for Unity: UniRX
    - 言語が違っても、概念としては基本
    - 資料UnityとuniRX(オススメ)
    http://www.slideshare.net/torisoup/unity-unirx
    http://www.slideshare.net/neuecc/reactive-programming-by-unirxfor-asynchronous-event-processing
    - 詳しい説明サイト：http://reactive.io
    - Sample:
      - Button

```
 public Button searchButton;

 private void Start() {
   this.Input
       .onValueChangeAsObservable() //UniRxのイベントストリームにする
       .Select(x => !string.IsNullOrEmpty(x))
       .SubribeToInteractable...
 }

```

* UnityにおけるMV○○パターン：model view reative Presenter

  - View: scene, hiearachy
    -> Reactive property: 通知可能プロパティ
  - Passive view <-> Presenter(supervising controller) <-> Reactive

# OrangeCubeの方から自社フレームワーク

  - 公開できる：iteratorTask
  - 非同期処理を楽にする、差分更新、変更された部分の変更通知が欲しい
  - Frameworkを作っている：IteratorTaks/ TaskInteraction
  * InteratorsTasks: System.Threading.Tasks class同様、unityには使えない。。。
  スマホゲーム：非同期処理を止めずに実施（サーバーからの処理があること）
    - 今までcallback, .continueWith() を利用すると便利が、.await()

  * IteratorTasks: unityがCoroutine(yeld return)非同期処理Task互換ライブラリを作って使っている。
    Iterator -> task

```
    public async Task RunAsync() {

    }
```

# Page遷移

* Statemachine + task
  - Page遷移はステートマシン
  - state: どのページにる
  - trigger: どのボタンを押すか？タイムアウト？リストをタブかどうか
* Framework:
  - 「戻る」ボタン対応
  - グループ：グループ内遷移
* 定義ファイルから通信コード生成できるようにする
* C# -> C# 定義を行う
