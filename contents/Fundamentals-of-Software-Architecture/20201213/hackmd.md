# Fundamentals of Software Architecture Chap.14

- イベントページ
  - [READING.13 #技術書を英語で読む会](https://reading.connpass.com/event/197476/)
- 課題図書
  - [Fundamentals of Software Architecture: An Engineering Approach](https://learning.oreilly.com/library/view/fundamentals-of-software/9781492043447/)
- 貼っている画像の引用先
  - [Updated Fundamentals of Software Architecture Images](http://fundamentalsofsoftwarearchitecture.com/images.html)
- これまでのイベントで扱ったHackMDのリンク集
  - [技術書を英語で読む会の雑談メモリンク集](https://hackmd.io/@gkzz/H1fdY9jOP)

### written by @gkzz

- Chap.14
  - `inventory` (noun)
    - meaninig: a complete list of items such as property, goods in stock, or the contents of a building.
      - Syn: list, listing, catalogue, directory, record, register, checklist
  - Pros of Broker
    - ![](https://i.imgur.com/R4KsdLD.png =400x)
      - 出所:[Architectural Patterns For IoT — Event Driven Architectures by prashun javeri](https://link.medium.com/9bqmn54A9bb)
    - **`Highly decoupled event processors`**
    - High scalability
    - High responsiveness
    - High performance
    - High fault tolerance 
  - Pros of Mediator
    - ![](https://i.imgur.com/hS8p6yU.png =400x)
      - 出所:[同上](https://link.medium.com/9bqmn54A9bb) 
    - Workflow control
    - **`Error handling`**
    - Recoverability
    - Restart capabilities
    - Better data consistency
  - 感想： **`疎結合な設計としたい場合Brokerを、エラーハンドリングを優先したい場合Mediatorを`**
  - Q.AWSのSQS/Step FunctionsがBroker/Mediatorの機能を取り込んでいる？どう組み込むかは考えなくてよい？
    - そんなことはない。AWSのサービスを使っても考える必要はある。
　- cf.![](https://i.imgur.com/WImxNbQ.png)
      - 出所：[AWS Black Belt Online Seminar](https://d1.awsstatic.com/webinars/jp/pdf/services/20200610_AWS_BlackBelt_Building_Event_driven_Architectures_on_AWS.pdf) 
 

### written by @fujiwara

- Chap.14 Event-Driven Architecture Style
    - イベントを非同期で受け取り、処理する疎結合のイベント処理コンポーネントで構成されたアーキテクチャ。
    - request-based model: request orchestrator向けにシステムにあるアクションのまとまりを実行するようにリクエストを送る。 request orchestratorはユーザーインターフェースが典型的なパターン。APIレイヤーや、エンプラのサーバーバスでの実装パターンもある。
    - request orchestrator→様々なrequest processorsに対して決定的かつ同期的にリクエストを向ける。
    - Topology: 
        - mediator
        - broker
    - request-reply messaging (sometimes referred to as pseudosynchronous communications)
        - correlation ID
        - temporary queue
    - [Scalable serverless event-driven architectures with SNS, SQS & Lambda](https://virtual.awsevents.com/esearch/search?keyword=%22scalable%20serverless%20event-driven%22)
        - 見てみましたがKinesisはノータッチ。FIFO/Exactly Onceの設定ポイント、エラーハンドリングはAWSの設定をする、という観点で参考になりました。


### written by y-wat

- Chap.14
イベントを非同期に受信し処理する、分断されたイベント処理コンポーネントによって構成される
    - Topology
        - mediator topology
        ワークフローを管理したい場合
        - broker topology
        レスポンス性とイベント処理の動的管理を行いたい場合
        そうか・・・？？
    - Broker Topology
    中央のイベント中継サービスは無く、イベントは個別のイベントプロセッサに散っている
    4つの主要なコンポーネント: initiating event, event broker, event processor, processing event
    initiating event: イベントフローの起点。event brokerに配信する。
    event broker: たぶんチャンネルの集合
    event processor: event brokerからeventを受け取り処理を行う
    processing event: event processorが処理した内容を次のチャンネルに配信する
    fire and forget: publish-and-subscribe
    拡張性を考慮すると後続処理が無くても処理結果を配信すべき: そうか??何を配信すべきかは宛先のキューによって違うはずなので載せるメッセージ内容が変わるような気がする。キューを処理の後ろ側で紐付ける設計なのか?
    エベントを流すというよりオブジェクト自体を流すイメージなんだろうか(fig.14-4)
    個別event processorは独立してスケール可能だがtopicにはback pressureが必要
    negative: 全体的なワークフローが無い、エラー処理にシステムとして気づく方法がない、リカバリ性が提供されない
    ここは製品やサービスに依存すると思うけどなぁ
    - Mediator Topology
    event mediator: ワークフローを管理制御する
    event processors: イベントの処理済み通知をmediatorに戻す
    結局mediatorってビジネスロジックや処理順序制御みたいな機能を持って無いように見えて、だったら要らないんじゃないかと思ってしまう。event processors間の疎結合度合いを上げたいみたいな話のほうが筋が通るような。
    broker topologyでもエラー対処とかリカバリは出来るけどなぁ。なんで出来ない体裁で話を進めてるんだろうか。
    negative: declaratively modelは複雑なフローでは表現が難しい、mediatorのスケール性能(いうほど辛いか??)、event processorsがbroker topologyほど分離できない(そうか??)
    sagaとかtccの話が出てこないのwhy これ一番気になったかな [TCCパターンとSagaパターン](https://qiita.com/nk2/items/d9e9a220190549107282)
    そういえばこの章ってトランザクションの話が出てこないな。
    - Asynchronous Capabilities
    - Error Handling
    エラーデータの自動修復?やっていいのか?正常なデータのパターンは登録できるが、それと違ったデータを検知したところで違いが発生した理由や原因を追わないと直し方も判らないのでは??
    - Preventing Data Loss
    processorAとchannnel間: persistent message queue(永続化レイヤを持ったキューってことですかね)で対処
    channelとprocessorB間: client acknowledge modeで対処
    processorB内でのデータ永続化: acid
    - Broadcast Capabilities
    単一のpublisherに複数のsubscriber
    - Request-Reply
    非同期処理の結果をpublish元が知る必要のある場合: 戻り用のqueueを用意して、blocking waitする(これ非同期でやる意味ある?? blocking waitさせるということは、このインスタンスは結果が戻るまで別処理を実行できないということ??)
    - Choosing Between Request-Based and Event-Based
    下記
    - Hybrid Event-Driven Architectures
    まあhybridになるでしょうね
    - Architecture Characteristics Ratings
    この星表は体感と合わない。
    deployはもっと高くていい。
    elasticityは5で良くないか。
    overallコストは判断分かれる。トランザクション管理が入ると上がる気がする。
    performanceは盛りすぎ。
    reliabilityはもっと高くていい。
    testablityももっと高くていい。疎結合にしてるのにテスト性が低いってどういうことだ。
    number of quantaに裏のdb instance数を紐付けないほうがいい気がする。それ言い出すとほとんどのシステムは1。
    ドメインの認定と分割をどうするかのほうが大事な気がしてきた。
    なんか思ってるイベント駆動の解説と違った。

| Advantage over request based | Trade offs | comment |
| -------- | -------- | -------- |
| Better response to dynamic user content | Only supports eventual consistency | better responseは何のことだ。キューが外部リソースだとネットワーク時間で笑えないことになるぞ。結果整合性はトレードオフか？ |
| Better scalability and elasticity | Less control over processing flow | mediatorの場合はless controlでもないような。 |
| Better agility and chage management | Less certainty over outcome of event flow |  |
| Better responsiveness and performance |  | performance的にbetterかと言われると?? |
| Better real time decision making |  | これどこから出てきた |
| Better reaction to situational awareness |  | これもどこから出てきた |

### written by @takemon

- Chap.14
オライリー契約しました。次回から勉強してきます。