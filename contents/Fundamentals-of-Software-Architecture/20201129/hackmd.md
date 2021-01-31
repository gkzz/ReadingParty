# Fundamentals of Software Architecture Chap.9-11

- イベントページ
  - [READING.11 #技術書を英語で読む会](https://reading.connpass.com/event/195945/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)

### written by @gkzz

- Chap.9
  - 今後読んでいく章について
    - Chap.10-12
      - Monolithic: Layered architecture, Pipeline architecture, Microkernel architecture
    - Chap.13-17
      - Distributed: Service-based architecture, Event-driven architecture, Space-based architecture, Service-oriented architecture, Microservices architecture (Chapter 17)
  - `Big Ball of Mud`を[wiki](https://ja.wikipedia.org/wiki/%E5%A4%A7%E3%81%8D%E3%81%AA%E6%B3%A5%E3%81%A0%E3%82%93%E3%81%94)で調べた
    - > 大きな泥だんご (おおきなどろだんご、英: Big ball of mud) は理解可能なアーキテクチャが欠けている ソフトウェアシステム のことを指す。 ソフトウェア工学の視点から望ましくない状態にも関わらず、このようなシステムは事業の圧力、開発者の 刷新 や コードエントロピー などの理由によって当たり前に発生している、アンチパターン の1つである。
    - `the absence of any discernible architecture structure`
      - 識別不可能なアーキテクチャ、構造
        - `discernible` (adj)
          - meaning: able to be discerned; perceptible.
            - e.g.: "the scandal had no discernible effect on his career"
   - `Unitary Architecture`
     - > Generally, software systems tend to grow in functionality over time, `requiring separation of concerns to maintain operational architecture characteristics`, such as performance and scale.
     - `unitary` (adj)
       - meaning: forming a single or uniform entity.
         - e.g.: "a sort of unitary wholeness"
  - `the fallacies of distributed computing`
    - > `A fallacy is something that is believed or assumed to be true but is not`. All eight of the fallacies of distributed computing apply to distributed architectures today. 
      - > 誤認
  - `Stamp coupling`を解決する方法
    - > Create private RESTful API endpoints, Use field selectors in the contract, Use GraphQL to decouple contracts, Use value-driven contracts with consumer-driven contracts (CDCs), Use internal messaging endpoints 
    - cf. [設計におけるオブジェクトの責務分配に有効なものさし -凝集度と結合度-](https://www.ogis-ri.co.jp/otc/hiroba/technical/Cohesion_Coupling/Cohesion_Coupling.html)
      - > 結合度は、望ましいものから順に、以下のように分類されます。
      - > 1.非直接結合, 2.データ結合, `3.スタンプ結合(Stamp coupling)`, 4.制御結合, 5.外部結合, 6.共通結合, 7.内容結合 

- Chap.10
  - > Each layer of the layered architecture style has a specific role and responsibility within the architecture.
    - cf.[[DDD]ドメイン駆動 + オニオンアーキテクチャ概略](https://qiita.com/little_hand_s/items/2040fba15d90b93fc124)
      - `「EricEvansのドメイン駆動」で紹介されたレイヤードアーキテクチャ`
        - > 伝統的レイヤードアーキテクチャから、Domain層のモデルに業務的な知識を持たせ、メンテナンス性を高めようとした。(中略) この設計によってモデリングのしやすいさは大幅に改善されましたが、まだ弱点があります。 Domain層がInfrastructure層に依存していること です。これはつまり、ライブラリの変更やデータベースの切り替えなどのインフラストラクチャレイヤの変更により、ビジネスロジック全体に影響が発生する可能性がある 
      - `オニオンアーキテクチャ`と`依存関係逆転の原則`
        - > ローレベルなレイヤを実装してからハイレベルなレイヤに依存させるのではなく、ハイレベルなレイヤが公開したInterfaceに基づいてローレベルレイヤが実装するのです！これにより、ハイレベルなレイヤの独立性を高めることができます。
  - > The trade-off of this benefit, however, is `a lack of overall agility (the ability to respond quickly to change)`. 
  - `the layered architecture`の評価(☆が多いほど高評価)
    - ![](https://i.imgur.com/Sawnc7F.png =200x)

- Chap.11
  - Pipes
    - Be form the communication channel between filters. 
    - Each pipe is typically unidirectional and point-to-point (rather than broadcast)
  - Filters
    - Be self-contained, independent from other filters, and generally stateless. 
    - Should perform one task only. 
      - Producer, Transformer, Tester, Consumer
    - cf.[データパイプラインに関する知見をカジュアルに語る！ Data Pipeline Casual Talkに参加してきた #DPCT](https://dev.classmethod.jp/articles/report-data-pipeline-casual-talk-vol-1/)
      - > 『最初にかっちり決めて作るのはほぼ不可能』。環境や条件は変わることを前提にして、むしろ『進化させていく』ように作っていくべき。イコール『データ基盤を"育てる"』。
      - > Airflow導入で苦労したこと：バージョンアップが結構面倒、ExecutionDateと実際の実行時刻がずれる、ジョブのスケジュール管理が全て解決した訳ではない
    - cf. [Airflow のアーキテクチャをざっくり理解して、どうやって使うのか学んでみた](https://dev.classmethod.jp/articles/airflow-gs-arch-learn/)
      - > Airflowは、 管理画面表示部の Webserver と、Job実行のスケジュール管理部の Scheduler 、Job実行部の Worker(Executer) 
  - ![](https://i.imgur.com/VnhUYBe.png =300x)
 

### written by y-wat

- Chap.9 Foundations
    - Fundamenal Patterns
        - Big Ball of Mud
        アーキテクチャ的な特徴が明確でない
        ドメイン欠乏症もここか
        コード品質と構造に対するガバナンスの欠如
        - Unitary Architecture
        単一のコンピュータとそこで走るプログラムに閉じたアーキテクチャ
        - Client/Server
        - Desktop + Database Server
        - Browser + Web Server
        - Three-Tier
    - Monolithic Versis Distributed Architectures
    monolithic - layerd, pipline, microkernel
    distributed - service0based, event-driven, space-based, service-oriented, microservices
    以下、distributed computingの誤審(ハマり所)
        - Fallacy #1: The Network is Reliable
        - Fallacy #2: Latency is Zero
        - Fallacy #3: Bandwidth is Infinite
        - Fallacy #4: The Network is Secure
        パフォーマンスにも影響
        - Fallacy #5: The Topology Never Change
        経路の要素は変化するもの
        - Fallacy #6: There is Only One Administrator
        - Fallacy #7: Transport Cost is Zero
        - Fallacy #8: The Network is Homogeneous
        ベンダー間の機器の相性
        - Other Distributed Considerations
            - Distributed Logging
            - Distributed Transactions
            ```high scalability, performance, and availability at the sacrifice of data consistency and data integrity```
            結果整合のリード側設計難しい
            - Contract Maintenance And Versioning
- Chap.10 Layered
```The layered architecture style also falls into several architectural anti-patterns, including the architecture by implication anti-pattern and the accidental architecture anti-pattern.```
    - Topology
    ドメインではなく技術的役割ごとにコードをグループ化する
    - Layers of Isolation
    レイヤーはクローズドまたはオープン
    クローズド: 一層ずつしか降りれない
    オープン: バイパス許容
    layers of isolation: あるレイヤーへの改修が他のレイヤーに影響を出さないようにする
    オープンとかクローズドとかって、結局良心の問題？？
    - Adding Layers
    - Other Considerations
    architecture sinkhole: ただプレゼンテーション層から永続化層まで何もビジネスロジックなしにパラメタを渡し、またプレゼンテーション層までクエリ結果をそのまま戻す。オブジェクト生成でメモリ利用やパフォーマンスに影響が出る。
    - Why Use this Rchitecture Style
    単純、よく知られている
    まだアーキテクチャを決めていないときにとりあえず
    単純で実装コストが低い、というのは初期の話
    - Architecture Charateristics Ratings
- Chap.11 Pipline Architecture Style
低レベル実装でも高級アプリケーションでも用いられる
範囲広いな
コンセプトとしては理解したがアプリケーションでのイメージがつかない
    - Topology
        - Pipes
        - Filters
    - Example
    - Architecture Characteristics Ratings

### written by fujiwara
- 起動失敗。殆ど読めていないので、ほぼ聞く専門になります🙇‍♂️
- Chapter 9
    - Fallacyは考慮漏れしやすい部分なので、メモとして残しておく
- Chapter 10
    - Ratingsもキープ



## 雑談メモ

- [AWS Application Auto Scaling を使用した Amazon Kinesis Data Streams のスケーリング](https://aws.amazon.com/jp/blogs/news/scaling-amazon-kinesis-data-streams-with-aws-application-auto-scaling/)