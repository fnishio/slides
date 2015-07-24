# html5jplat 第7回 勉強会
## Webはいつもあなたを見守っている
2015-07-08

@f_nishio




## Introduction
@chikoski (mozilla)


### Web of Things
- IoT -> Web of Things
- Web of Things at W3C
- [http://www.w3.org/WoT/](http://www.w3.org/WoT/)


### Interoperability
  - identity -> url
  - protocol -> http, websocket
  - data -> semantic web
  - representation -> ?
  - data format -> json
  - programming language -> javascript


### WoT
- 第7回: device側
- 第8回: BaaS / mBaaS



## Arduino + Johnny-five
@y_iwanaga_ (Iwanaga-san@IIJ)


### Arduino
- IoT端末を最も簡単で安く作る！-> だったらArduino
- ネットワークついてないけどねw
− PC側のネットワークをつかえばOK


### Johnny-five
Johnny-five：PCからArduinoを操作するモジュール

1. standard famata書き込み
2. node.js + npm install Johnny-five
3. instantiate Board, Sensor
4. MQTT publish -> MQTT subscribe

（MQTT勉強しとこう！）



## Edison + MRAA
@a_nakatsugawa (Nakatsugawa-san@Moongift)


### Edison
IDE: Intel XDK IoT Edition


### MRAA
- developed by Intel
- Edisonだけじゃない。Raspberry PI, Beaglebone Black
- （ラズパイでも使える!）


### Intel Edison Kit for Arduino
- 5Vが使える！
- （これ重要！）


### Little Bits
- Arduino coding Kit
- センサー系が欲しい場合LittleBitsいい！
- （結構高いw）


### mBaas
− mBaaS：Nifty cloud mobile backend
- (mBaaSは次回。次回までに調べておこう！)



## RasPi2 + Win10 + node.js
(Ohta-san@Microsoft)


### Windows 10 IoT Core
Windows 10 IoT Core < IoT for mobile devices < IoT for industry devices


### IoT Core
- UWP対応
- 256MB RAM
- セットアップ簡単になった！
  - Let's say "www.WindowsOnDevices.com" !
  - SDカードイメージ使えばOK


### Universal Windows Apps開発
- VS 2015 RC
  - （Win8でも動くらしい）
- C#, VB, Node.js Python
- MacのひとはVirtual Machineでどうぞ
- VS2015RCで開発
  - テンプレート javascript
  - ADXL345 sample
  - AZURE cloud
  - Stream Analytics
  - http://aka.ms/IoTKitHoL
  - ”IoTあるじゃん”コミュニティ
