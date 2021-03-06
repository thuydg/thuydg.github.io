---
layout: blog
title: For MQTT Client Development
category: blog
tags: [mqtt, iot]
summary: MQTTデーターやりとりするために
image: https://encrypted-tbn2.gstatic.com/images?q=tbn:ANd9GcTG8c5Dt2ZFsgu0dQzdSiRCI8IU2qeYsyZRm0q8n-inRMEqQH4t
---

# What is MQTT?

> MQTT stands for MQ Telemetry Transport. It is a publish/subscribe, extremely simple and lightweight messaging protocol, designed for constrained devices and low-bandwidth, high-latency or unreliable networks. The design principles are to minimise network bandwidth and device resource requirements whilst also attempting to ensure reliability and some degree of assurance of delivery. These principles also turn out to make the protocol ideal of the emerging “machine-to-machine” (M2M) or “Internet of Things” world of connected devices, and for mobile applications where bandwidth and battery power are at a premium.

(src:link below)

![IoT向け通信プロトコルの理解](http://codezine.jp/static/images/article/8000/8000_02_s.gif)

# How to create a MQTT server?

> MQTT As a Service: sangoをリリースしました
2014年8月に、GitHubアカウントで簡単に登録できてMQTTを使い始められるsangoを時雨堂がリリースしました。



# How to create a MQTT client?

よく参照されているもの:

* Mosquitto
* RabbitMQ - RabbitMQ MQTT Adapter
* Paho - Open Source messaging for M2M
* ActiveMQ Apollo

MosquittoはCで書かれた古くからある実装で、ほぼすべての機能を実装しており、参照実装として扱われることが多いです。
RabbitMQはerlang製の定評あるMQサーバーです。AMQPなどにも対応していますが、MQTTにも対応しています。
Pahoは前述の通りIBMから寄贈された実装で、Java版やPython、JSなど、多彩な言語に対応しています。
ActiveMQ ApolloはMQTTTの他STOMPやAMQPなどもできます。
また、クローズドソースですが、HiveMQというものもあります。

* 作ろうとしているのはiOSクライアントなので、以下のように検討：
** MQTTKit: https://github.com/jmesnil/MQTTKit
*** Example: https://github.com/jmesnil/MQTTExample

## POD INSTALL

     $sudo gem install cocoapods
     $pod install

### Memo:
Got this error:
```
$ pod install
Analyzing dependencies
/Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/user_interface/error_report.rb:103: warning: Insecure world writable dir /usr in PATH, mode 040777
/System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/2.0.0/pathname.rb:422:in `open': No such file or directory - /Users/username***/.cocoapods/repos (Errno::ENOENT)
  from /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/2.0.0/pathname.rb:422:in `foreach'
  from /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/2.0.0/pathname.rb:422:in `children'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/sources_manager.rb:63:in `all'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/user_interface/error_report.rb:130:in `repo_information'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/user_interface/error_report.rb:34:in `report'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/command.rb:58:in `report_error'
  from /Library/Ruby/Gems/2.0.0/gems/claide-0.7.0/lib/claide/command.rb:300:in `handle_exception'
  from /Library/Ruby/Gems/2.0.0/gems/claide-0.7.0/lib/claide/command.rb:274:in `rescue in run'
  from /Library/Ruby/Gems/2.0.0/gems/claide-0.7.0/lib/claide/command.rb:264:in `run'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/lib/cocoapods/command.rb:45:in `run'
  from /Library/Ruby/Gems/2.0.0/gems/cocoapods-0.35.0/bin/pod:43:in `<top (required)>'

```
Solution:

```
pod setup
pod install
```

# Reference

* [MQTTサイト](http://mqtt.org/faq)
* [IoT時代を支えるプロトコル「MQTT」](http://codezine.jp/article/detail/8000)
* [MQTTまとめ](http://tdoc.info/blog/2014/01/27/mqtt.html)
