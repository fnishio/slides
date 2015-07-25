# BluemixでIoTしてみた

\#bluemix \#iot \#mqtt

@f_nishio



# Summary

サンプルコードは github: [mqtt-sample](https://github.com/fnishio/mqtt-sample)

# IoT
3つのパターン

- モニタリング
  - センサーからデータを収集、アプリケーションが保管、分析
  - 車両の位置、速度のモニタ
  - 心拍数、生体信号リモートモニタ、医療情報記録・分析
- リモート制御
  - 外からエアコンを起動
- M2M (Mono 2 Mono) 通信
  - 土壌湿度センサー情報から、スプリンクラーを制御

http://www.ibm.com/developerworks/jp/cloud/library/cl-raspberrypi-iot-remote-monitoring-app/index.html



# MQTT
IoTには、センサデバイスからの情報収集や一斉同報通知など安全に通信するためのプロトコルが必要
>MQTT is a machine-to-machine (M2M)/"Internet of Things" connectivity protocol.
It was designed as an extremely lightweight publish/subscribe messaging
transport」（http://mqtt.org/）

MQTT = MQ Telemetry Transport



# IBM Bluemix


## IoTサービス

IoTやってみよう！

- MQTT broker が必要
- IoTアプリケーションをBackendで動かしたい

さて、どうする…

**IBM Bluemixがあるじゃないか！**

- IBM Internet of Thnings Foundation (MQTT Broker)
- Node-REDでお手軽アプリ作成


## Setup

1. [Bluemix](https://console.ng.bluemix.net)にsign in
1. 「カタログ」の「ボイラープレート」から「Node-RED starterコミュニティ」を作成
1. 「カタログ」の「モノのインターネット」から「Internet of Things」を作成



# Sample - モニタリング
こんなものを作ってみる
- Device: 定期的にインクリメントされるカウンター値をpublishする
- App: Deviceからのカウンター値をモニター(subscribe)して、カウンター値が5になったらリセットするようDeviceにコマンドをPublishする

道具立ては
- Device: python + [paho-mqtt](https://pypi.python.org/pypi/paho-mqtt)
- App: Node-RED

http://www.ibm.com/developerworks/jp/cloud/library/cl-mqtt-bluemix-iot-node-red-app/

## Device - 接続機器の登録
IoT Foundationのdashboardを開いて接続する機器を登録する。
登録後に表示される認証用のAuthentication TokenはMQTT Broker接続時の認証パスワードとして使う。
![Device Regist](./images/device_reg.png)

## Device - MQTT Brokerにつなぐ
```python
client_id = "d:{org_id}:{type_id}:{device_id}"
endpoint = "{org_id}.messaging.internetofthings.ibmcloud.com"
client = mqtt.Client(client_id)
client.username_pw_set("use-token-auth", PASSWORD)
client.on_connect = on_connect
client.on_message = on_message
client.connect(endpoint, 1883)
```
``org_id, type_id, device_id, PASSWORD``はIoT Foundationへの登録情報を元に適切に設定する。


## Device - Event Publish
1.5秒ごとに``count``をインクリメントしながらpublishする。
```python
count = 0
while client.loop() == 0:
    msg = json.dumps({ "d" : { "count" : count } });
    client.publish("iot-2/evt/eid/fmt/json", msg, 0, True)
    print("sent: " + msg)
    time.sleep(1.5)
    count = count + 1
```


## Device - Command subscribe
- Brokerに接続したら``iot-2/cmd/cid/fmt/json``トピックをsubscirbe
- ``reset``コマンドが来たら``count``をコマンドに含まれている値に再設定

```python
def on_connect(client, userdata, flags, rc):
    client.subscribe("iot-2/cmd/cid/fmt/json")

def on_message(client, userdata, msg):
    global count
    payload = json.loads(msg.payload.decode())
    if payload['cmd'] == "reset":
        count = payload['count']
```


## Service - Node-RED
サービス側のアプリはNode-REDで手っ取り早く作る。
![flow](./images/monitor_app_flow.png)


## Service - Event subscribe
``MQTT Device``から送信されるトピック``iot-2/evt/eid/fmt/json``のイベントをsubscribeする

![in](./images/monitor_app_in.png)


## Service - Monitor
countイベントをモニターして、countが4を超えたら次のフローへ進む

![switch](./images/monitor_app_switch.png)


## Service - Command payload
resetコマンドを組み立てる

![reset](./images/monitor_app_reset.png)


## Service - Command publish
deviceIdの機器に対して、トピック``iot-2/cmd/cid/fmt/json``にコマンドをpublish

![out](./images/monitor_app_out.png)


## 実行
```
nishio@macbookair:0$ python3 device.py                  (~/project/mqtt-sample)
sent: {"d": {"count": 0}}
sent: {"d": {"count": 1}}
sent: {"d": {"count": 2}}
sent: {"d": {"count": 3}}
sent: {"d": {"count": 4}}
sent: {"d": {"count": 5}}
iot-2/cmd/cid/fmt/json b'{"cmd":"reset", "count": 0}'
sent: {"d": {"count": 0}}
sent: {"d": {"count": 1}}
```



# Sample 2 - リモート制御
(To Be Continued)