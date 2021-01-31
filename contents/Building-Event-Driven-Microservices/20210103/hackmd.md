# Building Event-Driven Microservices Preface, Chap.2

- イベントページ
  - [READING.16 #技術書を英語で読む会](https://reading.connpass.com/event/199543/)
- 課題図書
  - [Building Event-Driven Microservices](https://learning.oreilly.com/library/view/building-event-driven-microservices/9781492057888/)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)

---

### written by @gkzz
- Preface
  - 期待高まる。
    - > culmination of my own personal experiences
      - `culmination` (noun)
        - meaning: the highest or climactic point of something, especially as attained after a long time.
        - Syn: climax, pinnacle, peak, high point, highest point

- Chap.1
  - mediumの変遷が人対人の関係性、社会構造に変化をもたらしたように、`computer system architectures`もまた人対人との関係性に変化をもたらした
    - > each new medium has fundamentally changed people’s relationship with computing
    - > The medium of the asynchronously produced and consumed event has been fundamentally shifted by modern technology
  - > Microservices and microservice-style architectures have existed for many years, in many different forms, under many different names.
    - cf. https://fukabori.fm/episode/29 の「集中と分散の螺旋」
    - Service-oriented architectures
      - be composed of multiple microservices
      - communicate synchronously
    - Message-passing architectures
      - communicate asynchronously
    - **`Event-based communication`**
      - not new
      - `It's new to handling big data sets, at scale and in real time`
      - > these services can be stateful or stateless, complex or simple; and they might be implemented as long-running, standalone applications or executed as a function using Functions-as-a-Service
  - > **`Domain-driven design`**, (略), introduces some of **`the necessary concepts for building event-driven microservices`** 
  - > **`more specialized skill sets can be provided on a cross-team, as-needed basis`**. These best practices are covered in more detail in **`Chapter 14`**
    - Chap.14. Supportive Tooling 
  - event driven microservicesの有用性について
    - Communication Structures in Traditional Computing
      -　> This model encourages many direct point-to-point couplings, which become problematic to maintain as an organization grows 
    - Event-Driven Communication Structures
      - not replacement for request-response communications
      - Chap.3 has details
    - benefits of using event-driven microservices
      - **`granularity/scalability/flexibility on tech and biz requirements/loosely coupling/CD support/high testability`**

  - 単語帳
    - > Each of these inventions 
        - `invention` (noun) <- `invent` (verb)
          - meaning: create or design (something that has not existed before); be the originator of.
          - Syn: originate, create, innovate
    - > These events can now be persisted indefinitely 
      - `persist` (verb)
        - meaning: continue to exist; be prolonged.
        - Syn: continue, hold, carry on
    - > These improvements to the humble and simple event-driven medium have far-reaching impacts
      - `humble`
        - meaning: having or showing a modest or low estimate of one's importance.
        - Syn: meek, deferential, respectful
      - > `far-reaching`
        - meaning: having a wide range or effect  
    - > The internal operations of the context should be intensive and closely related
      - `intensive`
        - meaning: concentrated on a single subject or into a short time; very thorough or vigorous.
        - Syn: thorough, in-depth, concentrated
    - > Bounded contexts should be highly cohesive
      - cf.[Difference Between Cohesion and Coupling](https://stackoverflow.com/questions/3085285/difference-between-cohesion-and-coupling)
        - > Good software design has high cohesion and low coupling. 
        - > Cohesion is the indication of the relationship within a module
        - > Coupling is the indication of the relationships between modules
        - ![](https://i.imgur.com/RYfnrEg.png =300x)
    - > Conversely, aligning microservices on technical requirements is problematic
      - `problematic` (adj)
        - meaning: constituting or presenting a problem. 

    - > laborious to obtain via point-to-point connections
      - `laborious` (adj)
        - meaning: requiring considerable time and effort.
        - Syn: arduous, hard, heavy

  - みなさんからご意見を募りたいこと
    - `Leveraging Domain Models and Bounded Contexts` の **`Leverage`** とは、subdomainを分割しすぎて。 **`ideally a bounded context and a subdomain will be in complete alignment`** ができなくならないように。という意味が込められている？
      - > This division process repeats **`until the subdomain models are granular and actionable and can be translated into small and independent services by the implementing teams. `**`
        - 
    - microservicesはDDDのように望ましい設計条件はある？
      - |DDD/bounded contexts | microservices |
        |---------------------|---------------|
        |be built around business requirements and not technological requirements | aligning microservices on technical requirements is problematic | 
      - どこかの章でヒントがあるかも
        - > These tradeoffs will be examined in greater detail throughout this book
        - 技術軸に立脚、ビジネス軸、ドメインやサブドメインに寄せる
    - `If you find that it is too hard to access data in your organization` で始まるCAUTIONで出てくる **`you’re likely experiencing the effects of poor data communication structures`** とはたとえばどういった構造はpoor？
      - 直前で書かれている、`Databases may provide read-only replicas; however, this can expose their inner data models unnecessarily.` のことを指している
      - ひとつの上方をとるのに、あちこちのサービスから取ってこなくちゃいけないこと。sales, support部門間でやりとりしている例とか


  - 雑多メモ
    - [Confused about Bounded Contexts and SubDomains](https://stackoverflow.com/questions/18625576/confused-about-bounded-contexts-and-subdomains)

- Chap.2
  - producer microservices v.s. consumer microservices 
    |producer                        |consumer                        |
    |--------------------------------|--------------------------------|
    |produce events to event streams |consume from input event streams|
    - the stateless(Chap.5) / the stateful(Chap.7) / the sync- req-res APIs(Chap.13)
  - > Communication between event-driven microservices is completely asynchronous.
  - **`the table-stream duality`**
    - > you can convert a table into a stream of entity events by publishing each update to the event stream
    - > fundamental to the creation of state in an event-driven microservice
  - event brokers v.s. message brokers
    - |event brokers |message brokers |
      |--------------|----------------|
      |retains them for as long as the organization needs |deletes events after acknowledgment

  - **`The microservice tax`**
    - includes the cost of managing, deploying, and operating the event broker, CMS, deployment pipelines, monitoring solutions, and logging services.
    - `paid by the organization or by each microservices`

  - 単語帳
    - > A microservice topology details the inner workings of a single microservice. A business topology, on the other hand, details the relationships between services. 
      - `topology` (noun)
        - meaning: the way in which constituent parts are interrelated or arranged
        - cf. [Difference between network diagram and network topology?](https://superuser.com/questions/832773/difference-between-network-diagram-and-network-topology)
          - > A Network Topology is the actual design of a network. A Network Diagram is a diagram (drawing) of a network.
        - > be often used to mean the processing logic of an individual microservice.
        - > be used to refer to the graph-like relationship between individual microservices, event streams, and request-response APIs.
    - > The microservice topology ingests events from event stream A
      - `ingest` (verb)
        - meaning: jjjjabsorb (information), take in or soak up (energy or a liquid or other substance) by chemical or physical action.
    - > an arbitrary grouping of services
      - `arbitary`
        - meaning: based on random choice `or personal whim`, rather than any reason or system.
        - Syn: capricious, whimsical, random

 - 雑多メモ
   -  [イベントドリブンなマイクロサービスアーキテクチャ](https://yunkt.hatenablog.com/entry/2018/10/14/234311)
   -  [LINEの大規模データパイプラインを支える、Apache Kafkaプラットフォームの運用の裏側](https://logmi.jp/tech/articles/320330)  
---

### written by @fujiwara

- Preface
- Chap.1
    - Bounded context: サブドメインに関連する論理的な境界。
        - Bounded contextとサブドメインが完全に連携している状態が理想だが、レガーシステム/技術負債/サードパーティーとの統合で例外が作られることがよくある。
        - highly cohesive responsibilities であれば、デザインのスコープを減らし、よりシンプルな実装になる
    - Event Streams Provide the Single Source of Truth
        - コミュニケーションの構造は、その情報の信憑性と同じくらい優れているため、組織が信頼できる唯一の情報源としてイベントストリームの説明を採用することが重要。
        - 一部のチームが競合するデータを他の場所に配置することを選択した場合、組織のデータ通信バックボーンとしてのイベントストリームの機能が大幅に低下する。
    - Drawbacks of Synchronous Microservices
        - DISTRIBUTED MONOLITHS: Point-to-point services make it easy to blur the lines between the bounded contexts, as the function calls to remote systems can slot in line-for-line with existing monolith code.
- Chap.2
    - Building Topologies: Microservice Topology/Business Topology
    - Upsert: Upserting means inserting a new row if it doesn’t already exist in the table, or updating it if it does.
    - table-stream duality: stateful table ⇆ entity event stream
    - tombstone: The deletion of a keyed event is handled by producing a tombstone. A tombstone is a keyed event with its value set to null. 
    - マイクロサービスを導入した経緯、戻した理由などが読んでいて理解しやすかった: [Why I've Been Merging Microservices Back Into The Monolith At InVision](https://www.bennadel.com/blog/3944-why-ive-been-merging-microservices-back-into-the-monolith-at-invision.htm)
        - In short, all the benefits of Conway's Law for the organization have become liabilities over time for my "legacy" team. And so, we've been trying to "right size" our domain of responsibility, bringing balance back to Conway's Law. Or, in other words, we're trying to alter our service boundaries to match our team boundary. Which means, merging microservices back into the monolith.
    - Microservice Single Writer Principle
    - Powering Microservices with the Event Broker
        - Event Storage and Serving
        - Event Brokers Versus Message Brokers
        - Paying the Microservice Tax

---

### written by @y-wat

- Preface
- Chap.1
  テクノロジの変化は組織のあり方にも変化を及ぼす、というように見えないの弊社の動きがよろしくないと言えてしまう??
  (システム)イベントは大規模に永続化され、必要に応じて任意のサービスから消費が行われる
    - What are event-drive microservices?
      These events are not destroyed upon consumption as in message-passing systems, but instead remain readily available for other consumers to read as they require. remainさせておく場所はどこだろう
      小さく(だいたい開発期間2週間)、特定用途のために開発される
      stateless or statefulはどちらでもいいらしい
      イベントストリームとマイクロサービスをビジネス組織をまたいだ活動の結合グラフとして形成する ビジネス組織って何だろうな
    - Introduction to domain drive design
      ドメイン: ビジネスの問題空間
      サブドメイン: 特定の責務サブセットに注目し、ビジネスの組織構造を反映する
      ドメインモデル: ドメインの抽象モデル
      境界づけられたコンテキスト: サブドメインに関連した論理的境界。内部は高結合。
      境界づけられたコンテキスト間を疎結合にすることで、ビジネス側の問題の変化に追従しやすくする。
        - leveraging domain
          ドメインをどう切るか悩む
        - aligning bounded context with business requirements
          境界づけられたコンテキストはビジネス要求に合わせて定義するのであって、技術単位ではない
          レイヤードなモノリス実装ではどのチームも単独で実装に責任を持てなくなる
          横断的な技術やチームの依存関係はシステム変更の速度に影響を及ぼす
    - communication structures
      communication structuresは3種類
        - business communication
          会社組織の話
        - implementation communication structures
          組織コミュニケーションの境界と提供機能境界って一致するものかね
        - data communication 
          ビジネスや実装をまたいだデータの流通構造
          サブドメインを跨いだデータアクセスが必要な場合の設計
        - conway's law and communication structures
          データ流通は緩すぎても厳しすぎてもサービス開発を止めてしまう
          domain data is often needed by other bounded contexts within an organization
          わかる
          Data communication structures play a pivotal role in how an organization designs and builds products, but for many organizations this structure has long been missing
          わかる
          Batch processes can dump data to a file store to be read by other processes, but this approach can create issues around data consistency and multiple sources of truth
          それな。embulkとairflowは今すぐ消えてください。
    - communication structures in traditional computing
        - option1: make a new service
        - option2: add it to the existing service
        - pros and cons of each option
          データレプリケーションは結構難易度高いからなぁ
          Scalability, performance, and system availability are often issues for both systems, as the data replication query may place an unsustainable load on the source system.
          わかる
          Copied data will always be somewhat stale by the time the query is complete and the data is transferred.
          わかる
          it’s due to a weak or nonexistent data communication structure.
          これは微妙。自分の担当シス範囲内では、そもそも依頼側が自分でアーキテクチャ要求を定義できないケースが多すぎる。エンジニア側も指摘に動けていない。
        - the team scenraio, continued
        - conflicting pressures
    - event drivem communication structures
      データの作成と所有を分離する
        - events are the bases of communication
          組織内のデータをイベントストリームとして表現する
        - event streams provide the single source of truth
          永続化を意味するのかどうか
        - consumers perform their own modeling and querying
        - data communication is improved across the organization
          データの生成と配信(消費)が分離されるので、データは境界を超えて相互活用できるようになる
        - accessible data supports bussiness communication changes
    - asynchronous event-driven microservices
        - example team using event-driven microservices
    - synchronous microservices
      各マイクロサービスを関数として実装するか、キュー間のタスクとして実装するかの違いだと思っている
        - drawbacks of synchronous microservices
            - point to point couplings
            - dependent scaling
            - service failure handling
            - api versioning and dependency management
            - data access tied to the implementation
            - distributed monoliths
            - testing
        - benegits of synchronous microservices
    - summary
    - 感想
      個別マイクロサービスは表向きinmemory datagridと通信して裏のRDBは外向けIF扱いにするのってできるんですかね(試したことはない)
    
- Chap.2 event driven microservice funcamentals
  orderingはスケールの足かせにならないのか？？
    - building topologies
      businness topology > businness communication structures > microservices
        - microservice topology
        - business topology
    - the contents of an event
      必要な内容であれば何でも良い
      single source of truthの記録
    - the structure of an event
      そう振る??
        - unleyed event
        - entity event
        - keyed event
    - materializing state from entity events
      キーごとに最新イベントを集約するとテーブルになる
      テーブルの更新を常にpublishするとイベントストリームになる
      これなかなか理解してもらえない特にDBA
      These commands can be produced as events to an immutable log, such as a local append-only file (like the binary log in MySQL) or an external event stream.
      rdbの本体はイベントログ
      tombstone: not nullで設計していればね
      Compaction: compaction要否はどこにストアしておくかにも依存するので単純には言えないような。対抗サービスによってもデータの遡り期間は違うので、streamだけで決められないはず。
    - event data definitions and schemas
    - microservice single writer principle
    - powering microservices with the event broker
      event broker: イベントを受け取り、キューまたはストリームに保存する
        - event storage and serving
          キューではなくストリーミングでの設計な雰囲気。しかしこれ全体を満たそうとするとキューでもストリームでも単体では無理じゃないか。
          パーティショニング
          strict ordering: 実質シリアル処理になるので全体のスループットが激しく落ちるはずだが
          inndexing: ストリーム内のindexとconsumerのindex差分で必要なスケールを調整する(インクリメント数字前提か?)
          infinite retention
          replayability
        - additional factors to consider
            - support tooling
              スキーマを公開するスキーマストアでも用意したほうが良いんかね
            - hosted services
            - client libraries and processing frameworks
            - community support
            - long term and tiered storage
              storageがどこで出てくるのか
        - event brokers versus message brokers
          message brokers: pubsub.
          event brokers: 順序付けられたファクトログを提供するためのもの。
          Applications that share consumption from a queue will each receive only a subset of the records
          gcp pubsubはそういう仕様ではない。後続subscriberは各自全量受け取れる。
          Additionally, a message broker deletes events after acknowledgment, whereas an event broker retains them for as long as the organization needs.
          gcp pubsubはそういう仕様ではない。設定でacknowledgeと削除を切り離せる。ただし全量を永続保持する仕様ではないというのはそう。違う仕組みが必要。
          The consumer can pick up and reprocess from anywhere in the log at any time
          これが必須なのか考えたいところ。ordering + consumer任せの配信でどこまでスループット稼げるのか。
        - consuming from the immutable log
            - consuming as an event stream
            - consuming as a queue
              一つのサブスクリプションを複数のインスタンスから見させるのは並列処理させたい場合になるので、それをもって各インスタンスがイベント全量を処理しないとデメリット扱いするのはどうなのか。むしろorderingを強制するevent streamは後続がシリアルになるので処理速度辛くなるように思われるのだが。
        - providing a single source of truth
    - managing microservices at scale
        - putting microservices into connntainers
        - putting microservices into virtual machines
        - managing containers and virtual machines
    - paying the microservice tax
    - summary
    - 感想
      社内全体としてモノリスということは有り得ないので、実態としてマイクロではないが多数のサービスが稼働している状態。と考えると、マイクロサービスを個別サービスで採用せずとも社内全体としてイベントアウトリームを構築するのは必要だと思われる。
      過去イベントを任意のタイミングで任意の地点から再生出来る、というのを要件に上げているが、これストレージ代で破産しませんか。kafkaって3sとかgcsへの外部ストレージオプション有るの
      真面目に対応しようとするとcompactionできなくない？
      brokerってdomain的にどこになるの

---

### written by @chaspy

- Preface
    - >I found that many of the works I read mentioned event-driven architectures either only in passing or with insufficient depth. Some covered only a specific aspect of the architecture and, while helpful, provided only a small piece of the puzzle. Other works proved to be reductive and dismissive, asserting that event-driven systems are really only useful for one system to send an asynchronous message directly to another as a replacement for synchronous request-response systems. 
        - そうじゃないの？と思った
        - 非同期メッセージングを必要とするシーン以外に何がポイントなのかイマイチわからんな
    - >The technologies that support event-driven microservices have a significant impact on how we think about and solve problems, as well as on how our businesses and organizations are structured.
        - ふむふむ
        - how our organizations are structured との関係は気になるね
    - >Event-driven microservices change how a business works, how problems can be solved, and how teams, people, and business units communicate
        - 組織の話がポイントなのかね、確かに気になるが
        - 同期ベースの API でサービス間を繋ぐ場合に比べて、その"インターフェース"にあたるものが何か、あるいはどのように合意するかという点は確かに異なってくるね
- Chap.1
    - Compute resources can be easily acquired and released on-demand, enabling the easy creation and management of microservices
        - コンピューティングと人類の関わり方が変わってきている
    - >Event-based communication is certainly not new, but the need for handling big data sets, at scale and in real time, is new and necessitates a change from the old architectural styles.
        - イベントベース通信は新しいものではないが、ビッグデータセットのリアルタイム処理では新しいアーキテクチャが必要
    - >Compute resources can be easily acquired and released on-demand, enabling the easy creation and management of microservices
        - ここでいう"サービス"はかなり小さそう？
    - DDD の話ふたたび
    - マイクロサービス"ノード"はドメインに紐づくべき
    - でたコンウェイ
    - 3つの構造
        - Business Communication Structures
            - sales, engineering, customer support
        - Implementation Communication Structures
            - communication に関わるものが内包されたモノリスを構成する
        - Data Communication Structures
            - データがあり、それが必要なサービスがそれぞれアクセス、共有データベースパターン？
    - 途中まではマイクロサービスを考える上で一般の話
    - 非同期と同期の比較が出てきてる
- Chap.2
    - Materialize
        - イベントをデータストアのエンティティ？として具現化する、保存するみたいな感じか
    - マイクロサービストポロジとビジネストポロジ
        - >A business topology is the set of microservices, event streams, and APIs that fulfill complex business functions. 
        - ビジネストポロジがサービスの任意のグループ。Businesss Communication Structure であらわされる
    - The Structure of an Event
        - Unkeyed Event
        - Entity Event
        - Keyed Event
    - This is known as the table-stream duality / テーブルストリームの二重性
        - Each entity event is upserted into the key/value table, such that the most recently read event for a given key is represented.
        - you can convert a table into a stream of entity events by publishing each update to the event stream
        - Any consumer client can read an event stream of keyed events and materialize it into its own local state store
    - tombstone: 削除されたことを示すのに v=null いれてるやつ
        - A tombstone is a keyed event with its value set to null.
        - This is a convention that indicates to the consumer that the event with that key should be removed from the materialized data store, as the upstream producer has declared that it is now deleted.
        - なるほど
    - Powering Microservices with the Event Broker
        - This model provides several essential features that are required for running an event-driven ecosystem at scale:
        - Scalability
        - Durability
        - High availabilit
        - High-performance
    - Event Storage and Serving
        - These are the minimal requirements of the underlying storage of the data by the broker:
        - Partitioning
        - Strict ordering
        - Immutability
            - All event data is completely immutable once published. There is no mechanism that can modify event data once it is published. You can alter previous data only by publishing a new event with the updated data.
            - 公開されると、すべてのイベントデータは完全に不変になります。公開されたイベントデータを変更できるメカニズムはありません。以前のデータを変更するには、更新されたデータを使用して新しいイベントを公開する必要があります。
        - Indexing
        - Infinite retention
        - Replayability
    - Event Brokers Versus Message Brokers / イベントブローカーとメッセージブローカーの違いとは
        - Event brokers can be used in place of a message broker, but a message broker cannot fulfill all the functions of an event broker.
        - Event brokers, on the other hand, are designed around providing an ordered log of facts. 
        - Event brokers meet two very specific needs that are not satisfied by the message broker.
            - For one, the message broker provides only queues of messages, where the consumption of the message is handled on a per-queue basis. 
            - Applications that share consumption from a queue will each receive only a subset of the records.
            - This makes it impossible to correctly communicate state via events, since each consumer is unable to obtain a full copy of all events. 
        - Unlike the message broker, the event broker maintains a single ledger of records and manages individual access via indices, so each independent consumer can access all required events. 
            - Additionally, a message broker deletes events after acknowledgment, whereas an event broker retains them for as long as the organization needs. 
            - The deletion of the event after consumption makes a message broker insufficient for providing the indefinitely stored, globally accessible, replayable, single source of truth for all applications.
    - 結構違うんだな
        - Event brokers enable an immutable, append-only log of facts that preserves the state of event ordering.
        - The consumer can pick up and reprocess from anywhere in the log at any time.
        - This pattern is essential for enabling event-driven microservices, but it is not available with message brokers.
    - Event order is not maintained when processing from a queue. 
    - Parallel consumers consume and process events out of order, while a single consumer may fail to process an event, return it to the queue for processing at a later date, and move on to the next event.
    -  だいたい違いわかってきた
    -  Paying the Microservice Tax / マイクロサービス税w
        -  The microservice tax is the sum of costs, including financial, manpower, and opportunity, associated with implementing the tools and components of a microservice architecture. 
        -  This includes the cost of managing, deploying, and operating the event broker, CMS, deployment pipelines, monitoring solutions, and logging services.
        -  These expenses are unavoidable and are paid either centrally by the organization or independently by each team implementing microservices.
        -  The former results in a scalable, simplified, and unified framework for developing microservices, while the latter results in excessive overhead, duplicate solutions, fragmented tooling, and unsustainable growth.

---

### written by @hodagi

- Description
    今日の企業は、増え続けるデータ量とビジネス要件のバランスを取るのに苦労しています。さらに、競争の激しいデジタル業界では、大規模なリアルタイムデータの活用に対する需要が急速に高まっています。従来のシステム・アーキテクチャでは対応できない場合があります。この実用的なガイドでは、イベント駆動型マイクロサービスの原則を使用して、組織内のビジネスユニット全体で大規模データを活用する方法を学びます。

    著者のAdam Bellemare氏は、イベント駆動型マイクロサービスを活用した組織を構築するプロセスを紹介しています。データがどのように生成され、アクセスされ、組織全体に伝播されるかを再考することができます。このデータの価値を引き出すためのパワフルでシンプルなパターンを学びます。イベント駆動型の設計とアーキテクチャの原則を独自のシステムに組み込むことができます。また、ほぼリアルタイムにデータにアクセスできるようにすることで、組織がどのように価値を提供しているかを完全に見直すことができます。

    - 以下のことを学びます。

        - イベント駆動型アーキテクチャを活用して優れたビジネス価値を実現する方法
        - イベント駆動型設計をサポートするマイクロサービスの役割
        - 組織内でのチーム内・チーム間の成功を確実にするための建築パターン
        - 強力なイベント駆動型マイクロサービスを開発するためのアプリケーションパターン
        - マイクロサービスのエコシステムを軌道に乗せるために必要なコンポーネントとツール

www.DeepL.com/Translator（無料版）で翻訳しました。

- Adam Bellemare氏
    - https://www.linkedin.com/in/adambellemare/?originalSubdomain=ca
    - キャリア的にFlippというウォルマートなどのチラシ広告を一覧で見られるアプリのData Platform Engineerとしてずっといたっぽい
        - https://play.google.com/store/apps/details?id=com.wishabi.flipp&hl=ja&gl=US
    - 過去の講演だとこれも同じテーマ(Kafka Summit 2019年の講演)
        - [The Migration to Event-Driven Microservices (Adam Bellemare, Flipp) Kafka Summit NYC 2019](https://www2.slideshare.net/ConfluentInc/the-migration-to-eventdriven-microservices-adam-bellemare-flipp-kafka-summit-nyc-2019)

- Chap.1
    - Kafka周りでよくいわれること
        - State Sourcing/Event Sourcing
    - TIP
        - One of the tenets of event-driven microservices is that core business data should be easy to obtain and usable by any service that requires it. This replaces the ad hoc data communication structure in this scenario with a formalized data communication structure. For the hypothetical team, this data communication structure could eliminate most of the difficulties of obtaining data from other systems.
        - イベント駆動型マイクロサービスのテニュアの1つは、コアとなるビジネスデータは簡単に入手でき、それを必要とするあらゆるサービスで利用できるものでなければならないということです。このシナリオでは、アドホックなデータ通信構造を形式化されたデータ通信構造に置き換えます。仮説的なチームにとって、このデータ通信構造は、他のシステムからデータを取得する際の困難さのほとんどを解消することができます。
    - Synchronous Microservices との比較
        - POINT-TO-POINT COUPLINGS
            - 通信がどのサービスを通っているのかわからなーい
                - distributed tracingとかその文脈で発達したはず
        - DEPENDENT SCALING
            - スケーリングの依存性
        - SERVICE FAILURE HANDLING
            - サービス障害の処理
        - API VERSIONING AND DEPENDENCY MANAGEMENT
            - OpenAPIのDocGeneratorとか
        - DATA ACCESS TIED TO THE IMPLEMENTATION
            - RDBなど構えたときの集中アクセスとか？
        - DISTRIBUTED MONOLITHS(分散モノリス)
        - TESTING
            - テスト
- イベントブローカーとメッセージブローカーの違いとは
---

### written by @takemon

- Preface
背景や謝辞的なことなので省略
- Chap.1
一般的なマイクロサービスのメリットが言語化されてた。マイクローサービス化は技術的な側面だけではく、チーム開発のやり方にも大きく影響を与える点は興味深い。

- Chap.2
実運用されてるイベントストリームのアプリの実装例を知りたいと思った（個人的に複数のイベントストリームがつながったアプリの開発をしたことがないので）。Microservice Taxについても定量的なデータがあるなら知りたい。


### 雑談メモ
- 通知の内容は誰が、どう決める？

- Single source of truth

- 技術的には疎結合だけど
> API versioning and dependency management

- publishで型とは、webのRESTみたいな制約みたいなものですか？
- [Protocol Buffers | wiki](https://ja.wikipedia.org/wiki/Protocol_Buffers)
- https://docs.confluent.io/platform/current/schema-registry/serdes-develop/serdes-protobuf.html

- kafkaなどのイベントソーシングなマイクロサービスにおいて、サービスがイベントに基づきどのように動くのかサービス同士で握らないといけない。そのための仕様公開、例えばイベントにどのようなエンティティを載せるかその公開を誰が管理するのか。

- 作成時期が異なるサービス間でデータを受け渡す、って難しそうだと感じました。新しいサービスは古いサービスの仕様に則っていく足枷がつらそ。

- State Sourcing vs Event Sourcing

- 圧縮したら過去を遡れない
- 圧縮しないとエラい金額になる

- https://www.slideshare.net/techblogyahoo/pulsar-82786963
- https://stackoverflow.com/questions/39586635/why-is-kafka-pull-based-instead-of-push-based

- Kafka preserves the order of messages within a partition.
- https://blog.softwaremill.com/does-kafka-really-guarantee-the-order-of-messages-3ca849fd19d2?gi=1db587548665
- 結局スケールしたいパーティションとorderingするかわりにスケールを捨てたパーティションを分けるのかな？
- https://blog.softwaremill.com/does-kafka-really-guarantee-the-order-of-messages-3ca849fd19d2
- パーティショニングをどこまで切れるかで実質上限ですよねぇ