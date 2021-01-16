# Chapter 5. Event-Driven Processing Basics
- この章ではpull型のみ。

## Composing Stateless Topologies
はい

### Transformations
はい

### Branching and Merging Streams
mergeしたりbranchingしたり。はい。

## Repartitioning Event Streams

### Example: Repartitioning an Event Stream
- data localityとscale upの関係??

## Copartitioning Event Streams
- パーティションを複数streamsで揃えるという話??
  - 複数stream間を横串にするパーティションを用意する、みたいな話か

### Example: Copartitioning an Event Stream

## Assigning Partitions to a Consumer Instance

### Assiging Partitions with the Partition Assignor

### Assigning Copartitioned Partitions
- ```All partitions marked as copartitioned must be assigned to the same single consumer instance.``` :thinkingface:

### Partition Assignment Strategies

### Round-Robin Assignment

### Static Assignment

### Custom Assignment

## Recovering from Stateless Processing Instance Failures

## Summary
- ```Event streams with the same key, the same partitioner algorithm, and the same partition count are said to be copartitioned``` なるほど

## 感想
- わかったようでわからない。実装してないからか。
- partitionにつきconsumer instanceは1台なのか? consumer instance側から見ると??複数っぽいな。
- partitionにアサインする、というのは厳密にはどういう処理なんだろうか


# Chapter 6. Deterministic Stream Processing


## Determinism with Event-Driven Workflows
- 2 states: long runnning and near-real time / catching up to the present time
- event streamは極力deterministicが必要らしい。再走行時も含めて。
  - 自作するとどうなるかな

## Timestamps
- まあtimestampで整列させるしかないですよね
  - timestampとkeyでlinked-listして実データはストレージに入れておくとか??
- offsetは処理済みの判定に使う

### Synchronizig Distributed Timestamps
- ```Event scheduling is the process of selecting the next events to process when consuming from multiple input partitions.``` ふむ

### Processing with Timestamped Events


#### Example: Selecting Order of Events When Processing Multiple Partitions
- instanceにpull結果のストアを作って、pullとprocessingを内部で分離するしか無いんじゃないかな

## Event Scheduling and Deterministic Processing


### Custom Event Schedulers


### Processing Based on Event Time, Processing Time, and Ingestion Time


### Timestamp Extraction by the Consumer


### Request-Response Calls to External Systems


## Watermarks
- spark, beamで分散streamingを行うときの内部的なstate管理手法

### Watermarks inn Parallel Processing


## Stream Time
- kafka streamaで使われる手法
- ```the event-scheduling algorithm to select the next event to process, and then updates the stream time if it is larger than the previous stream time. Stream time will never be decreased.``` ふむ

### Stream Time in Parallel Processing
- ```the Kafka Streams approach sends the repartitioned events back to the event broker using what’s known as an internal event stream``` group by keyとaggregateの間にもstreamを挟む

## Out-of-Order and Late-Arrriving Events
- 非同期でeventは登録されるのに後続はordered必須というのも何か釈然としない

### Late Events with Watermarks and Stream Time


### Causes and Impacts of Out-of-Order Events


#### Sourcing From Out-of-Order Data


#### Multiple Producers to Multiple Partitions


### Time-Sensitive Functions and Windowing
- window処理までevent processingで扱う??

#### Tumbling Windows


#### Sliding Windows


#### Session WIndows


## Handling Late Events


## Reprocessing Versus Processing in near-Real Time


## Intermittent Failures and Late Events


## Producer/Event Broker Connectivity Issues


## Summary and Further Reading


## 感想
- マイクロサービス間を疎結合にするためのデータ配信パイプくらいに思っていたが、なんかそういう話でもなさそうである。ここまでリッチな機能をもたせるなら、キューでは無理。
- マイクロサービス間のイベント伝播というよりsparkとかbeamの内部実装を読んでる気分になってきた。
- この章で出てきたイベントの分割や結合を行うのはイベントソーシングシステム(個別ドメインマイクロサービスとは別物)なのか、個別ドメインマイクロサービスのIF部分なのか??
- 複数streamからのイベントを結合したり分割させる、というのはイベントに対するドメイン知識無しに開発できるのか。個々のマイクロサービスからドメインモデルが漏れているのは許容されることなのか。stream processingに諸マイクロサービスのドメイン知識が集中しているのは、実質密結合と言えたりはしないのか。
- sagaみたいな話との繋がりが見えない気がするのは何故か。