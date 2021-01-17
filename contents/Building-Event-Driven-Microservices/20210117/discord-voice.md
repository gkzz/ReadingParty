- > TransformationsのMapとMapValueについて。Mapを使うときはMapValueでは要件を満たせないときのみ？ValueだけではなくKeyを変えたくなるときってたとえばどういうとき？
  - 「hadoop, map/reduce」についてググること
  - 単価、価格から合計

- [Map Reduce 〜入門編：仕組みの理解とアルゴリズムデザイン〜](https://www.slideshare.net/doryokujin/map-reduce-8349406)
  - 18/78枚目からmap -> shuffle -> reduce

- [MapReduce - Wikipedia](https://en.wikipedia.org/wiki/MapReduce)
  - > Another way to look at MapReduce is as a 5-step parallel and distributed computation:
  - > Prepare the Map() input – the "MapReduce system" designates Map processors, assigns the input key K1 that each processor would work on, and provides that processor with all the input data associated with that key.
  - > Run the user-provided Map() code – Map() is run exactly once for each K1 key, generating output organized by key K2.
  - > "Shuffle" the Map output to the Reduce processors – the MapReduce system designates Reduce processors, assigns the K2 key each processor should work on, and provides that processor with all the Map-generated data associated with that key.
Run the user-provided Reduce() code – Reduce() is run exactly once for each K2 key produced by the Map step.
  - > Produce the final output – the MapReduce system collects all the Reduce output, and sorts it by K2 to produce the final outcome.

- [vitessio/vitess: Vitess is a database clustering system for horizontal scaling of MySQL.](https://github.com/vitessio/vitess)

- [Scaling Datastores at Slack with Vitess - Slack Engineering](https://slack.engineering/scaling-datastores-at-slack-with-vitess/)

- kafkaが抱える責務、おもすぎないか。
- マイクロサービスのメリットは粗結合だと思っていただけに。
- データを待ち受けるものならいいけど。
- どうとってくかは後続のサービス次第であればいいけどkafkaもやるの？
- sagaはchap8にありますね。
  - > Distributed transactions in an event-driven world are often known as sagas and can be implemented through either a choreographed pattern or an orchestrator pattern. The saga pattern requires that the participating microservices be able to process reversal actions to revert their portion of the transaction.
  - > Figure 8-7. Simple orchestrated transaction topology
- pub/sub、bufferingに徹していればよい
- stream処理までやらせるからめんどう、ステップ管理-> shuffle必要
- フラグをトピックごとにもつのか。
- サブスクライバーが個別にフラグを持てばよくないか

- [ストリーム処理を１からKappa Architectreまで学ぶ | PLAID engineer blog](https://tech.plaid.co.jp/realtime_stream_system/)
  - > Log-structured data flow：ログを１つに集約する

- [ログのエクスポートの概要  |  Cloud Logging  |  Google Cloud](https://cloud.google.com/logging/docs/export)

- 余談: ギリシャ語のアルファベット(Ελληνικό αλφάβητο)ごとにアーキテクチャーがありそう。
  - Αα    アルファ
  - Ββ    ベータ
  - Γγ    ガンマ
  - Δδ    デルタ
  - Εε    エプシロン
  - Ζζ    ゼータ　https://www.oreilly.com/content/zeta-architecture-hexagon-is-the-new-circle/#:~:text=The%20Zeta%20Architecture%20is%20an,integrating%20data%20into%20the%20business.
  - Ηη    イータ　
  - Θθ    シータ　https://www.essi.upc.edu/dtim/bignovelti/documents/BigNovelTI-Paper3-theta-architecture.pdf
  - Ιι    イオタ
  - Κκ    カッパ
  - Λλ    ラムダ

- [さくらインターネット、高負荷に耐えるNTPサーバー「FPGA ベース・ハードウェアNTPサーバ（Stratum1）」を開発](https://ascii.jp/elem/000/004/006/4006304/)
  - > 高負荷に耐える専用デジタル回路を設計開発し、NTPサーバーとして働く「FPGA ベース・ハードウェアNTPサーバ（Stratum1）」を開発した

- [7. CI/CDとか、CircleCI自体の設計・開発プロセスとか](https://fukabori.fm/episode/7)
  - > 全世界に分散した開発
  - > CTOが乱入するお客様対応

- kafkaはutcをみている？
  - >「2038年問題」への対応進むLinux

- id, timestampなど特定のデータを後続の処理が使う場合、特定のデータの加工が終わらないと詰まる？？
  - https://zenn.dev/gkz/scraps/fe827186c5d8bc#comment-5d8009d756861e
  - timestampが狂っていないことが重要。これはOSの責務。
  - kafkaが新しいidを作るということはドメイン知識いるよね？
  - timestampはライブラリ使えばよし。utc/jstやらは見せ方の問題。idは多少生成面倒

- 海外のエンジニアと仕事することについてお話したので補足資料
  - [【受付終了】berlin.tech.meetup #1 ベルリンでエンジニアとして働く](https://connpass.com/event/157899/)
  - [ベルリンでエンジニアとしてはたらく](https://drive.google.com/file/d/1807ZO9uobNCZfliyuL0hbzNMbtJVv1LX/view)
  - [sli.do](https://app.sli.do/event/khbkvsqc/live/questions)

