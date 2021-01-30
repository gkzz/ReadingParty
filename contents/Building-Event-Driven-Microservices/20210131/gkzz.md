# 「Building Event-Driven Microservices」の7,8章
2021/01/31(Sun) 09:00am-10:30am

## 読書会当日に話したいこと

### Chap.7

- （ Each stateful partitionが）Materialized、実体化されるとは、「何がどうなる」のでしょうか？
  - 以下の2つのmaterializedは別のニュアンス？
  - 後者の`Each stateful partition is materialized twice` とは、 Materialized state  になることか？
  - 冒頭より
    - > `Materialized state`
    - > A projection of events from the source event stream (immutable)

  - やや中盤より
    - > `Using hot replicas`
    - > Figure 7-5 shows a three-instance deployment with an internal state store replication factor of 2. `Each stateful partition is materialized twice`, once as the leader and once as a replica.
    - > ... (略)
    - > Figure 7-5. Stream-table join with three instances and two hot replicas per materialized input partition

---

### Chap.8

- ChoreographyとOrchestrationの違いについて整理したので添削お願いします。
  - |          |Choreography |Orchestration|
    |----------|-------------|-------------|
    |mediator  |なし          |あり         |
    |修正の容易さ|差し込みが難あり||
    |ユースケース|simple(small) workflow||
  - Orchestrationはdirect-call（サービスのAPIを直叩き）アリ、なしの2つがある。
  - なしの場合、event brokerがいる。

