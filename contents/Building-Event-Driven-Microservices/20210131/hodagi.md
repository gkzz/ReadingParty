# Chapter 5. Event-Driven Processing Basics

1. 入力イベントストリームからイベントを消費します。
2. そのイベントを処理します。
3. 必要な出力イベントを生成します。

→ ETLっぽい。あるいはlambda, LINQ式メソッドチェーン

## Repartitioning Event Streams
![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0502.png)

* RDBの正規化にあたるもの？
* パーティションの再編は並列化、スループットに影響する。
  * 参考: https://www.infoq.com/jp/articles/apache-kafka-best-practices-to-optimize-your-deployment/

> パーティション数はトピックレベルの設定値であり、パーティションが多いほど並列化とスループットは向上しますが、
それに伴ってレプリケーションのレイテンシ、再バランス、オープンするサーバファイルの数も増えます。

* そもそもなんでpartition(データ分割)が必要か
  * 参考: https://blog.newrelic.com/engineering/effective-strategies-kafka-topic-partitioning/

>次の場合は、データの属性でパーティションを作成する必要があります。
> * トピックの利用者は、データの属性ごとに集計する必要があります
> * consumerはある種の `Ordering guarantee` (注文保証)を必要としています  
>   - 要するに順番を決めて処理すること
> * もう1つのリソースはボトルネックであり、データをシャーディングする必要があります  
>   - 負荷が高いtopicは集中して高い処理性能を持つサーバーに処理をさせたい
> * ストレージやインデックス作成の効率のためにデータを集中させたい

