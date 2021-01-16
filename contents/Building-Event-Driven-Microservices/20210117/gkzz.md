# 「Building Event-Driven Microservices」の5,6章
2021/01/17(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chap.5
- TransformationsのMapとMapValueについて。Mapを使うときはMapValueでは要件を満たせないときのみ？ValueだけではなくKeyを変えたくなるときってたとえばどういうとき？
  - > Note that if you change the key, you may need to repartition to ensure data locality.

- `data locality`について深堀した
  - そもそも`data locality`とは
    - > ローカリティ（locality）パフォーマンス最適化の一種で、頻繁に同時に必要になる複数のデータ片を同じ場所に置くこと。
     Source: [データ指向アプリケーションデザイン ―信頼性、拡張性、保守性の高い分散システム設計の原理](https://learning.oreilly.com/library/view/untitled/9784873118703/)
  - jsonやNoSQLはlocalityの考えが使われている
    - > JSONの表現であれば、すべての関連情報は1カ所に集まっているので、一度のクエリだけで十分
    - > リレーショナルの例でプロフィールをフェッチしようとすれば、複数のクエリを実行する

### Chap.6
- 本でベストエフォートって書かれているの、初めてみたかもしれない。そんなことない？
  - > The overarching goal of `deterministic processing` is that a microservice should produce the same output whether it is processing in real time or catching up to the present time.
  - 同じにすることは難しいと思っていたのでベストエフォートというスタンスそのものは同意。

- 本書で出てくるウォーターマークとは
  - 著作権保護の文脈で使われるものとはまた違うものとは思っている。
    - [ウォーターマーク | wiki](https://ja.wikipedia.org/wiki/%E3%82%A6%E3%82%A9%E3%83%BC%E3%82%BF%E3%83%BC%E3%83%9E%E3%83%BC%E3%82%AF)
  - 本書ではwatermarkについてこのように。
    - > Watermarking is used to track the progress of event time through a processing topology and to declare that all data of a given event time (or earlier) has been processed. This is a common technique used by many of the leading stream-processing frameworks, such as Apache Spark, Apache Flink, Apache Samza, and Apache Beam. 
  - ↓にちかいニュアンスかなと。
    > Apache Beam が追跡するウォーターマークは、特定のウィンドウのすべてのデータがパイプラインに届くときを予測するためのシステムの概念です。

    Source: [Apache Beamのプログラミング モデル](https://cloud.google.com/dataflow/docs/concepts/beam-programming-model?hl=ja)
 - 本書で挙げられていた参考資料：[A whitepaper from Google ](https://static.googleusercontent.com/media/research.google.com/en//pubs/archive/43864.pdf) 


- `fundamental issues in stream processing`という観点での落とし所
  - > you can never be sure that you have received all of the events.
  - > how much state to store

---

## 読書メモ

### Chap.5
#### Basic idea
- Event-driven microservices' process
  - create a producer client and a consumer client
  - register itself with any necessary consumer groups
  - starts a loop to poll the consumer client for new events, processing them as they come in and emitting any required output events. 

- `traverse`
  - verb
  - meaning: move back and forth or sideways. 

#### Common transformations
- Filter
  - > emits zero/one 
- Map
  - > Changes the key and/or value of the event, emitting exactly one event. 
  - > if you change the key, **`you may need to repartition to ensure data locality. `**
- MapValue
  - > Change **`only the value of the event, not the key. `** 
  - > **`Repartitioning will not be required.`** 
- Custom transforms
  - > Apply custom logic, look up state, and even communicate with other systems synchronously.


#### Necessities to branch event streams or to merge streams
- to branch event streams
  - to output it to **`a new stream based on the result`**
  - streamが増える

- to merge streams
  - to output to a single output stream
  - from multiple input streams are consumed
  -   streamが減る、以前あったものを結合する

See the details in Chap. 6
> how to handle consuming and processing events from multiple input streams in a consistent and reproducible order.

#### Repartitioning
- the act of producing a new event stream with one or more of the following properties:
  > - Different partition count
  > - Different event key
  > - Different event partitioner

- `delegate`
  - verb
  - meaning: entrust (a task or responsibility) to another person, typically one who is less senior than oneself. 
    - Syn: assign, entrust, give, pass on 

- `colocate`
  - verb
  - meaning: place side by side or in a particular relation.

### Chap.6

- `fault`
  - noun
  - meaning: .responsibility for an accident or misfortune.

- `watermark`
  - noun
  - meaning: A watermark is an identifying image or pattern in paper that appears as various shades of lightness/darkness when viewed by transmitted light (or when viewed by reflected light, atop a dark background), caused by thickness or density variations in the paper. 

- `concise`
  - adj
  - meaning: giving a lot of information clearly and in a few words; brief but comprehensive.
  - Syn: succinct, short, brief 


### Two processing states
|   | typical of long-running microservices  | common for underscaled and new services                   |
|--------|---------------------------------------------------|----------------------------------------------------------------------------|
| state | at near–real time                                  | from the past in an effort to catch up to the present time |


### best-effort determinism
- consistent timestamps
- well-selected event keys
- partition assignment
- event scheduling
- strategies to handle late-arriving events.

- `reconcile`
  - verb
  -  meaning: restore friendly relations between.

- Event time
   - > assigned to the even by the producer at the time the event occurred.
- Broker ingestion time
  - > assigned to the even by the event broker.

- Consumer ingestion time
  - > ingested by the consumer

- Processing time
  - > processed by the consumer

> 分散システムでは「どちらのイベントが先に発生したか」を断定するのが不可能なことがある

Source: [『Time, Clocks, and the Ordering of Events in a Distributed System』の要約](https://gist.github.com/sile/5f4c04d15b8ff25e70c9d3c18670397b)

#### stream times, Kafka Streams
- 並列処理に使える
  -> Figure 6-4. Watermark propagation between nodes in a single topology with multiple processors
  - cf. [[Apache Kafka] Kafka StreamsでStream処理をしてみる [node.js]](https://dev.classmethod.jp/articles/kafka-streams/)

#### Out-of-Order and Late-Arriving Events
- Microserviceごとに「遅れているとみなす基準が違う」
-> One microservice may consider any out-of-order events as late, whereas another may be fairly tolerant and require many hours of wall-clock or event time to pass before considering an event to be late

- 原因
  - out-of-order data
    - >  when data is consumed from a stream that is already out of order or when events are being sourced from an external system with existing out-of-order timestamps.
　 - > Multiple producers writing to multiple output partitions 
     - e.g. Repartitioning 

#### Windowing
- grouping events together by time. 
- particularly useful for events with the same key, where you want to see what happened with events of that key in that period of time. 


|Tumbling|Sliding|Session|
|------------|---------|-----------|
|a fixed size|a fixed window size and incremental step|not-fized|with a session gap due to inactivity|