- Compensation Workflowsとその一例としてのチケット在庫システムを通じて、sagaの欠点として言われる `Isolation` について少し理解したので添削してほしいです。
  - これまでの読書会でもsagaは出てきましたが、Isolationが欠けているとはなんなのか？分かっていなかったと認識。
  - Isolationとは、ローカル・トランザクションの結果が他サービスに見えていない状態。
    - 例でいう、「割引クーポン付与」（compenstaion workflow）というトランザクションと、チケット在庫管理システムの注文を受けてから在庫確認をするトランザクションは本来は双方の結果を知らない。
    - しかし、「割引クーポン付与」は在庫確認の結果、在庫切れであると分かってから実行されるので、Isolationは崩れているとなる。
    - cf. [理解して拡げる分散システムの基礎知識 - Speaker Deck](https://speakerdeck.com/tzkoba/li-jie-sitekuo-gerufen-san-sisutemufalseji-chu-zhi-shi?slide=20)
    - cf. [マイクロサービスとサービス・メッシュ（Istioが求められる背景） | Think IT（シンクイット）](https://thinkit.co.jp/article/14639)

---

## 読書メモ

### Chap. 7 Stateful Streaming
> how to build, manage, and use state for event-driven microservices.

#### Materialized state/State store
- Materialized state
  - > immutable 
  -  > enable you to use common business entities in your microservice applications
- State store
  - > mmutable  
  - > enable you to store business state and intermediate computations.

- `materialize`
  - verb
  - meaning: become actual fact; happen.
     - e.g.: "the forecast rate of increase did not materialize"
     - Syn: happen, occur, come about take place

#### `where the service will store its data`
> `Internally`, such that the data is stored in the same container as the processor, `allocated in memory or on disk`
> `Externally`, such that the data is stored outside of the processor’s container, in some form of external storage service. `This is often done across a network.`

- `allowcation`
  - noun
  - meaning: the action or process of allocating or sharing out something.
    - e.g.: "more efficient allocation of resources"
    - Syn: allotment, assignment, issuing, issuance, awarding, grant
  
 - `duality`
  - noun
  - meaning: : the quality or state of having two different or opposite parts or elements 

#### `RockDB` について深堀
  - > また、LevelDBのシングルスレッドの圧縮プロセスが特定のサーバワークロードに対して適切に機能しないのに対し、RocksDBはそうしたI/OバウンドワークロードでLevelDBを上回る性能を発揮できるという。
  - > 用途としては、閲覧履歴やユーザーの状態を保存するWebサイトのアプリケーション、スパム検出アプリケーション、グラフ検索クエリ、Hadoopへのリアルタイムクエリが必要なアプリなど、低遅延のデータベースアクセスが必要なアプリケーションを挙げている。Facebookでは現在、各種アプリケーションのペタバイトに近いデータをRocksDBで管理しているという。
 
Source:  [Facebook、Key-Valueストア「RocksDB」をオープンソース化：C++ライブラリとして構築 - ＠IT](https://www.atmarkit.co.jp/ait/articles/1311/25/news096.html)

- `deterministic`
  - adj
  - meaning: relating to the philosophical doctrine that all events, including human action, are ultimately determined by causes regarded as external to the will. 

#### Pros/Cons of Internal State
- Pros: 
  - > Scalability requirements are offloaded from the developer
  - > Physically attached local disk can be quite performant for the majority of modern microservice use cases. 
  - > Flexibility to use network-attached disk
- Cons:
  - > Limited to using runtime-defined disk
  - > Wasted disk space
  - > The new or recovered instance needs to materialize any state defined by its topology before it can begin processing new events. The quickest way to do so is to reload the changelog topic for each stateful store materialized in the application.  

#### Pros/Cons of External State
- Pros: 
  - > Full data locality
- Cons:
  - >  Performance loss due to network latency
  - > Financial cost of external state store services
  - > Full data locality  

#### Disadvantages of Using Internal State | Limited to using runtime-defined disk
> In addition, many compute resource management solutions `allow only for volume size to be increased,` as decreasing a volume’s size means that data would need to be deleted.

cf. [EC2にアタッチしているEBSボリュームのサイズは縮小できますか？ – 株式会社サーバーワークス サポートページ](https://support.serverworks.co.jp/hc/ja/articles/115001410714-EC2%E3%81%AB%E3%82%A2%E3%82%BF%E3%83%83%E3%83%81%E3%81%97%E3%81%A6%E3%81%84%E3%82%8BEBS%E3%83%9C%E3%83%AA%E3%83%A5%E3%83%BC%E3%83%A0%E3%81%AE%E3%82%B5%E3%82%A4%E3%82%BA%E3%81%AF%E7%B8%AE%E5%B0%8F%E3%81%A7%E3%81%8D%E3%81%BE%E3%81%99%E3%81%8B-)


> Apache Kafka has this functionality built into its Streams framework via a simple configuration setting. This setting `provides highly available state stores and enables the microservice to tolerate instance failures with zero downtime.`

- `num.standby.replicas` 深堀
> The number of standby replicas. Standby replicas are shadow copies of local state stores. Kafka Streams attempts to create the specified number of replicas per store and keep them up to date as long as there are enough instances running. Standby replicas are used to minimize the latency of task failover. A task that was previously running on a failed instance is preferred to restart on an instance that has standby replicas so that the local state store restoration process from its changelog can be minimized. Details about how Kafka Streams makes use of the standby replicas to minimize the cost of resuming tasks on failover can be found in the State section.

[Apache Kafka](https://kafka.apache.org/documentation/streams/developer-guide/config-streams.html#num-standby-replicas)

---

### Chap. 8 Building Workflows with Microservices

#### choreographyパターンを使う場合の注意点
- stepを差し込むことワークフローの順番を変えることになりかねず、課題となりがち。
  - > While choreography allows for simple addition of new steps at the end of the workflow, it may be `problematic to insert steps into the middle or to change the order of the workflow.`


#### The choreographed saga pattern 
- suitable for `simple distributed transactions`
- `are unlikely to change over time`


#### 単語帳(順不同)
- `exacerbate`
  - verb
  - meaning: make (a problem, bad situation, or negative feeling) worse.
    - e.g.: "the exorbitant cost of land in urban areas only exacerbated the problem"
    - Syn: aggravate, make worse, worsen, inflame, compound, intensify 

- `brittle`
  - adj
  - meaning: 1. delicate and easily broken: 2. unkind and unpleasant: 3. delicate and easily broken 

- `mitigate`
  - adj
  - meaning: make (something bad) less severe, serious, or painful.
    - Syn: alleviate, reduce, diminish, lessen, weaken, lighten, attenuate

- `discern`
  - verb
  - meaning: recognize or find out.
  -  Syn: perceive, make out, pick out, detect, recognize, notice

- `resilent`
  - adj
  - meaning: (of a person or animal) able to withstand or recover quickly from difficult conditions.
    - e.g.: "babies are generally far more resilient than new parents realize"
    - Syn: strong, tough, hardy

- `meanwhile`
  - adv
  - meaning: in the intervening period of time.
    - e.g.: "meanwhile, I will give you a prescription for some pills"
    - Syn: for now, for the moment, for the present, for the time being
   - meaning: on the other hand.
    - e.g.: "he has said little, meanwhile, about how he plans to live his life" 


- `subordinate`
  - adj
  - maeniang: placed in or occupying a lower class, rank, or position
    - e..g: inferior a subordinate officer. 
- `encapsulation`
  - noun
  - meaning: the action of enclosing something in or as if in a capsule.

---
#### 8章関連の外部記事

- [17. Microservices Architecture - Fundamentals of Software Architecture](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/ch17.html)

  -  choreography
  - > In choreography, each service calls other services as needed, without a central mediator. 
  - [Figure 17-7. Using choreography in microservices to manage coordination](http://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1707.png)

  - orchestration
  - > In Figure 17-8, the developers create a service whose sole responsibility is coordinating the call to get all information for a particular customer. T

  - [Figure 17-8. Using orchestration in microservices](http://fundamentalsofsoftwarearchitecture.com/images/book/fosa_1708.png)

- [マイクロサービスアーキテクチャにおけるオーケストレーションとコレオグラフィ - Qiita](https://qiita.com/kawasima/items/17475a993e03f249a077)

  - > どのサービスを呼び出すかを、アプリケーション側は知らなくてよいので、同じように新規会員登録のイベントを作成しパブリッシュするだけです。


- [伊藤直也氏が語る、サーバーレスアーキテクチャの性質を解剖する（中編）。QCon Tokyo 2016 － Publickey](https://www.publickey1.jp/blog/16/qcon_tokyo_2016_1.html)

  - > 重要なのは、FaaSは自然とコレオグラフィを指向(略)マネージドサービス間を非同期イベントで連携して接続するアーキテクチャなので、これ以外に作りようがない


- https://pages.awscloud.com/rs/112-TZM-766/images/wp_mad_201906.pdf

  - エラー特定のためにログは中央に集約。
  - > AWS Lambda を利⽤してマイクロサービスを実装している場合は、AWS Lambda がサポートする
各開発⾔語で標準出⼒に対してログを送信すると Amazon CloudWatch Logs にログ情報が送られ
る

