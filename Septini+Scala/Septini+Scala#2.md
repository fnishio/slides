* Septini x Scala 勉強会#２ 〜 DDD設計

** Septeni
− ネット広告業を本業（cyber agentに次ぐ）
− GANMA, PYXIS,
- playframework + scala, AngularJS + TS, Android + Scala, DDD / sisioh?

** Play2 with DDD (Kato-san@Chatwork)
− 業務知識、ユビキタス言語
− シナリオ→ドメインモデル→モデル実装
- DDD layer: application - domain - infrastructure
- 下の層は上の層のモデルを知っていてはいけない、重要！
- repositoryはdomain層、内部実装以降はInfra層に委譲

** Scala x DDD x Septini実践例
− DDDのコンテキストマップをコードに落とせる
− ユビキタス言語→コンテキストマップ→ドメイン図
− ユーザストーリ
-- Product ownerとストーリを確認→コンテキストマップを作成する
-- Product ownerと一緒にドメインをつくりあげる、重要！
- 実装
-- product owner による trait review
-- trait ならコード書けなくてもレビューできる！
- DDD失敗談
-- ドメインを技術で捻じ曲げるのはNG
-- 逆流現象：下の層が上の層を知ってしまうのはNG.プロジェクト分割すると防げる

-- PULL REQは24時間以内にさばく、ルール
