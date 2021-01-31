# Fundamentals of Software Architecture Chap.15-16

- イベントページ
  - [READING.14 #技術書を英語で読む会](https://reading.connpass.com/event/197477/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)

### written by @gkzz


- 読書メモではないですが、これは書き残したい。
  - [Google Cloudの主要サービスが10時間ものあいだ障害発生。原因は分散アクセスコントロールへの大量の変更要求が引き起こしたメモリ不足](https://www.publickey1.jp/blog/20/google_cloud10.html)

- Chap.15
  - 前提としてリクエストが各サーバーが受け取る流れを確認し、` space-based architecture`が求められる背景を解説
    - **`a request from a bowser -> the web server -> an application server -> the database server`**
    - 多少のhigh user load(requestが増えると？)であれば、web serverをスケールアウトさせればOK
      - **`それ以上のhigh user loadの場合、ボトルネックは解消されない。`**
      - 後ろに控えるアプリケーションサーバー/データベースサーバーがボトルネックとなる
      - データベースをスケールアウトさせることは難しいので、キャッシュやデータベース製品を使うことになるが、一般的なアプリケーションの負荷対策が難しいことに変わりなし
    - ![](https://i.imgur.com/MDAY4SE.png =250x)
  - > The space-based architecture style is specifically **`designed to address problems involving high scalability, elasticity, and high concurrency issues`** . It is also a useful architecture style for applications that have **`variable and unpredictable concurrent user volumes`**.
    - `address the problems` ≒ solve problems
      - 参考：[address the problems / synonyms](https://www.powerthesaurus.org/address_the_problems/synonyms) 
  - > Space-based architecture gets its name from the concept of **`tuple space`** , the technique of using multiple parallel processors communicating through shared memory. 
    - タプルスペース（tuplespace）とは`概念上の共有メモリ上で型つきのデータレコード（タプル）
    - 参考：[Linda - Wikipedia](https://ja.wikipedia.org/wiki/Linda)
  - ![](https://i.imgur.com/pQ32l8Y.png =300x)
    - **`Processing Unit`**
      - > usually includes web-based components
      - > also contains an in-memory data grid and replication engine like `Hazelcast, Apache Ignite, and Oracle Coherence`
    - **`Virtualized Middleware`**
      - > handles the infrastructure concerns
      - > include a messaging grid, data grid, processing grid, and deployment manager
      - cf. chap.16 
    - **`Messaging Grid`**
      - > determines `which active processing components are available` to receive the request and forwards the request
    - **`Data Grid`**
      - ![](https://i.imgur.com/ghoC1wK.png =300x)
      - > **`asynchronously`** and very quickly, usually completing the data synchronization
      - **`Q.a remote callとは？`**
        - > A processing unit can contain as many replicated caches as needed to complete its work. Alternatively, one processing unit can make **`a remote call`** to another processing unit to ask for data (choreography) or leverage the processing grid (described in the next section) to orchestrate the request.
          - > [RPCとは. Remote Procedure Call](https://www.otsuka-shokai.co.jp/words/rpc.html)
          - cf. [29. 技術選定の審美眼(2) w/ twada 00:35:00](https://fukabori.fm/episode/29)
    - **`Processing Grid`**
      - > `mediates and orchestrates the request` between those two processing units
      - > e.g., an order processing unit and a payment processing unit
    - **`Deployment Manager`**
      - > manages the dynamic startup and shutdown of processing unit instances based on load conditions 
    - **`Data Pumps`**
      - > `sending data to another processor` which then updates data in a database
  - **`Q. Collision RateのUR^2とは？`** 

  - > Table 15-1. Distributed versus replicated caching
    - > Distributed caching for data consistency
    - > Replicated caching for performance and fault tolerance
    - **`Q.どちらか選択するうえで決定打となる比較項目は？`** 
  - **`Examples of space-based architecture`**
    - > caching hybrid model bridging in-memory data grids with a distributed cache. 
    - 実装例：Concert Ticketing System/Online Auction System

  - `concurrent requests`とは、きっちり同時期というより、前のリクエストの処理が終わるまでリクエストがどのくらい届くかぐらい
    - [What does concurrent requests really mean?](https://stackoverflow.com/questions/5017392/what-does-concurrent-requests-really-mean)
      - how many requests arrive during the processing of a request by the application
    - [オンメモリデータベースとは何？ Weblio辞書](https://www.weblio.jp/content/%E3%82%AA%E3%83%B3%E3%83%A1%E3%83%A2%E3%83%AA%E3%83%87%E3%83%BC%E3%82%BF%E3%83%99%E3%83%BC%E3%82%B9)
      - > インメモリデータベースとは、データを全てメインメモリ上に格納する方式で構築されたデータベースのことである。(略) なお、「インメモリ」の代わりに「オンメモリ」の語が用いられる場合もある。
    - [ACID TRANSACTIONS WITH APACHE IGNITE](https://ignite.apache.org/features/acid-transactions.html)
    - [In-Memory Database vs In-Memory Data Grid: Revisited - GridGain Systems](https://www.gridgain.com/resources/blog/in-memory-database-vs-in-memory-data-grid-revisited)  

- Chap.16
  - 消化しきれず。
  - > “Reuse…and Coupling”.
  - > conway's law


### written by y-wat

- Chap.15 Space-Based Architecture Style
    スケールアウトはweb->app->dbの順で容易
    Space-Based Architecture: scalability, elasticity, and high concurrencyに対応
    - General Topology
    中央データベースでなく、インメモリデータグリッドでデータをプロセッシングユニットに複製して管理する
    データベースへの書き込みは非同期に行われる
    processing unit: アプリケーションコード
    virtualized middleware: プロセッシングユニットの管理
    data pumps: データベースに更新を配信する
    data writers: 更新をデータベースに記録する
    data readers: 立ち上がりの時にデータベースからデータを取得する
        - Processing Unit
        アプリケーションロジック(バックエンドロジック) + インメモリデータグリッド
        - Virtualized Middleware
            - MESSAGE GRID
            リクエストとセッション状態管理
            - DATA GRID
            VMの話のはずがprocessing unitの内部っぽい話もあって混乱する
            こいつの役割がよくわからん
            インメモリデータグリッドはどのユニットも同じデータを保つ必要がある
            同期は非同期に100millisec以下で行われる(遅くないか？)
            - PROCESSING GRID
            単一リクエストから複数processing unitを呼ぶ場合の中継
            - DEPLOYMENT MANAGER
        - Data Pumps
        データベースへの更新データをmessagingでpushする
        messingはFIFO(そうか??要らなくないか??)
        - Data Writers
        data pumpからもメッセージをDBに反映する
        - Data Readers
        すべてのプロセッシングユニットがクラッシュした場合、すべてのプロセッシングユニットを再デプロイする場合、複製キャッシュに無いデータを読み出す場合
        あるプロセッシングユニットがオーナーとしてキャッシュのロックを取得し、readerにデータ取得リクエストを送る
        ownerはデータを受け取ったらロックを開放し、キャッシュを同期する
        data writerとdata readerはデータ抽象化レイヤを構成する
    - Data Collisions
    active/active構成での同期レイテンシによるデータ衝突
    衝突の見積もりは計算式が存在する
    同期レイテンシが衝突率に決定的影響を持つ
    - Cloud Version On-Premises Implementations
    - Replicated Versus Distributed Caching
    replicated caching: すべてのプロセッシングユニットが同じキャッシュを保持する。障害耐性もある。100MBを超えると辛くなる(純粋に量的な話??)
    distributed caching: 外部にセントラルキャッシュを持つ。redis?
    - Near-Cache Cosiderations
    中央の外部全量キャッシュと、各プロセッシングユニットでの部分キャッシュを併用する
    保持パターン: most recently user, most grequently user, random replacement
    データ整合性はfront-backキャッシュ間で行い、front間では行わない
    front間で整合性が取れない可能性があるので非推奨
    - Implementation Examples
        - Concert Ticketing System
        - Online Action System
    - Architecture Characteristics Ratings
    シンプルさとテスト容易性は劣る
    プロセッシングユニットはマイクロサービスのドメインサービスとして見立てることも可能
    トランザクション境界で分割しても良い

- Chap.16 Orchestration-Driven Service Oriented Architecture
    - History and Philosophy
    1990年代後半に流行った話
    オープンソースOSはまだ実用的でなくライセンス体系も違い、アプリベンダとDBベンダが対立し、アーキテクトは「再利用」が最優先の考慮事項だった時代
    - Topology
    - Taxonomy
        - Business Services
        コードはなく、in, outとスキーマ情報のみ
        ビジネスユーザが定義するのでビジネスサービス
        - Enterprise Services
        ビジネスドメインごとの共有実装
        が、技術もビジネスも動的なのでうまくいかない
        - Application Services
        一点物の処理
        - Infrastructure Services
        モニタリング、ロギング、認証認可
        - Orchestration Engine
        各サービスの関係性を定義し、ハブになる
        トランザクション制御がorchestration engine依存になるので、トランザクション境界の制御が困難になる
        - Message Flow
        サービス間通信は必ずEBSを通過する
    - Reuse...annd Coupling
    ある共通概念をサービスとして共有化する -> コンポーネント間の結合度が増す&コンポーネント間での差分への対応&技術的分割に注目しすぎ
    - Architeture Characteristics Ratings

### written by fujiwara

- 全然文脈と関係無くこちらが気になっている。オプションだと思ったら、デフォルト設定で強整合性になっていた。なお、公式の日本語は追いついていない。
    - [Amazon S3 data consistency model
](https://docs.aws.amazon.com/AmazonS3/latest/dev/Introduction.html#ConsistencyModel)
    - [[UPDATE] Amazon S3で強い書き込み後の読み込み整合性がサポートされました！ #reinvent
](https://dev.classmethod.jp/articles/update-amazon-s3-strong-read-after-write-consistency/)


### written by @takemon

- ざっくり読んだ。一般的なスケールアウトの構成は実践でも使ったことあるのですぐ理解できたが、Vitualized MiddlewareやIn-memory data gridのあたりの実装経験がないので、イマイチわかっていない。


## 雑談メモ
- golangとscala勉強するとしたらどちらが？
- [ESB（Enterprise Service Bus）（3ページ目） | 日経クロステック（xTECH）](https://xtech.nikkei.com/it/article/REVIEW/20070227/263335/?P=3)
  - 図3●従来のEAIツールにおける処理形態の問題点
    - ![](https://i.imgur.com/nwyRcmN.png =300x) 
  - 図4●ESBにおける分散型の処理形態
    - ![](https://i.imgur.com/ptMleUG.png =300x)
- [Spannerを解説したら講義になった話](https://cloudpack.media/52502)
- cf. [28. 技術選定の審美眼(1) w/ twada](https://fukabori.fm/episode/28)
- cf. [29. 技術選定の審美眼(2) w/ twada](https://fukabori.fm/episode/29)
  - cf. [Worse Is Better - 過去を知り、未来に備える。技術選定の審美眼 2019 edition](https://speakerdeck.com/twada/worse-is-better-understanding-the-spiral-of-technologies-2019-edition) 
- **`人駆動な勉強`**をする場
  - 人から聞いて知らないということを知って勉強するのもいい