![](https://blog.newrelic.com/wp-content/uploads/streaming_system.jpg)

要するにいったんイベントを受け付けてから再編成するイメージ。
あ、やっぱりLINQだこれ。

# 余談

なんか気になって、golangにおいて、LINQみたいな書き方ってどうすればいいのか調べてみた。

https://github.com/ahmetb/go-linq

後で検証する

# Chapter 6. Deterministic Stream Processing

* ランポートのパン屋のアルゴリズム..分散システムにおける時計の扱い方を思い出した

参考: [ランポートと時計（分散システムは相対性理論の心を持っている）](https://spacelike.cocolog-nifty.com/blog/2018/11/post-41f8.html)
参考: http://funini.com/kei/logos/clock.shtml

![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0601.png)

## 4つの時間
  - Event time
  - Broker ingestion time(取り込みにかかった時間)
  - Consumer ingestion time
  - Processing time

>For the most accurate depiction events in the real world,
>it is best to use the locally assigned event time provided you can rely on its accuracy. 
>If the producer has unreliable timestamps (and you can’t fix it), your next best bet is to set the timestamps based on when the events are ingested into the event broker. 
>It is only in rare cases where the event broker and the producer cannot communicate that there may be a substantial delay between the true event time and the one assigned by the broker.

## watermark

* 要はtrace id?

# Chapter 7. Stateful Streaming

## Materialized StateとState Storeの違いって？
>Materialized state  
>* A projection of events from the source event stream (immutable)

>State store  
>* Where your service’s business state is stored (mutable)

ピンと来なかったので、ググったら [MaterializedView Pattern](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/materialized-view)と呼ばれる
アーキテクチャデザインに関する説明が見つかった。

>コンテキストと問題
データを保存するときに、開発者とデータ管理者は、多くの場合、データを読み取る方法ではなく、保存する方法を優先します。 選択されるストレージ形式は、通常、データの形式、データ サイズとデータ整合性の管理の要件、使用されているストアの種類と密接に関連しています。 たとえば、NoSQL ドキュメント ストアを使用する場合、データは一連の集計として表されることが多く、それぞれにそのエンティティのすべての情報が含まれています。
ただし、これはクエリに悪影響を及ぼす可能性があります。 クエリで一部のエンティティのデータのサブセットだけが必要な場合 (注文の詳細がまったく含まれていない、複数の顧客の注文の概要など)、必要な情報を取得するために、関連するエンティティのすべてのデータを抽出する必要があります。

>解決策
効率的なクエリをサポートするには、一般的な解決策として、必要な結果セットに適した形式でデータを具体化するビューを事前に生成します。 具体化されたビュー パターンでは、ソース データがクエリに適した形式ではない環境、適切なクエリの生成が難しい環境、またはデータやデータ ストアの性質に起因してクエリのパフォーマンスが低い環境で、データの事前設定されたビューを生成します。
これらの具体化されたビューには、クエリに必要なデータだけが含まれているため、アプリケーションは必要な情報をすばやく取得できます。 テーブルの結合やデータ エンティティの組み合わせに加え、具体化されたビューには、計算列またはデータ項目の現在の値、データ項目の値の組み合わせまたは変換の実行の結果、クエリの一部として指定された値を含めることができます。 具体化されたビューは、1 つのクエリだけを対象に最適化することもできます。
重要なのは、具体化されたビューとそこに含まれるデータは、ソース データ ストアから完全に再構築できるため、完全に破棄可能であるという点です。 具体化されたビューはアプリケーションによって直接更新されることはないので、特殊なキャッシュと言えます。

![](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/_images/materialized-view-pattern-diagram.png)

。。。OracleのMaterialized Viewの経験があるなら、なんで素のテーブルではなくViewを使うのか？で全てわかるはず。
イミュータブルの意味をやっと理解。そういえばそうだけど、Materialized Viewは読み取り専用。あくまで、後からデータを集計するためのクエリに特化した機能なのだ。

このMaterializedView Patternの課題は、ビューのソースであるデータの更新を元にどうやって遅滞なくビューを更新するか？

![](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/_images/event-sourcing-overview.png)

[イベントソーシングパターン](https://docs.microsoft.com/ja-jp/azure/architecture/patterns/event-sourcing)からの引用。
本書で靄っとしていた内容についてだいたい知りたいこと書いてあった。

→上記の内容って、あんまり関係なかった。。

>* stateとして扱うEvent
>  * 送金元、送金先、金額、日付、時刻の詳細が記載された銀行口座振替
>  * 各商品、購入者、日付、時刻、合計金額、支払いプロバイダーの詳細が記載されたeコマース注文
>  * 各イベントに関連付けられているorderId（既存の一意のデータIDを使用する）出荷目的で借方記入された在庫

## オフトピ
* Why we moved from Apache Kafka to Apache Pulsar
  * どうしてApache KafkaからApache Pulsarに移ったのか？ 
  * 参考: https://streamnative.io/en/blog/tech/2020-04-21-from-apache-kafka-to-apache-pulsar

Event-Driven なFWの宿命...全てのイベントを保存しないと、マテリアライズド・ビュー、つまり今の状態を確認できない。
Apache Kafkaは、`tiered storage`機能がなかったので、ストレージにとてもコストがかかっていた。

一方でApache Pulsarは`tiered storage`機能があるので、全てのイベントをセグメントに分解し、inactiveなログのみをS3に送るような調整が可能とのこと。
コストと速度のバランスを取った柔軟なオフロードポリシーを組めるそうだ。

オフトピの後で、Internal StorageとExternal Storageの違いについてこだわっている？点を振り返るとわかるかも。

* Before
![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0708.png)

* After
![](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/assets/bedm_0709.png)

# Chapter 8. Building Workflows with Microservices

* 実装にかんする具体的な紹介記事がないかなと思ったらMicroservice Patternの例をgolangで実装していた人がいらっしゃった。
[Choreography-based saga をローカルで実験するためのフレームワーク](https://enakai00.hatenablog.com/entry/2020/08/03/234301)

* The Choreography Pattern vs The Orchestration Pattern
  * Kubernetesの内実はコンテナオーケストレーションだけど、コレオグラフィパターンに近い。

>gkzzさんのメモ
>sagaの欠点として言われる `Isolation`

IsolationはACID特性の一つ。[トランザクションを複数同時に実行しても、単独実行の場合と同じ処理結果にならなければならない。](https://www.atmarkit.co.jp/ait/articles/1703/01/news194.html)

>このため複数のサーガが並行して実行される際、そのままでは Lost Update6 や Dirty Read 7 といった「異常（anomaly）」が生じうる。これを防ぐ技法が countermeasure で、Semantick Lock、Commutative Updates8、Pessimistic View9、Reread Value10、Version File11、By Value12 といったものがある。Saga パターンでは Semantic Lock を中心に、必要に応じて他の countermeasure を併用する。
>https://qiita.com/yasuabe2613/items/b0c92ab8c45d80318420#countermeasure

The Orchestration Patternは、KafkaをStreamとして扱うパターン。
