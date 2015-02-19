title: 東京Node学園 15時限目めも
author: @f_nishio


## io.js - governance

- io.jsはnode.jsの_spork_
    - fork ほど分岐してない、friendly fork
- open governance.
    - nodeの不透明性を問題視
    - 合議制
    - New Committers (Ohta-san from JP)
    - io.jsへのcommit数増加

## io.js - feature

- v8 4.1.0.14 - nodeは3.28くらい?
    - ES6が使える! (ﾟдﾟ)ｳﾏｰ
    - [koa](http://koajs.com/)がそのまま動く
    - const, let
    - --es_staging
    - v8 API (require(v8))
    - util.debuglog
- fs.net.tls込でちょっとnodeより速い？
- Node.js or io.js ?
    - discussion on slack !


## Extensible Web

[Extensible Web Manifesto](https://extensiblewebmanifesto.org/ja/)

- 標準化は時間がかかる
- 標準化→ベンダー→開発者
- 開発者まで降りてきて初めてフィードバック可能、手遅れ
- 開発者がまず実装→いいものなら標準化→ベンダーが実装、としたい
- そのためには low level APIが必要
    - 低レベルAPIを「標準化→ベンダー→開発者」(-"-;)ﾑﾑ･･･


## WebSocket deflate圧縮

- wsモジュール
- permessage-deflate extension実装
- Sec-WebSocket-Extensions:
- bi-directional: 双方向で圧縮
- Context takeover: メッセージ交換を繰り返すほど圧縮効率高まる
- サポート状況
  - chrome ready
  - Firefox v37
  - socket.io v1.4

## CodeOnMobile

github.cm/dai-shi

- mobileでcodingしたい！
- client side: ACE (? 何?)

## 今できる通信高速化

- (javascript & goto)
- lz4 command
    - 巨大なJSONをlz4 + gzip < gzip
    - http上をgzip, JSでlz4展開したら効率よいのでは?
- lz4 on JS
    - JSXで実装 (?)
    - webworker
- 通信量削減可能
    - lz4展開コストを回収できるデータ量なら

## Socket.ioでLife game

build with

- Socket.IO
- HTML5 Canvas
- io.js
