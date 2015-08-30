html5jplat 第8回
====================

2015/08/18(火) html5j Webプラットフォーム部　第8回勉強会 - 白い雲のように【IoT/WoTバージョン】
のメモ

一人でできる！ｍBaaSでスマートホーム化
----------------------------------
by Nakatsugawa-san

- Smart Home
 - home automation ←今日はコッチ
 - energy 最適化
- kick starter の芝生プロジェクトは全部成立！！！→どんだけ需要あるんだヨ
 - 自動給餌、自動給水
- HAにおけるクラウド
 - ステータス記録
 - 指定時間での処理トリガー
 - リモートでの監視
 - しきい値を超えた時の処理
- ニフティクラウド mobile backend
 - MQTT（同時接続数100）
 - WebSocket
 - Timer
 - HTTP
 - fluented
- デモ
 - 機材
   - RaspberryPi2
   - カメラ
   - IRKit HTTP経由で赤外線通信
   - USBマイク
 - Push通知
 - 監視システム
   - Webカム＋motion


IoTデータ分析・可視化（MS Azure）
------------------------------
by Hisamori-san@MS Azure

- RealTime可視化
- IoTではストリームデータの可視化
- MS Azure
  - 日本に2つのREGION
  - Event Hub
  - Stream Analytics
- Azure Event Hubs
 - 数百万イベント/秒
 - HTTPS, AMQP
- Stream Analytics
 - SQL likeなクエリで流れてくるデータを解析
 - Windowing
  - Tumbling 重複なく集計
  - Hopping
  - Sliding Window イベント発生毎に直近ｘ秒
- Power BI Dashboard
 - リアルタイムダッシュボード
 - UIコンポーネント
 - モバイル対応
- デモ
 - センサーデータをリアルタイムに可視化
 - Stream Analyticsは
 EventHubからデータをPULLしている→EventHubは停めずにStreamAnalyticsの設定変えたりできる！


Bluemixで始めるIoT
---------------------
by Fujita-san@IBM

- IoTの世界
 - 開発サイクルのさらなる短縮化
 - よりコンポーザブルな開発
- センサデバイスの接続
- 新しいプロトコルへの対応（MQTT)
- ストリームデータの扱い★
- Recipes
 - IoT Foundation
 - Node-RED
- 本格的なIoTシステム構築事例
 - プジョーConnectedCar
   - 走行データをMQTTで収集
   - リアルタイム分析でドライバに情報提供
   - APIを公開、保険会社等にあらたなビジネス
 - データの蓄積、アナリティクス
   - アナリティクスでインサイトを
 - API公開とエコシステム
 - 水平分業
- BMXUG@Facebook


AWSでできるIoT
------------------
by Enami-san@Amazon

- amazon dash
  - voice recognition
  - button
- amazon echo
 - Voice Interaction
 - カレンダー連携
 - Connected Home
 - ショッピング
 - Alexa Skill Kitで機能追加、AWS Lambdaでプログラミング可
- AWS Lambda
 - ステートレスでリクエスト駆動なコード実行
 - ビジネスロジックにフォーカス
 - スケール、耐障害などはやってくれる
 - Node.js / Java
- Intel EdisonとHello World
 - API Gateway (RESTfull API)
 - Lambda
- AWS for IoT
 - scale
 - low cost, 小さく始められる
 - 収集 S3, Dynamo, Kinesis*
 - 処理 Lambda
 - 分析 Elastic Map Reducer (hadoop)
 - S3
   - Dataを自動複製
   - 耐久性はナインイレブン
 - Kinesis
   - データのストリーミング処理のためのマネージドサービス
   - 低レイテンシー
 - Apache Spark
 - Amazon Redshift
   - データウェアハウス
