# Fundamentals of Software Architecture Chap.17-18

- イベントページ
  - [READING.15 #技術書を英語で読む会](https://reading.connpass.com/event/197478/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)

### written by @gkzz 

- Chap.17
  - Microserviceはいろんなアーキテクチャの考えの影響を受けている
    - > One concept in particular from **`DDD, bounded context`**, decidedly inspired microservices. The concept of bounded context represents **`a decoupling style`**.
    - cf. [どうやってBounded Contextを見つけるか](https://qiita.com/suin/items/49545ba8ca041a41b5d3)
      - > 組織といったコミュニケーション構造に従ってSub Domainを模索することはBounded Contextを設計するための近道
  - to include all necessary parts to operate independently
    - e.g. databases 

  - **`monolithic v.s. microservice`**
    - |monolithic       |microservice                                              |
      |-----------------|----------------------------------------------------------|
      |                 |bounded context(context内ではリソースは共有するけど外ではしない) |
      |coupling         |decoupling                                                |
      |reusable         |non-reusable                                              |
      | > **`some resource becomes constrained on the shared infrastructure`**?? | |
      |reusable         |non-reusable                                              |
      |                 |distributed                                               |
      |                 |> Each service is meant to represent a domain or subdomain|
    
    - > with cloud resources and container technology, teams can reap the benefits of extreme decoupling, both at the domain and operational level.
      - cf. おなじみの ？[29. 技術選定の審美眼(2) w/ twada](https://fukabori.fm/episode/29)
        - > Dockerの登場と、コンテナ技術, 冪等性の難しさ, 巨大化したモノリスによる問題から、マイクロサービスへ
          - 集中と分散の螺旋
          - 一見、コンピューティングリソースは集中と分散を振り子のように行き来しているように見える
          - 実は取り囲む技術背景によって、今の分散(4)と以前の分散(2)とでは差分がある
          - | 集中                                                                         | 分散                                                                             |
            |-----------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
            |1)                                                                           |2) EJB, Service-oriented Architecture, RPCベース, 設定多い, XML職人                              |
            |3) Rails, 規約を守れば設定なくてよい, コーディングゼロ, 生産性高い, 開発は質よりスピード優先 |4) REST, XMLからJSON, スケールアウト, YAML職人, クラウドコンピューティング                           |        
  - `Entity trap`
    - [Fundamentals of Software Architecture Chap.6-8](https://hackmd.io/g-mADNkbSDybO6zlDtlJ1Q)より
      - > - エンティティの罠
      - > アーキテクチャの分割をORM的なエンティティ分割と混同すること 
  - synchronous or asynchronous communication
    - synchronous communication 
      - **`protocol aware heterogeneous interoperability`**
    - asynchronous communication
      - messages
  - **`compensating transaction framework`** はユースケース、懸念事項を調べる
    - [マイクロサービスにおける決済トランザクション管理](https://engineering.mercari.com/blog/entry/2019-06-07-155849/#%E8%A3%9C%E5%84%9F%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B6%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%B3)

  - 疑問点
    - マイクロサービスのひとつひとつのサービスはモノリシック？
      - ”モノリシック”というよりマイクロサービス（複数形）のコンポーネント 


  - 他関連資料
    - [【ZOZOTOWNマイクロサービス化】API Gatewayを自社開発したノウハウ大公開！](https://techblog.zozo.com/entry/zozotown-api-gateway-intro)
      > ストラングラーパターンは、レガシシステムを徐々に新しいシステムに置き換えて移行する方法です。今回ご紹介するAPI Gatewayがストラングラーファサードの役割を担っています。
    - [Monolith to Microservices](https://learning.oreilly.com/library/view/monolith-to-microservices/9781492047834/)
    - [Fallacies of distributed computing](https://en.wikipedia.org/wiki/Fallacies_of_distributed_computing)
      - > The network is reliable
    - [マイクロサービスアーキテクチャとそれを支える技術](https://knowledge.sakura.ad.jp/20167/)
    - [Fundamentals of Software Architecture Chap.12-13](https://hackmd.io/YG5hsfnWT7ao2Cok8OCVSQ?view)
      - [モノリシックからマイクロサービスへ。あるいは、サービスベースアーキテクチャを考える。](https://tech.askul.co.jp/entry/2019/04/09/132952)
      - [One Team At Uber Is Moving From Microservices To Macroservices](http://highscalability.com/blog/2020/4/8/one-team-at-uber-is-moving-from-microservices-to-macroservic.html)

- Chap.18
  - アーキテクチャをデザインする上での考慮点
    - > Monolith versus distributed
    - > Where should data live?
    - > What communication styles between services—synchronous or asynchronous?
  - [Shopifyはいかにしてモジュラモノリスへ移行したか](https://www.infoq.com/jp/news/2019/10/shopify-modular-monolith/)
    - > Westeinde氏は、モノリシックアーキテクチャはプロジェクトの出発点として適当だという考えから、"新しいプロダクトや新たな企業はモノリスから始めることを、実際に推奨していました"、と述べている。

Shopifyはいかにしてモジュラモノリスへ移行したか
https://www.infoq.com/jp/news/2019/10/shopify-modular-monolith/
 

### written by y-wat
- Chap.17 Microservices Architecture
    - History
    言い出したのFowlerなのか。理解。境界づけられたコンテクストがサービス境界になる。DDDの実装パターンくらいに見たほうが良いかもしれん。
    - Topology
    APIレイヤの裏に各サービスが独立して存在する。
    - Distributed
    コンテナにしたからといってリソースが綺麗に分散配置されるかというと、そうでも無いような。その場合はクラスタ等の指定デプロイ先を分けてるはずで、あまりVM分離とも変わらんような。
    単一プロセス内のメソッドコールで完結させるのか、複数プロセス間のプロシージャコールにするのかで分かれるような。
    トランザクション境界をどうするかはシステム粒度の決定に重要である。
    - Bounded Context
    ドメインが個々のサービスを構成する。サービスは自己完結的な実装になる。
        - Granularity
        サービス境界はドメインないしワークフローを捉える。目的、トランザクション、コレオグラフィから適切な境界を発見する。
        - Data Isolation
        共有スキーマやデータベースを結節点とすることは避ける。ORM的にDBでのモデルとアプリのデータ構造を一致させることとも違う。データの分離は頭痛でもあり機会でも有る。
    - API Layer
    mediatorやorchestrationとして利用してはならない。処理は境界づけられたコンテキストの中に閉じ込めること。
    - Operational Reuse
    サイドカーの実装を自力でやったことがないのでイメージがつかない。kube以外でもサイドカーの発想はあるのか？
    kube半年以上さわってないので記憶が・・・
    [Kubernetesで学ぶ分散システムデザインパターン](https://qiita.com/reireias/items/85bcd0acc7f6982041c4)
    サービスメッシュまで行かないとマイクロサービスは完成しない感
    - Frontends
    そういえばこの本ってフロントの話出てこないよな。
    わからん [翻訳記事マイクロフロントエンド](https://micro-frontends-japanese.org/)
    - Communication
    同期化or非同期
    protocol-aware: サービスは互いに相手との通信方法を知っている必要がある(のを隠蔽するのがservice meshと思ってたけど)
    heterogenous: 個々のサービスは別個の技術スタックで実装されうる
    interoperability: サービスを跨ぐトランザクションは避けられるべきだが、個別サービスは互いに呼び出す
    非同期でのブローカーパターンとオーケストレータパターン
        - Choreography and Orchestration
        choreography: 中央不在のブローカーパターン。サービス間の協調が必要な場合はローカルなmediator serviceから制御する。choreographyではサービスの独立性は高まるが、エラー対処や協調管理は難しくなる。
        - Transactions and Sagas
        サービスを跨ぐトランザクションは行わないのが最も良い。
        sagaパターン: 処理が途中で失敗したら補償トランザクションを走らせる。
        mediator使わないパターンが出てこないね
        内容薄いな
        [TCCパターンとSagaパターンでマイクロサービスのトランザクションをまとめてみた](https://qiita.com/nk2/items/d9e9a220190549107282)
    - Architecture Characteristics Ratings
    マイクロサービスってDevOps, TDD, DDD, ロギング, 監視, 耐障害性設計が適切に実装できるチームじゃないとたぶん無理。小さなAPI鯖をばら撒いて収集がつかなくなる。
    通信時間増がレスポンス時間等にどれくらい響いてるか実例無いかな
- Chap.18 Choosing the Appropriate Architecture Style
どのアーキテクチャを採用すべきかは状況依存なので、事前に決め方を提示することは出来ない
    - Shifting "Fashion" in Architecture
    アーキテクチャのスタイルが変わる要因: 過去の観察、エコシステムの変化、新しい可能性(capability)、変化の加速、ドメインの変化、技術の変化、外部要因
    - Decision Criteria
        - 考慮事項
        ドメイン、構造にインパクトを与えるアーキテクチャ的特徴、データアーキテクチャ、組織的要素、知識、ドメイン/アーキテクチャの一致度
        モノリスか分散か
        データをどこで永続化させるか
        同期か非同期か
    - Monolith Case Study: Silicon Sandwiches
        - モジュラモノリス
        - マイクロカーネル
    - Distributed Case Study: Going, Going, Gone

### written by @fujiwara
- Chap.17
    - Granularity: 名前の由来はservice-oriented architectureのgigantic servicesとの対比
        - The term “microservice” is a label, not a description.
    - service planeとservice mesh。service meshってどれくらい本番環境に実装できているんだろう？
- Chap.18
    - データディスカバリーツールとしてこれまでに生み出してきた3世代のアーキテクチャに説明しているLinkedIn社の記事[DataHub: Popular metadata architectures explained](https://engineering.linkedin.com/blog/2020/datahub-popular-metadata-architectures-explained)

### written by @chaspy
- Chap.17
    - 17-1 の図の緑から水色の土管はなんだ
      - ![](https://i.imgur.com/cFIelKy.png =300x) 
    - ちょうど"モノリスからマイクロサービスへ"を読んでるところなので似たような話が出てくるなあ
    - >Because microservices is a distributed architecture, experienced architects advise against the use of transactions across service boundaries, making determining the granularity of services the key to success in this architecture.
    - サイドカーは便利だよなあ、考えたひと天才だわ
    - 図17-6 実はマイクロフロントエンドのうまみわかってない
        - フロントエンドをバックエンドごとに Component 分割するんかな
    - >In microservices, architects and developers struggle with appropriate granularity, which affects both data isolation and communication. Finding the correct communication style helps teams keep services decoupled yet still coordinated in useful ways.
        - ここのコミュニケーションはサービス間のコミュニケーションか
    - >The First Law of Software Architecture suggests that neither of these solutions is perfect—each has trade-offs
        - mediater をもつかどうかにトレードオフがある
    - >Building transactions across service boundaries violates the core decoupling principle of the microservices architecture (and also creates the worst kind of dynamic connascence, connascence of value)
        - なかなか強い言葉を使っているな
        - つまりトランザクションの範囲が1つのサービス粒度になりうるってこったね
        - まぁ言われてみればそれはそう感
    - 分散トランザクションはえぐいよなー
        - データ指向アプリケーションデザイン本であったな
    - >The high points of this architecture are scalability, elasticity, and evolutionary.
    - >Performance is another reason that microservices often use choreography rather than orchestration, as less coupling allows for faster communication and fewer bottlenecks.
        - 結局コレオグラフィーってなんだ
        - https://docs.microsoft.com/ja-jp/azure/architecture/patterns/choreography
        - 中央に mediater を持つのが orchestration パターン
        - そこの中央を非同期にするとか、中央の指揮者を持たないのが choreography パターンかな
            - イベントドリブンって思っとけばええんかな
- Chap.18
    - >Use synchronous by default, asynchronous when necessary.
        - なんでだろ、非同期だからこその難しさがあるからかな
    - Going Going Gone 全然わからん。。。

### written by @someone
- Chap.17
- Chap.18


## 雑談メモ

- [Microservices | martinfowler.com](https://martinfowler.com/articles/microservices.html)